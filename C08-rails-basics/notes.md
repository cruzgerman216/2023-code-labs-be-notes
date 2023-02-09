## Ruby on Rails Basics

### Byte Size News Todos

- [ ] Create Migration File to create Issues table
- [ ] Create Issue model
- [ ] Create a couple of issue records via the Rails console
- [ ] Create index file for issues
- [ ] Adjust search to search for issues

### Create a Migration file for News Issues

Create a migration file by entering the following in the command line

```
  rails g migration CreateIssues
```

**db/migrate/YYYYDDMMTimestamp**

- add columns title and content

```ruby
class CreateIssues < ActiveRecord::Migration[7.0]
  def change
    create_table :issues do |t|
      t.string :title
      t.string :content
      t.timestamps
    end
  end
end
```

To execute this file run the following

```
rails db:migrate
```

### Create Issue Model

In **app/models**, create **issue.rb**

- Define a class called Issue that inherits from ApplicationRecord

**app/models/issue.rb**

```ruby
class Issue < ApplicationRecord
end
```

### Create Issues through the Console

Enter the following

`rails console`

- Create an unsaved issue record by calling new
- Save the record to the database by calling save

```r
irb(main):001:0> issue = Issue.new(title: "SEMO Devs Marks One Year Since Created", content: "Meetings are every 3rd Wednesday of every month")
=>
#<Issue:0x000000010ec44d70
...
irb(main):002:0> issue.save
  TRANSACTION (0.1ms)  begin transaction
  Issue Create (0.6ms)  INSERT INTO "issues" ("title", "content", "created_at", "updated_at") VALUES (?, ?, ?, ?)  [["title", "SEMO Devs Marks One Year Since Created"], ["content", "Lorem Ipsum"], ["created_at", "2023-02-01 01:51:13.882772"], ["updated_at", "2023-02-01 01:51:13.882772"]]
  TRANSACTION (0.9ms)  commit transaction
=> true
irb(main):003:0> Issue.all
  Issue Load (0.8ms)  SELECT "issues".* FROM "issues"
=>
[#<Issue:0x000000010e95f510
  id: 1,
  title: "SEMO Devs Marks One Year Since Created",
  content: "Lorem Ipsum",
  created_at: Wed, 01 Feb 2023 01:51:13.882772000 UTC +00:00,
  updated_at: Wed, 01 Feb 2023 01:51:13.882772000 UTC +00:00>]
irb(main):004:0>
```

Create a record and then save by calling create

```r
irb(main):004:0> Issue.create(title: "Springfield Devs", content: "Meetings are every 1st Wednesday of every month")
  TRANSACTION (0.1ms)  begin transaction
  Issue Create (0.4ms)  INSERT INTO "issues" ("title", "content", "created_at", "updated_at") VALUES (?, ?, ?, ?)  [["title", "Springfield Devs"], ["content", "Meetings are every 1st Wednesday of every month"], ["created_at", "2023-02-01 01:59:51.018681"], ["updated_at", "2023-02-01 01:59:51.018681"]]
  TRANSACTION (1.0ms)  commit transaction
=>
#<Issue:0x000000010e633918
 id: 2,
 title: "Springfield Devs",
 content: "Meetings are every 1st Wednesday of every month",
 created_at: Wed, 01 Feb 2023 01:59:51.018681000 UTC +00:00,
 updated_at: Wed, 01 Feb 2023 01:59:51.018681000 UTC +00:00>
irb(main):005:0> Issue.all
  Issue Load (0.2ms)  SELECT "issues".* FROM "issues"
=>
[#<Issue:0x000000010e5c1160
  id: 1,
  title: "SEMO Devs Marks One Year Since Created",
  content: "Lorem Ipsum",
  created_at: Wed, 01 Feb 2023 01:51:13.882772000 UTC +00:00,
  updated_at: Wed, 01 Feb 2023 01:51:13.882772000 UTC +00:00>,
 #<Issue:0x000000010e5c1070
  id: 2,
  title: "Springfield Devs",
  content: "Meetings are every 1st Wednesday of every month",
  created_at: Wed, 01 Feb 2023 01:59:51.018681000 UTC +00:00,
  updated_at: Wed, 01 Feb 2023 01:59:51.018681000 UTC +00:00>]
irb(main):006:0>
```

Exit the console by entering

```r
  exit
```

### Adding Validators to Issues

- Make sure title is never null and has character length of 2 to 75
- Make sure content is never null and has character length of 2 to 300

**app/models/issue.rb**

```ruby
class Issue < ApplicationRecord
  validates :title, presence: true, length: {minimum: 2, maximum: 75}
  validates :content, presence: true, length: {minimum: 2, maximum: 300}
end
```

Try creating an issue without any information included for title and content

```r
irb(main):001:0> issue = Issue.new
=> #<Issue:0x000000010a752be0 id: nil, title: nil, content: nil, created_at: nil, updated_at: nil>
irb(main):002:0> issue.save
=> false
irb(main):003:0> issue.errors.full_messages
=>
["Title can't be blank",
 "Title is too short (minimum is 2 characters)",
 "Content can't be blank",
 "Content is too short (minimum is 2 characters)"]
irb(main):004:0>
```

- update a book with the `update` method
- delete a book with the `destroy` method

### Create index action for Issues

- Define a route that will allow the user to navigate to a page that lists all Issues.

**config/routes.rb**

```ruby
  get '/issues', to: 'issues#index'
```

**controllers**

- Create a file called issues_controller.rb

```ruby
class IssuesController < ApplicationController
  def index

  end
end
```

- In index, declare an instance variable and set that to all issues from the db

```ruby
  def index
    @issues = Issue.all
  end
```

**views**

Under the views directory,

- Create a folder called issues
- In issues, create a file called index.html.erb

**views/issues/index.html.erb**

Iterate through @issues and print out each content.

```html
<h1>List of all News Issues</h1>
<% @issues.each do |issue| %>
<h2><%= issue.title%></h2>
<p><%= issue.content%></p>
<% end %>
```

**views/shared/\_nav.html.erb**

- Add a link to issues

```html
<ul>
  <li><%= link_to "Home", root_path %></li>
  <li><%= link_to "About", about_path %></li>
  <li><%= link_to "Issues", issues_path %></li>
</ul>
```

### Implementing the search for issues

**app/models/issue.rb**

- add a class method called search
  - call `where` to filter out the issues given by the user input
    - user input should match any set of characters in title or content

```ruby
class Issue < ApplicationRecord
  validates :title, presence: true, length: {minimum: 2, maximum: 75}
  validates :content, presence: true, length: {minimum: 2, maximum: 300}

  def self.search(query)
    where('lower(title) LIKE :query OR lower(content) LIKE :query', query:"%#{query.downcase}%")
  end
end
```

**app/controllers/news/search_controller.rb**

- declare an instance variable and set that to the filtered issues by search

```ruby
module News
  class SearchController < ApplicationController
    def search_news
      @issues = Issue.search(params[:query])
    end
  end
end
```

**app/views/news/search/search_news.html.erb**

```html
<h1>Search Feed</h1>

<% @issues.each do |issue| %>
<h2><%= issue.title %></h2>

<p><%= issue.content %></p>
<% end %>
```

Now test it out and search SEMO. You should see just SEMO show. If you search devs, you should get both records.

### Exercises

<hr />

**1.1 Migrations, Models, and Records**

- create a new rails project called 'job_postings'
- Create a migration file for a job posting with the following properties:
  - Title
  - Company
  - Salary
  - Location(in-house/remote)
- Create a model for a job posting requiring the title, company, and salary to be present.
- Then create three records of a job posting using the rails console

**1.2 Controllers and Views**

- Create a route for listing out all job postings (hint: `index`)
- Create a job posting controller to handle the logic for the view
- Create a view for the index route that lists all job postings
- Once you have a list of all job postings, create a search bar that allows a user to search for a specific job.

**1.3 Filtering**

- Create a new action in the job posting controller called `remote_jobs_list`
- Create a few more (at least 3 more) records using the rails console, make sure to add the location either "in-house", or "remote"
- In the `remote_jobs_list` controller action, create an instance variable that stores only the jobs that are remote.
- Create a view for listing out only remote jobs. List out `each` remote job listing
- Create a route that directs the user to the remote job listings page.
- Make a `link_to` that allows the user to see the remote jobs route from anywhere on the page.
