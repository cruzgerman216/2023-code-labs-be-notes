# Rails Active Record Associations

## Books and Categories Relationship

```
rails g scaffold Book title:string summary:string image_path:string
```

```
rails g scaffold Category name:string
```

```
rails g migration createBooksCategories
```

```ruby
class CreateBooksCategories < ActiveRecord::Migration[7.0]
  def change
    create_table :books_categories do |t|
      t.belongs_to :book, null: false, foreign_key: true
      t.belongs_to :category, null: false, foreign_key: true

      t.timestamps
    end
  end
end
```

```
rails db:migrate
```

**app/models/category.rb**

```ruby
class Category < ApplicationRecord
  has_and_belongs_to_many :books
end
```

**app/models/book.rb**

```ruby
class Book < ApplicationRecord
  has_and_belongs_to_many :categories
end
```

```r

irb(main):001:0> category = Category.create(name:"fiction")
  TRANSACTION (0.1ms)  begin transaction
  Category Create (0.9ms)  INSERT INTO "categories" ("name", "created_at", "updated_at") VALUES (?, ?, ?)  [["name", "fiction"], ["created_at", "2023-02-05 21:34:06.891955"], ["updated_at", "2023-02-05 21:34:06.891955"]]
  TRANSACTION (1.3ms)  commit transaction
=>
#<Category:0x000000010af01828
...
irb(main):002:0> category.books
  Book Load (0.2ms)  SELECT "books".* FROM "books" INNER JOIN "books_categories" ON "books"."id" = "books_categories"."book_id" WHERE "books_categories"."category_id" = ?  [["category_id", 1]]
=> []
irb(main):003:0> category.books.create(title: "It", summary: "A scary clown", image_path: "https://static1.funidelia.com/26977-f6_big2/deluxe-it-the-movie-pennywise-costume-for-men.jpg")
  TRANSACTION (0.1ms)  begin transaction
  Book Create (0.8ms)  INSERT INTO "books" ("title", "summary", "image_path", "created_at", "updated_at") VALUES (?, ?, ?, ?, ?)  [["title", "It"], ["summary", "A scary clown"], ["image_path", "https://static1.funidelia.com/26977-f6_big2/deluxe-it-the-movie-pennywise-costume-for-men.jpg"], ["created_at", "2023-02-05 21:35:36.160357"], ["updated_at", "2023-02-05 21:35:36.160357"]]
  Category::HABTM_Books Create (0.3ms)  INSERT INTO "books_categories" ("book_id", "category_id", "created_at", "updated_at") VALUES (?, ?, ?, ?)  [["book_id", 1], ["category_id", 1], ["created_at", "2023-02-05 21:35:36.182302"], ["updated_at", "2023-02-05 21:35:36.182302"]]
  TRANSACTION (1.6ms)  commit transaction
=>
#<Book:0x000000010b55a940
 id: 1,
 title: "It",
 summary: "A scary clown",
 image_path: "https://static1.funidelia.com/26977-f6_big2/deluxe-it-the-movie-pennywise-costume-for-men.jpg",
 created_at: Sun, 05 Feb 2023 21:35:36.160357000 UTC +00:00,
 updated_at: Sun, 05 Feb 2023 21:35:36.160357000 UTC +00:00>
irb(main):004:0>
```

## Setup

```
  rails g controller Pages home
```

**views/pages/home.html.erb**

```
  <h1>Welcome to Book It</h1>
  <h2>Discover a New Journey</h2>
  <p>Start discovering today by browsing our books</p>
```

**config/routes.rb**

```
Rails.application.routes.draw do
  root to: "pages#home"
end
```

## Book and Review Relationship

```
rails g model Review book:belongs_to rating:integer content:string
```

```
rails db:migrate
```

**app/model/review.rb**

```ruby
class Review < ApplicationRecord
  belongs_to :book
end
```

**app/model/book.rb**

```ruby
class Book < ApplicationRecord
  has_and_belongs_to_many :categories
  has_many :reviews, dependent: :destroy
end
```

- dependent: :destroy will delete all reviews that are associated with the book itself.

```r
irb(main):005:0> book = Book.first
  Book Load (0.3ms)  SELECT "books".* FROM "books" ORDER BY "books"."id" ASC LIMIT ?  [["LIMIT", 1]]
=>
#<Book:0x000000010cf66a78
...
irb(main):006:0> book.reviews.create(rating: 5, content: "Had to leave the movie theatre early!")
  TRANSACTION (0.1ms)  begin transaction
  Review Create (0.8ms)  INSERT INTO "reviews" ("book_id", "rating", "content", "created_at", "updated_at") VALUES (?, ?, ?, ?, ?)  [["book_id", 1], ["rating", 5], ["content", "Had to leave the movie theatre early!"], ["created_at", "2023-02-05 21:48:14.640510"], ["updated_at", "2023-02-05 21:48:14.640510"]]
  TRANSACTION (1.1ms)  commit transaction
=>
#<Review:0x000000010c9d7440
 id: 1,
 book_id: 1,
 rating: 5,
 content: "Had to leave the movie theatre early!",
 created_at: Sun, 05 Feb 2023 21:48:14.640510000 UTC +00:00,
 updated_at: Sun, 05 Feb 2023 21:48:14.640510000 UTC +00:00>
irb(main):007:0> book.reviews
  Review Load (0.2ms)  SELECT "reviews".* FROM "reviews" WHERE "reviews"."book_id" = ?  [["book_id", 1]]
=>
[#<Review:0x000000010c9d7440
  id: 1,
  book_id: 1,
  rating: 5,
  content: "Had to leave the movie theatre early!",
  created_at: Sun, 05 Feb 2023 21:48:14.640510000 UTC +00:00,
  updated_at: Sun, 05 Feb 2023 21:48:14.640510000 UTC +00:00>]
irb(main):008:0>
```

### Populating DB

**gemfile**

```ruby
gem 'faker'
```

run in the terminal

```
bundle install
```

**db/seeds.rb**

```ruby
# Create 5 categories
(0..5).each do
  category = Category.create(name: Faker::Book.genre)
end

categories = Category.all

# Create books based on each category
(0..rand(0..5)).each do
  book = Book.new(title: Faker::Book.title, summary: Faker::Lorem.paragraph, image_path: "https://blog.springshare.com/wp-content/uploads/2010/02/nc-md.gif")
  # randomly choose categorires for books
  book.categories = categories.sample(rand(0..6))
  book.save
    # Create reviews based on each book
    (0..rand(0..5)).each do
      book.reviews.create(rating: (rand(0..5)), content: Faker::Lorem.paragraph)
    end
end
```

run

```
rails db:seed
```

### Adjusting Routes

**config/routes.rb**

```ruby
Rails.application.routes.draw do
  resources :categories
  resources :books do
    resources :reviews
  end
  root to: "pages#home"
end
```

- Create a navbar

**app/views/shared/\_nav.html.erb**

```
<ul>
  <li><%= link_to "Home", root_path%></li>
  <li><%= link_to "List of Books", books_path%></li>
</ul>
```

- Add to application layout

**app/views/layouts/application.html.erb**

```html
<body>
  <%= render 'shared/nav'%> <%= yield %>
</body>
```

### Adjusting the UI

**app/views/\_book.html.erb**

```html
<div id="<%= dom_id book %>">
  <% book.categories.each do |category|%>
  <b><%= category.name%></b>
  <% end %>
  <p>
    <strong>Title:</strong>
    <%= book.title %>
  </p>

  <p>
    <strong>Summary:</strong>
    <%= book.summary %>
  </p>

  <p>
    <strong>Image path:</strong>
    <%= image_tag book.image_path %>
  </p>
</div>
```

**app/views/books/_form_.html.erb**

```html
<div>
  <%= form.label :categories %> <%= form.collection_select(:category_ids,
  Category.all, :id, :name, {}, { multiple: true }) %>
</div>
```

**app/controllers/books_controllers.rb**

```ruby
    def book_params
      params.require(:book).permit(:title, :summary, :image_path, category_ids: [])
    end
```

**app/views/books/show.html.erb**

```
<p style="color: green"><%= notice %></p>

<%= render @book %>

<h1>Reviews</h1>
<% @book.reviews.each do |review| %>
<div>
    <% (0..review.rating-1).each do |i| %>
    &#9733;
    <% end %>
</div>
<p><%= review.content %></p>
<% end %>
<div>
  <%= link_to "Edit this book", edit_book_path(@book) %> | <%= link_to "Back to books", books_path %>
   <%= button_to "Destroy this book", @book, method: :delete %>
</div>
```

## Creating a Review

**app/views/books/show.html.erb**

- Add a link to the book show page to create a link

```
<div>
  <%= link_to "Edit this book", edit_book_path(@book) %> |
  <%= link_to "Back to books", books_path %>
  |
  <%= link_to "Create a review", new_book_review_path(@book) %>
  <%= button_to "Destroy this book", @book, method: :delete %>
</div>
```

Create a reviews controller file. Adjust the new method.

```ruby
class ReviewsController < ApplicationController
  def new
      @book = Book.find(params[:book_id])
      @review = @book.reviews.new
  end

  def create
  end

  def destroy

  end
end
```

**views/reviews/new.html.erb**

```
<h1>Create a review for <%= @book.title%> </h1>

<% if @review.errors.any? %>
  <% @review.errors.full_messages.each do |message| %>
    <%= message %>
  <% end %>
<% end %>

<%= form_with(model: @review, url: book_reviews_path(@book)) do |form| %>
  <div>
    <%= form.label :rating %>
    <%= form.select :rating, options_for_select((0..5).to_a)%>
  </div>

  <div>
    <%= form.label :content %>
    <%= form.text_field :content%>
  </div>


  <div><%= form.submit %></div>
<% end %>
```

**controllers/reviews_controller.rb**

```ruby
  def create
    @book = Book.find(params[:book_id])
    @review = @book.reviews.new(permit_review_params)
    if @review.save
      redirect_to book_path(@book)
    else
      render :new, status: :unprocessable_entity
    end
  end

  private

  def permit_review_params
    params.require(:review).permit(:rating, :content)
  end

```

### Deleting Review

```ruby
  def destroy
    @book = Book.find(params[:book_id])
    @review = Review.find(params[:id])
    @review.destroy
    redirect_to @book
  end
```

**app/views/books/show.html.erb**

```
<h1>Reviews</h1>
<% @book.reviews.each do |review| %>
  <div>
    <% (0..review.rating-1).each do |i| %>
    &#9733;
    <% end %>
  </div>
  <p><%= review.content %></p>
  <%= button_to "Destroy this review",book_review_path(@book, review),  method: :delete %>
<% end %>
```

### Categories

**app/views/shared/\_nav.html.erb**

```html
<ul>
  <li><%= link_to "Home", root_path%></li>
  <li><%= link_to "List of Books", books_path%></li>
  <li><%= link_to "Categories", categories_path%></li>
</ul>
```

**app/views/categories/show.html.erb**

- render all books to each category

```
<p style="color: green"><%= notice %></p>

<%= render @category %>

<h2>List of books</h2>
<% @category.books.each do |book| %>
  <h3><%= book.title%></h3>
  <p><%= book.summary%></p>
    <%= link_to "Show", book_path(book) %>
<% end %>
<div>
  <%= link_to "Edit this category", edit_category_path(@category) %> |
  <%= link_to "Back to categories", categories_path %>

  <%= button_to "Destroy this category", @category, method: :delete %>
</div>
```

### Exercises

<hr />

**Exercise 1: One To Many Relationship**

- Create a new Rails application. Establish a has_many and belongs_to association between blogs and users. 
  - A blog belongs to a user 
  - A user has many blogs 

A blog will have the following attributes 
- Title
- content 

A user 
- email
- first_name
- last_name 

What table will have the foreign key? 

In the console, create a single user. Allow this user to have 2 blogs. 

**Exercise 2: Many To Many Relationship**
- Create a new Rails application. Establish a many to many relationship between courses and students

- A course will have the following attributes 
  - name 
- A student will have the following attributes 
  - first_name
  - last_name 

Be sure to establish a third table to create this association.

In the Rails console, create several courses and students. 

Allow a student to have more than one course. 

**Exercise 3: has_and_belongs_to_many association**

What's the difference between a has_many through and a has_and_belongs_to_many association? 

- Create a new Rails application. Establish a has_and_belongs_to_many association between articles and tags. 
- A article can have many tags with the following attributes
  - title, content 
- A tag can have many articles with the following attributes 
  - name

Use the Rails console to create a few tags and a few articles. Be sure to make each article has at least one tag and every tag has at least one article.

- Create a RESTful application by defining all RESTful routes for articles and tags and defining their actions and appropriate views. 

Articles 
- In the index page, a user should see all the articles listed as well as their tags. 

**Bonus**
Allow the user to comment under articles
