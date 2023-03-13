      ___  __  ____  ____  ____  __    ____   __   ____  ____     __   ____  __
     / __)/  \(    \(  __)(  __)(  )  (  _ \ / _\ / ___)(  __)   / _\ (  _ \(  )
    ( (__(  O )) D ( ) _)  ) _)  )(    ) _ (/    \\___ \ ) _)   /    \ ) __/ )(
     \___)\__/(____/(____)(__)  (__)  (____/\_/\_/(____/(____)  \_/\_/(__)  (__)

![Rails API](https://miro.medium.com/max/1400/0*CUdFIQoT8xDr3rW8.png)

# Getting Started with the Base API

---

### Table of Contents

-   <a href="#Introduction">Introduction</a>
-   <a href="#Getting-Started">Getting Started with the Base API</a>
-   <a href="#gemfile">Gemfile</a>
-   <a href="#schema">Schema</a>
-   <a href="#models">Models</a>

---

**Base API**

-   The Base API is a pre-built foundational structure that provides a starting point for development.

**Versioning**

-   Practice of maintaining different versions of an API that may have different functionality, endpoints or parameters.
-   Allows for other services such as FE clients to choose the version that is compatible with their application without worrying about breaking changes or unexpected behavior.
-   “api/v1/users”

**Credential files with environment variables**

-   Credential files are used to securely store sensitive information such as passwords, API keys, and other secrets by encrypting them. This results in the creation of a file named ‘config/credentials.yml.enc'.
-   You can access this information through environmental variables.
-   To decrypt the credential files, you need a key.

**Environments**

-   Rails provides multiple environments for your application, including test, development, production, and staging. Each environment serves a specific purpose in the application's lifecycle.
-   Each environment has its own configuration files, which allow you to customize the behavior of your application in that environment. For example, you may want to use a different database in development than in production, or you may want to use caching in production to improve performance.

    -   **Production** This environment is used to deploy your application to a live server. It is optimized for performance and stability, and all debugging and verbose error messages are disabled. This environment should be used with caution, as changes made here affect the live application.
    -   **Staging** This environment is used as a mirror of the production environment, where you can test new features and changes before deploying to the production environment. This allows you to identify and fix issues before they affect the live application.
    -   **Test** This environment is used to run automated tests for your application. Test data is generated and cleaned up automatically, and test-specific configurations are used to ensure that your tests run consistently and independently.
    -   **Development** This environment is used for local development and testing. In this environment, you can test your code changes and new features without affecting the production environment. Debugging tools and verbose error messages are available to aid in the development process.

**Services**

-   A service is a class or module that encapsulates a specific set of functionality that can be shared across different parts of your application. Services are typically used to abstract complex business logic away from controllers and models, making your code more modular, reusable, and easier to test.

**Blueprinter**

-   Blueprinter is a gem that allows you to easily define and serialize objects into JSON, which is a popular format for sending and receiving data over the web. Blueprinter provides a simple DSL (domain-specific language) for defining the structure of your JSON responses, which makes it easy to customize the data that you want to return.

**Sendgrid**

-   SendGrid is an integration of Twilio.Twilio acquired SendGrid in 2018. SendGrid is an email marketing and communication platform that provides businesses with the ability to send emails in bulk.

**Sidekiq**

-   Sidekiq provides a simple and efficient way to execute background jobs asynchronously, freeing up the application's main thread to handle incoming requests.

**Twilio**

-   Twilio is a cloud communications platform that provides APIs for developers to easily integrate communication features such as voice, video, messaging, and authentication into their applications.

---

<div id="Introduction"></div>

## Introduction

You have now experience a Full Stack Ruby on Rails development process. It's more and more apparent however that, Rails is used not only for it's MVC architect but for API purposes! That's right, with the advent of Front End Frameworks (Angular), Rails can definitely be used in the server side as an API!

### What is an API?

API stands for application programming interface. An API is the communication between two programs or computers. One specific type of API we will focus on are RESTful APIs

REST stands for Representational State Transfer. In REST, HTTP verbs are standard protocol, here's an example of how these HTTP Verbs align with Rails actions. The good thing is, Rails already has RESTful like features built in as we've seen throughout the curriculum.

<img src="https://miro.medium.com/max/1324/1*OdQfB6npJJtjMDDoRzehVw.png" width="400px">

### Client-Server Architecture

The specific type of relationship we like to build is the client-server architecture. This style pattern allows our client side application (Angular app) to communicate with our server/Back End Rails API. This standard principle introduces a separation of concerns in which dissembles two applications. One side, client side. The other side, server side. This improves scalability and "it allows components to evolve independently".

<img src="https://i.pinimg.com/originals/d6/a1/27/d6a12727a608673c4a097378abcee581.jpg" width="400px">

---

<div id="Getting-Started"></div>

## Getting Started with the Base API

Before we start, keep in mind when reading code, how descriptive and how meaningfully worded each method, attributes, ect are. Clean code will really help you understand what something will do without knowing the logic behind it.

The Base API, provided by the Codefi team, is an **AWESOME** starter kit for developing a Rails API. The purpose of this section of the Back End is to get use to pre-existing code that's been handed to you, absorb all of it's available features and develop amazing APIs. We expect that when you are going into a technical interview, you will explain the workflow of the API and how you used it to your advantage. Keep in mind, we won't be using all of it's features (sending emails to users unless you really want to pay for that service) in the program but perhaps later down the road, you will. Sure you can [develop your own API from scratch](https://guides.rubyonrails.org/api_app.html) but again, the purpose of this module is to add features to pre-existing code and create a Full Stack Application (Front End Angular/Back End Rails). When you get hired, the first thing you'll do is get use to the code base and from there, add features. We are simulating that environment here.

Here is the [remote repository](https://github.com/leehodges/CodeLabsApi) for the base API we will be using. Click `use this template`.

Please fork the repo and open it in Visual Studio Code. These notes will guide you in understanding the Base API and explore it's available features. Experiment. Get curious and start building!

### README

The `README.md` should be the very first thing you go over. The `README.md` file will go over the necessary steps to configuring the API. Let's go over it!

### Version Requirement

The API is written in Ruby `3.2.0` and Rails `7.0.4.1`.

### Setup

From the [README.md](https://github.com/leehodges/CodeLabsApi#readme) there are two paths to the setup: `New Projects` and `Existing Project`. In this case, we are starting out fresh so we will go ahead with the `New Projects` setup.

### Change Databases 

When you use the base api template more than once, you might notice some odd behavior with your database like having already created data. That's because you may have used the template more than once.

Go to your `config/database.yml` and change the database names. For example 

```ruby
development:
  <<: *default
  database: BaseAPI_development
```

Change BaseAPI to your project name 

```ruby 
development:
  <<: *default
  database: ProjectName_development
```

Repeat this for testing and production.

### Rails Encrypted Credentials

When our application interacts with an external service, there will be times we will need keys/tokens to unlock the features of this service. Exposing this information to the public is dangerous and people can take advantage of this sensitive information. For instance, if your open source project is in GitHub, you don't want to share your private information. Pushing sensitive information should never be pushed to GitHub. In other instances, perhaps in a private environment, your local settings may not be suitable to your team. This is where Rails Encrypted Credentials come into play.

<img src="https://i1.wp.com/blog.magmalabs.io/wp-content/uploads/2022/03/Data-Encryption-with-Rails-7-SM_OG.png?fit=1200%2C628&ssl=1" width="400px">

Credentials such as keys/token/ect are stored in an encrypted file called `credentials.yml.enc`. Let's go ahead and generate this file.

Run `bin/rails credentials:edit`. We get an error

```
No $EDITOR to open file in. Assign one like this:

EDITOR="mate --wait" bin/rails credentials:edit

For editors that fork and exit immediately, it's important to pass a wait flag,
otherwise the credentials will be saved immediately with no chance to edit.
```

In order to run this command, you would first need to include your code editor in the format of

`EDITOR="code --wait" bin/rails credentials:edit`

`code` represents VS Code. Run `EDITOR="code --wait" bin/rails credentials:edit` in your terminal. This command will generate a new file called `master.key` and `credentials.yml.enc.` This is a way to store the applications hidden keys.

<details>
  <summary><strong>Note</strong></summary>
In order for you to decrypt `credentials.yml.enc` and see your hidden keys, you first would need the `master.key`. When running `EDITOR="code --wait" bin/rails credentials:edit` again, Rails will look for `master.key` and use it to decrypt `credentials.yml.enc`. `mastery.key` holds a value that you want to share with your team (this file is automatically ignored so we don't have to worry about accidentally pushing to github).
</details>

In the base API, credential files are parallel with the environments Rails includes. In `config/environments`, notice three files "production", "development" and "test".

When you run `rails s`

You get an error.

```
/Users/germancruz/Desktop/bapidemo/config/initializers/rswag_ui.rb:15:in `block in <main>': undefined method `[]' for nil:NilClass (NoMethodError)

  c.basic_auth_credentials Rails.application.credentials[:swagger][:username], Rails.application.credentials[:swagger][:password]
```

This is because, running rails s is running the server locally on your computer and this is considered the development environment.

This error has something to do with the environment variables that the app is dependent upon in each environment. This means you have to include environmental variables in each environment.

Let's add environmental variables for the development environment. First,

Delete `development.yml.enc`.

Run in the following:

```
EDITOR="code --wait" bin/rails credentials:edit --environment=development
```

This will create a credential file for the development environment.

### Adding Environmental Variables

Once you have opened `development.yml.enc`, go ahead and include all environment variables. Make sure they are indented correctly in the format of:

```ruby
    invitation:
         url: 'https://urlhere'

    twilio:
        default_number: '555-555-5555'
        account_sid: 'sid_here'
        auth_token: 'auth_token'

    sendgrid:
        default_email: 'fillthisout@email.com'
        domain: 'domain.com'
        address: 'smtp.sendgrid.net'
        username: 'apikey' #apikey actually is the username to authenticate with api secret token below
        password: 'api_token'

    sidekiq:
        auth_username: 'username'
        auth_password: 'password'

    workers:
        max_threads: #
        min_threads: #
    swagger:
        username: 'username'
        password: 'password'

```

These are keys used throughout the baseAPI. Most of these keys are placed already in the application.

Let's go ahead and set the `max_threads` and `min_threads` to 5 like so

```
    workers:
        max_threads: 5
        min_threads: 5
```

Run the following

`rails s`

And you shouldn't encounter any errors.

Repeat the same thing for test.yml.enc and production.yml.enc

### Access Rails Environment Variables

Use `Rails.application.credentials` to retrieve these values e.g, `Rails.application.credentials.sendgrid[:domain]`

For example, in `config/initializers/smtb`, this is a default setup for sendgrid.

```ruby
ActionMailer::Base.smtp_settings = {
  domain: Rails.application.credentials.sendgrid[:domain],
  address: Rails.application.credentials.sendgrid[:server],
  port: 587,
  authentication: :plain,
  user_name: Rails.application.credentials.sendgrid[:username],
  password: Rails.application.credentials.sendgrid[:api],
  :enable_starttls_auto => true
}
```

---

<div id="gemfile"></div>

## Gemfile

Let's take a look at what gems this API contains.

```ruby
source 'https://rubygems.org'
git_source(:github) { |repo| "https://github.com/#{repo}.git" }

ruby '3.2.0'

# ================== The BASICS ========================
# Bundle edge Rails instead: gem 'rails', github: 'rails/rails', branch: 'main'
gem 'rails', '~> 7.0.4.1'
# Use postgresql as the database for Active Record
gem 'pg', '>= 1.1'
# Use Puma as the app server
gem 'puma', '>= 5.0'
# Specify version, per dependabot
gem 'activesupport', '>= 6.1.3.1'
# Use Redis adapter to run Action Cable in production
gem 'redis', '>= 4.0'
# Use Active Model has_secure_password
gem 'bcrypt', '>= 3.1.7'
# Reduces boot times through caching; required in config/boot.rb
gem 'bootsnap', '>= 1.4.4', require: false


# ======================== RACK GEMS =======================
# Use Rack CORS for handling Cross-Origin Resource Sharing (CORS), making cross-origin AJAX possible
gem 'rack-attack'
gem 'rack-cors'

# ======================== Background Jobs Gems ========================
gem 'sidekiq'
gem 'sidekiq-scheduler'

# ======================== Communication Gems ========================
gem 'sendgrid-ruby'
gem 'twilio-ruby'

# ======================== JSON Serialization Gems ========================
gem 'blueprinter'
gem 'oj'
gem 'oj_mimic_json'

# ======================== Miscellaneous Gems ========================
gem 'to_bool', '~> 2.0'
gem 'faker', :git => 'https://github.com/faker-ruby/faker.git', :branch => 'main'

# ==================== Documentation Gems ====================
gem 'rswag'

# ==================== rSwag Gems =======================
gem 'rspec-rails'
gem 'rswag-specs'



# ======================== Development Gems ========================
group :development, :test do
  # Call 'byebug' anywhere in the code to stop execution and get a debugger console
  gem 'byebug', platforms: [:mri, :mingw, :x64_mingw]

  gem 'factory_bot_rails'
end

group :development do
  gem 'annotate'
  gem 'listen', '~> 3.3'
  # Spring speeds up development by keeping your application running in the background. Read more: https://github.com/rails/spring
  gem 'spring'
  # The commented out gem below speeds up spring, but is currently not compatible with latest version of Rails, it should be compatible shortly,
  # check projects github to subscribe to updates
  # gem 'spring-watcher-listen'

end

# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw, :jruby]
# If Platform Windows, monitor window directory changes
gem 'wdm', '>= 0.1.0' if Gem.win_platform?

```

```
I try to use as few gems as possible to achieve what needs done. While there are many gems for doing nearly anything, I've found that they often add significant amounts of memory bloat, and that I can often implement the limited set of functionalities I need that the gem provides with just a little bit of work. So, keep it lean; Rails makes it very easy to run high-memory applications.
```

#### Sidekiq and Sidekiq scheduler

```ruby
# ======================== Background Jobs Gems ========================
gem 'sidekiq'
gem 'sidekiq-scheduler'
```

[Sidekiq](https://github.com/mperham/sidekiq) is a service for background workers. You will need to run [Redis](https://www.rubyguides.com/2019/04/ruby-redis/) to store jobs. You can think of workers being scheduled to do certain jobs such as emailing a user for their monthly bill. We aren't concerned with Sidekiq at the moment but it's helpful to know what it is.

#### Sengrid

[Sendgrid](https://github.com/sendgrid/sendgrid-ruby) will allow you to send emails using their service.

#### Twilio

[Twilio](https://github.com/twilio/twilio-ruby) will allow you to send sms messages using their service.

#### BluePrinter

A easy and organize way to serialize your data.

<div id='schema'></div>

## Schema

Before diving into a Rails application, let's check out what our schema looks like.

```ruby
ActiveRecord::Schema[7.0].define(version: 2021_11_22_185403) do
  # These are extensions that must be enabled in order to support this database
  enable_extension "plpgsql"

  create_table "roles", force: :cascade do |t|
    t.string "slug"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
  end

  create_table "tokens", force: :cascade do |t|
    t.bigint "user_id", null: false
    t.string "value"
    t.datetime "expiry", precision: nil
    t.string "ip"
    t.datetime "revocation_date", precision: nil
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
    t.index ["user_id"], name: "index_tokens_on_user_id"
  end

  create_table "user_roles", force: :cascade do |t|
    t.bigint "user_id", null: false
    t.bigint "role_id", null: false
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
    t.index ["role_id"], name: "index_user_roles_on_role_id"
    t.index ["user_id"], name: "index_user_roles_on_user_id"
  end

  create_table "users", force: :cascade do |t|
    t.string "email", null: false
    t.string "first_name", null: false
    t.string "last_name", null: false
    t.string "phone", null: false
    t.string "password_digest", null: false
    t.boolean "invitation_accepted", default: false
    t.string "invitation_token"
    t.datetime "invitation_expiration", precision: nil
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
    t.index ["email"], name: "index_users_on_email", unique: true
  end

  add_foreign_key "tokens", "users"
  add_foreign_key "user_roles", "roles"
  add_foreign_key "user_roles", "users"
end

```

Here is a visual representation of the schema in a ERD.

![Base API ERD](../assets/images/C21/baseAPI-erd.png)

Let's talk about the data here. The base API has provided a series of tables: `users`, `roles`, `user_roles`, and `tokens`.

#### Users table

The users table has common attribute such as

```ruby
  create_table "users", force: :cascade do |t|
    t.string "email"
    t.string "first_name"
    t.string "last_name"
    t.string "phone"
    t.string "password_digest"
    t.boolean "invitation_accepted", default: false
    t.string "invitation_token"
    t.datetime "invitation_expiration"
    t.datetime "created_at", precision: 6, null: false
    t.datetime "updated_at", precision: 6, null: false
    t.index ["email"], name: "index_users_on_email", unique: true
  end
```

Notice how we have attributes `invitation_accepted`, `invitation_token`, `invitation_expiration`. These are mainly for verifying an email by sending an invitation email.

#### User_Roles table

```ruby
  create_table "user_roles", force: :cascade do |t|
    t.bigint "user_id", null: false
    t.bigint "role_id", null: false
    t.datetime "created_at", precision: 6, null: false
    t.datetime "updated_at", precision: 6, null: false
    t.index ["role_id"], name: "index_user_roles_on_role_id"
    t.index ["user_id"], name: "index_user_roles_on_user_id"
  end
```

This table will establish a connection between the users table and the roles table.

#### Roles table

```ruby
  create_table "roles", force: :cascade do |t|
    t.string "slug"
    t.datetime "created_at", precision: 6, null: false
    t.datetime "updated_at", precision: 6, null: false
  end
```

The roles table will keep track of the type of role a user has via `slug`.

If you navigate to `migrations/20211122185138_create_user_roles`, notice `references`.

```ruby
      t.references :user, null: false, foreign_key: true
      t.references :role, null: false, foreign_key: true
```

References will create an index for user and role. An index is a schema object that contains an entry for each value that appears in the indexed column(s) of the table or cluster and provides direct, fast access to rows. Setting `foreign_key` to `true` will also provide foreign keys.

<div id="models"></div>

## Models

Let's talk about the models of the Base API. Remember, models provide methods that are commonly used queries. We sometimes make our own custom queries. These methods don't have to be only for custom queries, maybe we like to add validations to prevent what can be saved to the database. Even as important are associations, relationships amongst two types of entities in our DB.

### User model

The user model is the most complex out of the models provided by the base API. There's a lot going on! Let's read from top to bottom.

```ruby
has_secure_password validations: false
```

By including the argument `validations:false`, this will remove validations. [source](https://api.rubyonrails.org/classes/ActiveModel/SecurePassword/ClassMethods.html)

<br>

```ruby
  has_many :tokens
  has_many :user_roles
  has_many :roles, through: :user_roles
```

Each user has a set of relationships with multiple entities. For example, in the base API, a user can have multiple tokens. This is necessary to have when logging in and being able to authorize user requests.

The next set of relationships are `user_roles` and `roles`. Creating a `has_many` relationship through `user_roles`, allows each user record to return their roles.

```ruby
validates :email, uniqueness: true
```

Every email has to be unique.

```ruby
  scope :invite_not_expired, -> { where('invitation_expiration > ?', DateTime.now) }
  scope :invite_token_is, ->(invitation_token) { where(invitation_token: invitation_token) }
```

-   `invite_not_expired` returns every user who's invite is not expired.
-   `invite_token_is` returns a user with the same invitation token.

More on [scopes](https://www.rubyguides.com/2019/10/scopes-in-ruby-on-rails/).

```ruby
  before_create :generate_invitation_token
```

Before every user is created, an invitation token is generated. This is mainly for verifying emails. Let's inspect `generate_invitation_token`, a method defined in the user model class.

```ruby
  def generate_invitation_token
    self.invitation_expiration = DateTime.current + 7.day
    loop do
      # Once we have a random, test whether it is unique in the DB
      self.invitation_token = SecureRandom.alphanumeric(15)
      break unless self.class.exists?(invitation_token: invitation_token)
    end
  end
```

```ruby
    self.invitation_expiration = DateTime.current + 7.day
```

`generate_invitation_token` stores the expiration date in `invitation_expiration` that is 7 days long. This is always changeable. Some expiration dates are 24 hours. Depending on your opinion/use case/argument.

```ruby
    loop do
      # Once we have a random, test whether it is unique in the DB
      self.invitation_token = SecureRandom.alphanumeric(15)
      break unless self.class.exists?(invitation_token: invitation_token)
    end
```

The next part of our method is a loop. You might've never seen a `loop` like this (I'd be careful, you don't want to start an infinite loop and break everything!) but it will stop when `break` is called.

`SecureRandom.alphanumeric(15)` is going to combine a set of random digits and letters, about 15 of them in one long unreadable text. As mentioned in the ruby docs `This library (SecureRandom) is an interface to secure random number generators which are suitable for generating session keys in HTTP cookies, etc.` More on [SecureRandom](https://ruby-doc.org/stdlib-2.7.0/libdoc/securerandom/rdoc/SecureRandom.html).

The loop continues and checks to see if the random value already exists, if so (highly unlikely but possible!), continue to the next iteration and generate a new value. If it doesn't already exist, then store it in `invitation_token` and break the loop! If you have a million users, doesn't hurt to check to see if there's one that exists.

Again, notice how descriptive the method name is `generate_invitation_token`, clean and precise. Let's move on to the next line of code.

```ruby
  before_save :generate_invitation_token, if: :will_save_change_to_invitation_token?
```

In case the `invitation_token` changes before saving the user, generate an invitation token instead. More on `will_save_change_to_attribute` [here](https://apidock.com/rails/v6.0.0/ActiveRecord/AttributeMethods/Dirty/will_save_change_to_attribute%3F).

### Sending Email to Invite User

```ruby
  after_commit :invite_user, if: :saved_change_to_invitation_token?
```

`after_commit`, will execute the following method `invite_user` after the user has been saved only if the `invitation_token` attribute was changed. More on `saved_changed_to_attribute` [here](https://apidock.com/rails/v5.2.3/ActiveRecord/AttributeMethods/Dirty/saved_change_to_attribute).

But what does `invite_user` do?

```ruby
  def invite_user
    # Email the user a link with the invitation_token
    InvitationWorker.perform_async(id)
  end
```

`invite_user` is another `User` method that sends a user an email via`invitation_token`. Notice how that is being performed by `InvitationWorker`. What is that? And where does that exist? Navigate to `workers/invitation_worker.rb` and you'll see the configuration setup for sending an email. We aren't going to dive into emailing users but you can find a set of notes of a step by step process to do so [here](./../other/email-users-with-sendgrid-and-sidekiq.md).

```ruby
  def invitation_accepted_at!
    update(invitation_accepted: true, invitation_token: nil, invitation_expiration: nil)
  end
```

`invitation_accepted_at` will update the invitation attributes for when the user accepts the invitation.

### Token Model

```ruby
class Token < ApplicationRecord
  belongs_to :user
end
```

The token model creates the association between tokens and users.

### user_role Model

```ruby
# Join model that connects users to roles
class UserRole < ApplicationRecord
  belongs_to :user
  belongs_to :role

  validates_uniqueness_of :user, scope: :role
end
```

### Role Model

```ruby
# frozen_string_literal: true

# Model that stores all of the available roles
class Role < ApplicationRecord
  validates_uniqueness_of :slug, presence: true

  scope :available_roles, -> { pluck(:slug) }

  def self.valid_role?(role)
    stringified_role = role.to_s.downcase.underscore
    stringified_role.in?(available_roles)
  end
end
```

## Routes

You're familiar with routes right? The requests the user makes and in return, the controllers handle these requests. I figured you knew. Let's navigate to `config/routes.rb`.

What the? What is that?

<img src="https://theactivevoice.com/wp-content/uploads/2016/08/ThinkstockPhotos-178062396-1024x683.jpg" width="200px">

```ruby
  scope :monitoring do
    # Sidekiq Basic Auth from routes on production environment
    if Rails.env.production?
      Sidekiq::Web.use Rack::Auth::Basic do |username, password|
        ActiveSupport::SecurityUtils.secure_compare(::Digest::SHA256.hexdigest(username),
                                                    ::Digest::SHA256.hexdigest(Rails.application.credentials.sidekiq[:auth_username])) &
          ActiveSupport::SecurityUtils.secure_compare(::Digest::SHA256.hexdigest(password),
                                                      ::Digest::SHA256.hexdigest(Rails.application.credentials.sidekiq[:auth_password]))
      end
    end
    mount Sidekiq::Web, at: '/sidekiq'
  end
```

This is a Sidekiq configuration block of code. `scope :monitoring` is prefixing the path such as `/monitoring`. This code block allows for basic authentication in the production environment, which will enable the web UI of Sidekiq. Sidekiq comes with a [web application](https://github.com/mperham/sidekiq/wiki/Monitoring#web-ui) that can display the current state of a Sidekiq installation. This a way to protect access to this information.

```ruby
  namespace :api, defaults: { format: :json } do
    namespace :v1 do
      namespace :users do
        post :login
        delete :logout
        get :me
        post :create
      end
    end
  end
```

Namespacing is just another way of prefixing the defined paths such as

-   logging in a user by sending a post request to `/api/v1/users/login`
-   logging out a user by sending a delete request to `/api/v1/users/logout`
-   returning the user by sending a get request to `/api/v1/users/me`
-   signing up a user by sending a post request to `/api/v1/users/create`

The default response all comes in the format of json (JavaScript Object Notation), a fast and lightweight way to send data.

Notice the paths all container the prefixes `/api/v1`. This signifies versioning which allows the API to continue to expand into other versions and development but still maintain the same resource of paths. Here's an example of what a defined version 2 set of routes may look like

```ruby
Rails.application.routes.draw do
  concern :api_base do
    resources :posts do
      resources :comments
    end
  end

  namespace :v2 do
    concerns :api_base
  end

  namespace :v1 do
    concerns :api_base
  end
end
```

<div id ="controllers"></div>

## Controllers

### Application Controller

Now, let's get to the meat of the API and move onto controllers. So far we've talk about the layout of the database, the models and associations as well as the defined routes users can request. Now how do we deal with these requests? Let's navigate to `controllers/application_controller.rb`. This class isn't inherited by any other controller class in the application but is a great baseline. Let's dissect this before moving onto version one controllers.

```ruby
class ApplicationController < ActionController::API
  include ActionController::HttpAuthentication::Token::ControllerMethods

  before_action :authenticate

  def authenticate
    authenticate_token || render_unauthorized
  end

  def authenticate_token
    authenticate_with_http_token do |token, options|
      @current_user = User.find_by(token: token)
      @current_user
    end
  end

  def render_unauthorized
    logger.debug "*** UNAUTHORIZED REQUEST: '#{request.env['HTTP_AUTHORIZATION']}' ***"
    self.headers['WWW-Authenticate'] = 'Token realm="Application"'
    render json: {error:"Bad credentials"}, status: 401
  end
end
```

Notice how `ApplicationController` is inheriting from `ActionController::API`, this is a lightweight version of `ActionController::Base`, the module we inherit when developing a FS Rails app as mentioned in the docs.

```
API Controller is a lightweight version of ActionController::Base, created for applications that don't require all functionalities that a complete Rails controller provides, allowing you to create controllers with just the features that you need for API only applications.

An API Controller is different from a normal controller in the sense that by default it doesn't include a number of features that are usually required by browser access only: layouts and templates rendering, flash, assets, and so on. This makes the entire controller stack thinner, suitable for API applications. It doesn't mean you won't have such features if you need them: they're all available for you to include in your application, they're just not part of the default API controller stack.
```

```ruby
  include ActionController::HttpAuthentication::Token::ControllerMethods
```

These methods provided by the line above is usually included by inheriting `ActionController::Base` but because we are inheriting from a downsize version, we must include this line for authorization.

```ruby
before_action :authenticate

def authenticate
    authenticate_token || render_unauthorized
end

```

Here we have defined two instances of whether a token will be authenticated or render `unauthorized`. Let's take a look at the first method defined in the very same class.

```ruby
  def authenticate_token
    authenticate_with_http_token do |token, options|
      @current_user = User.find_by(token: token)
      @current_user
    end
  end
```

Rails handles tokens from the Authorization header in any of the following formats with the `authenticate_with_http_token` method. It automatically checks the authorization header for a token and passes it in as an argument. It will then return any user that has this token.

```ruby
  def render_unauthorized
    logger.debug "*** UNAUTHORIZED REQUEST: '#{request.env['HTTP_AUTHORIZATION']}' ***"
    self.headers['WWW-Authenticate'] = 'Token realm="Application"'
    render json: {error:"Bad credentials"}, status: 401
  end
```

Using Rails logger allows us to display some useful information in the console. You can also use `puts` to log information but logger offers a few features that can be helpful.

In the next line of code `self` which refers to the instance of the controller that is handling the said request. In this case you can attach a response-type header such as `WWW-Authenticate` and set it to what is referred to as a realm. As said [here](https://www.geeksforgeeks.org/http-headers-www-authenticate/), "It serves as a support for various authentication mechanisms which are important to control access to pages and other resources as well". In this case, we are protecting the application from those who don't have valid credentials.

### Application Controller Version 1

<img src="https://cdn.vox-cdn.com/thumbor/mFiywP9BUHDC8AIRBDYJvXdfQiA=/1400x1050/filters:format(jpeg)/cdn.vox-cdn.com/uploads/chorus_asset/file/23265504/Spider_Man_meme.jpg" width="400px">

Don't get confused by file names, `controllers/application_controller.rb` acts as a layout and is just "there". While in version 1 of our application, `controllers/api/v1/application_controller.rb` includes the class our other controllers from v1 will inherit.

It looks very similiar to the original `application_controller` but has a couple more methods and also updated methods.

For example, the `authenticate_token` method.

```ruby
  def authenticate_token
    @ip = request.remote_ip || "unknown"
    authenticate_with_http_token do |token, _options|
      @token = Token.find_by(value: token)
      if @token.nil?
        render_unauthorized
      else
        if @token.expiry.after?(DateTime.now) && @token.revocation_date.blank?
          @current_user = @token.user
          @current_user
        else
          render_unauthorized
        end
      end
    end
  end
```

This method will check to see if the token exists and also checks to see if the token has been expired. If the token is valid and the token hasn't expired, return that specific user. Otherwise, call `render_unauthorized`.

---

### ensure_required_params

```ruby
  def ensure_required_params(required_params, passed_in_params)
    required_params = required_params.map(&:to_sym)
    passed_in_params = passed_in_params.keys.map(&:to_sym)

    remainder = required_params - passed_in_params

    count = remainder.size
    errors = remainder

    render json: { message: "Missing required parameters: #{errors.to_sentence}" }, status: :bad_request and return unless count.zero?
  end
```

`ensure_required_params` is a way to respond if the params are missing any require parameters. If so, then the response will include a message `"Missing required paramseters"` follow by the specific missing params.

---

### render_error

`render_error` structures an error response by including keys `success`, `errors`, and `status`.

```ruby
  def render_error(errors:, status: :internal_server_error)
    render json: {
      success: false,
      errors: errors,
    }, status: status
  end
```

`success` is automatically set to false. This is because when our Front End takes this response, we can include a condition that checks whether or not their request had failed.

`internal server error` is the status of the response, specifically a 500 error which means that something went wrong with the server.

### render_success

```ruby
  def render_success(payload:, status: :ok)
    render json: {
      success: true,
      payload: payload,
    }, status: status
  end
```

`render_success` structures a succcessful response.

## User Controller

Navigate to `controllers/api/v1/users_controller.rb`.

```ruby
# frozen_string_literal: true

module Api
  module V1
    # Handles endpoints related to users
    class UsersController < Api::V1::ApplicationController
      skip_before_action :authenticate, only: %i[login create]

      def login
        result = BaseApi::Auth.login(params[:email], params[:password], @ip)
        render_error(errors: 'User not authenticated', status: 401) and return unless result.success?

        payload = {
          user: UserBlueprint.render_as_hash(result.payload[:user], view: :login),
          token: TokenBlueprint.render_as_hash(result.payload[:token])
        }
        render_success(payload: payload)
      end

      def logout
        result = BaseApi::Auth.logout(@current_user, @token)
        render_error(errors: 'There was a problem logging out', status: :unprocessable_entity) and return unless result.success?

        render_success(payload: 'You have been logged out')
      end

      def create
        result = BaseApi::Users.new_user(params)
        render_error(errors: 'There was a problem creating a new user', status: 400) and return unless result.success?
        payload = {
          user: UserBlueprint.render_as_hash(result.payload, view: :normal)
        }
        #  TODO: Invite user to accept invitation via registered email
        render_success(payload: payload)
      end

      def me
        render_success(payload: UserBlueprint.render_as_hash(@current_user))
      end

      def validate_invitation
        user = User.invite_token_is(params[:invitation_token]).invite_not_expired.first

        render_success(payload: { validated: false }) and return if user.nil?
        render_success(payload: { validated: true })
      end
    end
  end
end
```

This controller involves a pattern that extracts logic out of the actions into services. It also extracts logic by using commonly used methods such as `render_success` and `render_error` are from `Api::V1::ApplicationController`. The reason for that is for readability purposes. It's a `size that fits all` type of situation for using `render_success` and `render_error` but also again, extracts logic so it's easier to read.

```ruby
module Api
  module V1
    # Handles endpoints related to users
    class UsersController < Api::V1::ApplicationController
    end
  end
end
```

```ruby
      skip_before_action :authenticate, only: %i[login create]
```

Here we are going to invoke `authenticate` for each action except `login` and `create`. In order for the user to fetch their information and logout, they must first be authenticated (login).

### login action

Let's dive deep into the logic action and talk about the api's pattern in controllers. So when the user sends a post to `domain-name/api/v1/users/login`, the following method will execute.

```ruby
      def login
        result = BaseApi::Auth.login(params[:email], params[:password], @ip)
        render_error(errors: 'User not authenticated', status: 401) and return unless result.success?

        payload = {
          user: UserBlueprint.render_as_hash(result.payload[:user], view: :login),
          token: TokenBlueprint.render_as_hash(result.payload[:token])
        }
        render_success(payload: payload)
      end
```

We're use to authenticating the user within this action here but we're extracted that into a module(service) called `BaseApi::Auth`. We aren't yet concerned with what login does at the moment but we know that it will handle authenticating the user. We've been doing that the entire time during our programming journey, using methods that we didn't create. This one is no difference. It takes in three parameters, email and password as well as `@ip`. `@ip` should be regarded as `request.remote_ip` which provides the ip address of the user.

`@ip` is used to create the token when logging in.

```ruby
        render_error(errors: 'User not authenticated', status: 401) and return unless result.success?
```

The next line of code will render errors and return if the result was unsucessful. Otherwise, `render_success` will be called.

```ruby
        payload = {
          user: UserBlueprint.render_as_hash(result.payload[:user], view: :login),
          token: TokenBlueprint.render_as_hash(result.payload[:token])
        }
```

A payload is information that is to be included with the response. When everything checks out, we can return a successful response.

```ruby
        payload = {
          user: UserBlueprint.render_as_hash(result.payload[:user], view: :login),
          token: TokenBlueprint.render_as_hash(result.payload[:token])
        }
        render_success(payload: payload)
```

We see something very interesting which is `UserBlueprint` and `TokenBlueprint`. These are classes from files in `blueprints` and inherits from `Blueprinter::Base` which is provided by the `Blueprinter` gem. Blueprinter allows us to serialize our data.

#### Serializing data with Blueprinter

Let's have a quick lesson on Blueprinter.

Please navigate to `blueprints/user_blueprint.rb`. Blueprinter takes hashes and serializes them into JSON objects. Blueprinter relies on the idea of predefining different ways of structuring the info being sent back in the response. Let's say in some responses, you don't want to include timestamps and other responses you do, so you are "predefining output for data in different contexts". A class that inherits from `BluePrinter::Base` looks like this. By inheriting from `BluePrinter::Base`, we get methods such as `identifier`, `fields` and more.

```ruby
# frozen_string_literal: true

# Defines the JSON blueprint for the User model
class UserBlueprint < Blueprinter::Base
  identifier :id
  fields :first_name, :last_name, :name, :email

  view :login do
    association :token, blueprint: TokenBlueprint do |user, _options|
      user.tokens.last
    end
  end

  view :normal do
    fields :first_name, :last_name, :name, :email, :phone
  end
end
```

`identifier` is, like its name, the identifier of the JSON object, in this case, is the id of the user record.

`fields` on the other hand are default attributes to be included in the JSON object. So every JSON object should include the records `first_name`, `last_name`, `name` and `email`. Notice how `phone` is left out. That's our choice to include it as default info. ALSO, notice `name`, that isn't an attribute from the Users table?

That is actually a method defined by the user's model class. This means we can include methods defined in our model class that will transform the data in some sort of way.

_models/user.rb_

```ruby
  def name
    "#{first_name} #{last_name}"
  end
```

Let's get back to blueprinter and see an example of how this works. We need to invoke a class method called `render_as_hash` from `UserBlueprint`. This will take a hash, for example, `result.payload[:user]` which will be a hash of the user info such as

```ruby
  {
    id: 1,
    first_name: "John",
    .
    .
    .
  }
```

This will serialize our data depending what the default view when we execute the line below

```ruby
UserBlueprint.render_as_hash(result.payload[:user])
```

Because this is the default 'view', this will return:

```json
{
            "id": 1,
            "email": "test@test.com",
            "first_name": "John",
            "last_name": "Doe",
            "name": "John Doe"
},
```

Remember, the default view includes attributes `first_name`, `last_name`, `name` and `email`. Don't forget about the identifier which is the `id` of the record.

Let's say that we want to include the token of the user in the JSON object. We can do the following

```ruby
  view :login do
    association :token, blueprint: TokenBlueprint do |user, _options|
      user.tokens.last
    end
  end
```

We would then need to include an additional argument to serialize the data such as

```ruby
UserBlueprint.render_as_hash(result.payload[:user], view: :login)
```

This will return the following:

```JSON
{
            "id": 1,
            "email": "test@test.com",
            "first_name": "John",
            "last_name": "Doe",
            "name": "John Doe",
            "token": {
                "id": 8,
                "created_at": "2022-04-13T23:40:55.866Z",
                "expiry": "2022-04-20T23:40:55.859Z",
                "ip": null,
                "revocation_date": null,
                "updated_at": "2022-04-13T23:40:55.866Z",
                "user_id": 1,
                "value": "40910ff7846064fcd91db36f3da6ed23a13e0585"
            }
  },
```

### Logout Action

<img src="https://media.istockphoto.com/photos/logout-button-picture-id177335293" width="200px">

```ruby
      def logout
        result = BaseApi::Auth.logout(@current_user, @token)
        render_error(errors: 'There was a problem logging out', status: :unprocessable_entity) and return unless result.success?

        render_success(payload: 'You have been logged out')
      end
```

```ruby
result = BaseApi::Auth.logout(@current_user, @token)
```

The logic to logout the user comes from the define method `logout` from the `BaseApi::Auth` module. This module comes from `services/base_api/auth.rb`. This method takes in two arguments: `@current_user` and `@token`. Where are these variables being defined? Don't forget, the authenticate method executes before the logout action and this is where `@current_user` and `@token` are being defined.

_controllers/api/v1/application_controller_

```ruby
  def authenticate
    authenticate_token || render_unauthorized
  end

  def authenticate_token
    @ip = request.remote_ip || "unknown"
    authenticate_with_http_token do |token, _options|

      @token = Token.find_by(value: token)
      if @token.nil?
        render_unauthorized
      else
        if @token.expiry.after?(DateTime.now) && @token.revocation_date.blank?
          @current_user = @token.user
          @current_user
        else
          render_unauthorized
        end
      end
    end
  end
```

Let's get back to the `logout` method.

```ruby
      def logout
        result = BaseApi::Auth.logout(@current_user, @token)
        render_error(errors: 'There was a problem logging out', status: :unprocessable_entity) and return unless result.success?

        render_success(payload: 'You have been logged out')
      end
```

If the `result` is unsuccessful, we can call `render_error` and return. Otherwise, we give a successful response.

### Create Action

The `create` action, as you guess it, is dealing with the logic that creates a user record if valid.

```ruby
      def create
        result = BaseApi::Users.new_user(params)
        render_error(errors: 'There was a problem creating a new user', status: 400) and return unless result.success?
        payload = {
          user: UserBlueprint.render_as_hash(result.payload, view: :normal)
        }
        #  TODO: Invite user to accept invitation via registered email
        render_success(payload: payload)
      end
```

```ruby
BaseApi::Users.new_user(params)
```

The `new_user` method is define in the `BaseApi::Users` module from `services/base_api/users.rb`. The rest of logic follows the same pattern as the previous actions we've gone through. "If we run into an error, call `render_error` and return otherwise call `render_success`.

### Me Action

```ruby
      def me
        render_success(payload: UserBlueprint.render_as_hash(@current_user, view: :normal))
      end
```

The `me` method returns `current_user` info. Remember, the user has to be authenticated first before being able to request this information.

```ruby
skip_before_action :authenticate, only: %i[login create]
```

### Validate Invitation Action

We won't worry about `validate_invitation` but it's nice to know what it's purpose is and how it works.

```ruby
      def validate_invitation
        user = User.invite_token_is(params[:invitation_token]).invite_not_expired.first

        render_success(payload: { validated: false }) and return if user.nil?
        render_success(payload: { validated: true })
      end
```

When a user is sent an invitation email, the user will be able to send a request back with the `invitation_token` that is handled by the `validate_invitation` action.

```ruby
User.invite_token_is(params[:invitation_token])
```

`invite_token_is` is a scope method from the `User` model, that performs a custom query in finding the user who holds this `invitation_token`

_models/user.rb_

```ruby
scope :invite_token_is, ->(invitation_token) { where(invitation_token: invitation_token) }
```

```ruby
User.invite_token_is(params[:invitation_token]).invite_not_expired
```

When `invite_token_is` returns this specific user, `invite_not_expired` is called upon that user. `invite_not_expired` will check to see if that token is expired. If not, this method will return an array with this user, hence why `first` is called at the end.

```ruby
        user = User.invite_token_is(params[:invitation_token]).invite_not_expired.first
```

---

---

## Services

### Fat Model Thin Controller Demonstration

"Fat Model Thin Controller" is a pattern for when actions aren't compact with too much logic and instead are extracted into the model. Here's an example. I went ahead and refactored the `login` action from `controllers/user_controller.rb` to demonstrate this concept.

```ruby
      def login
        result = nil
        user = User.find_by(email: params[:email]).try(:authenticate, params[:password])
        result = OpenStruct.new({ success?: false, payload: nil, errors: convert_to_custom_error('User not found') }) if user.nil?
         result = OpenStruct.new({ success?: false, payload: nil, errors: convert_to_custom_error('Incorrect password') }) unless user && result
        token = user.generate_token!(@ip)
        result = OpenStruct.new({ success?: true, payload: { user: user, token: token }, errors: convert_to_custom_error(nil) }) if result == nil
        render_error(errors: 'User not authenticated', status: 401) and return unless result.success?
        payload = {
          user: UserBlueprint.render_as_hash(result.payload[:user], view: :login),
          token: TokenBlueprint.render_as_hash(result.payload[:token])
        }
        render_success(payload: payload)
      end
```

Notice how difficult this is to read. It's hard to manage and figure out what exactly is going on and what is dealing with the `login` logic. This is referred to as a `fat` controller action. There will be use cases where a controller method can be as big as 20 lines of code and there's not a way for it to extract it and that is fine. This is just a commonly used pattern for readability purposes. Let's go ahead and extract this logic into a model to confirm to the `fat model thin controller` pattern.

```ruby
      def login
        result = User.login(params[:email], params[:password], @ip)
        render_error(errors: 'User not authenticated', status: 401) and return unless result.success?

        payload = {
          user: UserBlueprint.render_as_hash(result.payload[:user], view: :login),
          token: TokenBlueprint.render_as_hash(result.payload[:token])
        }
        render_success(payload: payload)
      end
```

That's a lot better. This is much more easier to read. But something's not right.

```ruby
result = User.login(params[:email], params[:password], @ip)
```

We have the User model handling the logic to the login but models shouldn't deal with the requests, rather, models are only associated with business logic (interacting with the database). We can instead direct our attention to services.

<img src="https://yourdiamondteacher.com/wp-content/uploads/2017/03/BUT-WAIT-THERES-MORE.png" >

#### Plain Old Ruby Objects

This is where the concept "Plain Old Ruby Objects" in services come into play. Where we extract this logic into a service instead of a model. A service is just a module or class that encapsulates the logic and makes services lean and readable. Instead of including the login logic in a model, let's extract it in a service. The name of the service or module will be `BaseApi::Auth`.

```ruby
        result = BaseApi::Auth.login(params[:email], params[:password], @ip)
```

Why is it called "Plain Old Ruby Objects"?

"A service object in Rails is a plain old Ruby object created for a specific business action. It usually contains code that doesn't fit in the model or view layer, e.g., actions via a third-party API like posting a tweet." We don't see this happening but behind the scenes of `BaseApi::Auth.login(params[:email], params[:password], @ip)`, this is returning an object.

If the method `login` deems to be a successful result, then the object should include two attributes such as:

-   An attribute called `success?` that is set to `true`. This let's us know whether or not the logic was deemed successful.
-   An attribute called `payload` that is set to some data, e.g, user information.

All in all, you get something like this:

```ruby
{
  success?: true,
  payload: 'some-data'
}
```

If the method `login` deems to be an error response, then the object should include two attributes such as:

-   An attribute called `success?` that is set to `false`.
-   An attribute called `error`.

The makeup of the object will look like the following:

```ruby
{
  success?: false,
  error: 'some-error'
}
```

How are these objects being created? We first have to start off with the `ServiceContract` module.

## Services

### Service Contract

Navigate to `services/service_contract.rb`. This is the `ServiceContract` module.

```ruby
# frozen_string_literal: true

# Standardizes what a service method should always return
module ServiceContract
  # Create the contractual return object
  def self.sign(success:, payload:, errors:)
    OpenStruct.new({ success?: success, payload: payload, errors: convert_to_custom_error(errors) })
  end

  def self.success(payload)
    OpenStruct.new({ success?: true, payload: payload, errors: convert_to_custom_error(nil) })
  end

  def self.error(errors)
    OpenStruct.new({ success?: false, payload: nil, errors: convert_to_custom_error(errors) })
  end

  # Convert a string, an array of strings, or a model's errors to a CustomError instance
  def self.convert_to_custom_error(errors)
    case errors.class.name.to_sym
    when :String, :NilClass
      custom_error = CustomError.new(errors)
    when :Array
      custom_error = CustomError.new
      errors.each { |e| custom_error.add(e) }
    else
      custom_error = CustomError.new.convert(errors)
    end
    custom_error
  end
end
```

This module provides methods that "standardizes" or adheres to the PORO pattern. We will be using these methods throughout our services. Let's start with the `sign` method.

### Sign Method

```ruby
  def self.sign(success:, payload:, errors:)
    OpenStruct.new({ success?: success, payload: payload, errors: convert_to_custom_error(errors) })
  end
```

The `sign` method defines three keyword parameters `success`, `payload` and `errors`. Notice how they are being included in a hash.

```ruby
{ success?: success, payload: payload, errors: convert_to_custom_error(errors) }
```

It's definitely a customizable hash that includes not only the payload but also the errors.

There's two questions that pop up. What is `convert_to_custom_error`? And what is `OpenStruct`?

### OpenStruct

Let's talk about `OpenStruct`. `OpenStruct` is a class that turns a hash into an object. In an OpenStruct object, you are free to add attributes. Here's an example.

```ruby
  user = OpenStruct.new({username: "johndoe123"})
  # returns an instance of OpenStruct with the attribute username.
  user.username = "amywinehouse123"
  puts user.username # prints amywinehouse123
  user.age = 5
  puts user.age # 5
```

### Struct vs OpenStruct vs Hash

Structs define classes as though they are templates with pre-defined attributes.

```ruby
  User = Struct.new(:name, :age)
  User.new("Jimmy", 34)
```

OpenStructs are different because although they are pre-define attributes, you can add more attributes such as

```ruby
  user = OpenStruct.new({username: "johndoe123"})
  user.age = 5
```

OpenStruct is a lot more flexible than hashes and structs. There may be cases where we do want to include attributes to the object.

### Convert To Custom Error Method

So we now know what `OpenStruct` is, let's go ahead and go back to our two parter and go over `convert_to_custom_error`.

```ruby
  def self.sign(success:, payload:, errors:)
    OpenStruct.new({ success?: success, payload: payload, errors: convert_to_custom_error(errors) })
  end
```

```ruby
  # Convert a string, an array of strings, or a model's errors to a CustomError instance
  def self.convert_to_custom_error(errors)
    case errors.class.name.to_sym
    when :String, :NilClass
      custom_error = CustomError.new(errors)
    when :Array
      custom_error = CustomError.new
      errors.each { |e| custom_error.add(e) }
    else
      custom_error = CustomError.new.convert(errors)
    end
    custom_error
  end
```

`convert_to_custom_error` uses a `case/when` block to structure an error depending what the class of the error is. Is it a string? A nil class class? Or an array of errors? Here, `CustomError` is being used. In `services/custom_error.rb`, is where this class exists and how it converts error messages.

```ruby
# frozen_string_literal: true

# Helper class for handling error messages
#
# Methods: add(message), size, none?, all, as_sentence, convert
class CustomError
  def initialize(message = nil)
    @errors = []
    @errors << message unless message.blank?
  end

  def add(message)
    raise_if_no_message_provided(message)
    @errors << message
    self
  end

  def size
    @errors.size
  end

  def none?
    size.zero?
  end

  def all
    @errors
  end

  def as_sentence
    @errors.to_sentence.capitalize
  end

  def convert(errors)
    class_type = errors.class.to_s
    messages = []
    # Convert to a messages array based on the type passed in
    # If it's an active model's errors object
    messages = errors.full_messages if class_type == 'ActiveModel::Errors'
    # If it's an array
    messages = errors if class_type == 'Array'
    # If it's any active model object
    messages = errors&.errors&.full_messages || [] unless class_type.in?(%w[Array ActiveModel::Errors])

    # Loop over the messages, adding them to the @errors array
    messages.each { |error| @errors << error }
    self
  end

  private

  def raise_if_no_message_provided(message)
    raise 'Must provide usable error message!' if message.blank?
  end
end
```

### Success Method

Remember, to adhere to the PORO pattern, we must create a representation of a success object. That is what the `success` method provides.

```ruby
  def self.success(payload)
    OpenStruct.new({ success?: true, payload: payload, errors: convert_to_custom_error(nil) })
  end
```

### Error method

Same with an error representation.

```ruby
  def self.error(errors)
    OpenStruct.new({ success?: false, payload: nil, errors: convert_to_custom_error(errors) })
  end
```

## Users Service

<img src = "https://media.istockphoto.com/vectors/vector-comic-cartoon-of-tired-or-overworked-businessman-or-man-or-vector-id1205473265" width = "200px">

Okay that was a lot of jumping around. From "fat models thin controllers" to custom error messages and service contracts to setup PORO. Let's go ahead and go over each service file, starting with `services/base_api/users.rb`

```ruby
# frozen_string_literal: true

module BaseApi
  module Users
    def self.new_user(params)
      user = User.new(
        first_name: params[:first_name],
        last_name: params[:last_name],
        email: params[:email],
        phone: params[:phone],
        password: params[:password],
        password_confirmation: params[:password_confirmation]
      )
      user.save!
      return ServiceContract.error('Error saving user.') unless user.valid?

      ServiceContract.success(user)
    end

    def self.destroy_user(user_id)
      user = User.find(user_id)
      return ServiceContract.error('Error deleting user') unless user.destroy

      ServiceContract.success(payload: user)
    end
  end
end
```

As you can see, the file consist of a module called `BaseApi` follow by a nested module called `Users`. Within the `Users` module, there are two methods that are extracting the logic from controller actions: `new_user` and `destroy_user`.

```ruby
    def self.new_user(params)
      user = User.new(
        first_name: params[:first_name],
        last_name: params[:last_name],
        email: params[:email],
        phone: params[:phone],
        password: params[:password],
        password_confirmation: params[:password_confirmation]
      )
      user.save!
      return ServiceContract.error('Error saving user.') unless user.valid?

      ServiceContract.success(user)
    end
```

The `new_user` method will try to create a User record from params. Depending on whether it be successful or not, an object will be returned to represent the outcome (PORO). Same with `destroy_user`.

```ruby
    def self.destroy_user(user_id)
      user = User.find(user_id)
      return ServiceContract.error('Error deleting user') unless user.destroy

      ServiceContract.success(payload: user)
    end
```

## Roles Service

Let's navigate to `services/base_api/roles.rb`.

```ruby
# frozen_string_literal: true

module BaseApi
  # Container for methods related to handling roles on users
  module Roles
    # Handles determining if a user has a given role
    def role?(role)
      roles.any? { |r| r.slug.underscore.to_sym == role }
    end

    # Handles adding a role to a user
    def add_role(role)
      return ServiceContract.error('Role must be a symbol') if role.class.name.to_sym != :Symbol

      return ServiceContract.error("Role type '#{role}' is not available.") unless Role.valid_role?(role)

      target_role = Role.find_by_slug(role)
      roles << target_role unless roles.include?(target_role)
      ServiceContract.success(roles)
    end

    # Handles removing a role from a user
    def remove_role(role)
      return ServiceContract.error('Role must be a symbol') if role.class.name.to_sym != :Symbol

      return ServiceContract.error("Role type '#{role}' is not available.") unless Role.valid_role?(role)

      role = Role.find_by_slug(role)
      if user_roles.where(role: role).destroy_all
        ServiceContract.success(nil)
      else
        ServiceContract.error("Could not destroy #{role}")
      end
    end
  end
end
```

The Roles service isn't being used at the moment. But that doesn't mean we can't use it's methods to our benefit. In order to implement this service, we must first include it in our User model.

```ruby
class User < ApplicationRecord
  include BaseApi::Roles
```

Now each user has access to these defined methods. Let's go through them.

```ruby
    def role?(role)
      roles.any? { |r| r.slug.underscore.to_sym == role }
    end
```

The `role` returns true or false depending on whether the user already has that specific role. Where is `roles` being defined? Because this method is included in the user model, it has access to the models methods like `roles`, `tokens`, ect.

```ruby
    # Handles adding a role to a user
    def add_role(role)
      return ServiceContract.error('Role must be a symbol') if role.class.name.to_sym != :Symbol

      return ServiceContract.error("Role type '#{role}' is not available.") unless Role.valid_role?(role)

      target_role = Role.find_by_slug(role)
      roles << target_role unless roles.include?(target_role)
      ServiceContract.success(roles)
    end
```

Notice how `ServiceContract` is being called here, this allows us to follow the PORO pattern and we are expecting either an error or successful outcome from the `add_role` method.

So the first condition checks to see if `role` is a symbol and if not, return an object as a failed outcome.

The next condition will go ahead and check to see if the user already has that role using the `valid_role?` method from the `Role` model class. Here is that code snippet below to remind you what `valid_role?` does. It downcases the parameter and then checks to see if there is a role with its same exact value.

_models/role.rb_

```ruby
  def self.valid_role?(role)
    stringified_role = role.to_s.downcase.underscore
    stringified_role.in?(available_roles)
  end
```

Back to `add_role` in `services/base_api/roles.rb` . We make our way to add the Role to the user once we check to see if the role actually exists. If so we can go ahead and add that role onto the user.

```ruby
      target_role = Role.find_by_slug(role)
      roles << target_role unless roles.include?(target_role)
      ServiceContract.success(roles)
```

## Rswag 

RSwag is a gem that provides tooling for documenting and testing APIs built with Ruby on Rails. It allows developers to generate Swagger documentation for their API endpoints, which can be used to automatically generate API client libraries and interactive API documentation.

To generate the API docs in Rswag run the following 

```
rails rswag
```

Run the server and then go to `/api-docs` to see documentation of the api.

### Wrap up

There are several files we haven't fully explored but I urge you to go through the files yourselves and break it down sort of like how we did it. Use the descriptive methods and variables to your advantage of what is what.

## _Additional Resources_

### Documentation

-   [Rails as an api](https://guides.rubyonrails.org/api_app.html)
-   -   [Sidekiq web ui](https://github.com/mperham/sidekiq/wiki/Monitoring#web-ui)
-   [Introducing json](https://www.json.org/json-en.html)
-   [ActionController:HTTPAuthentication::Token::ControllersMethod](https://api.rubyonrails.org/v6.1.0/classes/ActionController/HttpAuthentication/Token/ControllerMethods.html)
-   [WWW-Authenticate](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/WWW-Authenticate)
-   [ActionController::HttpAuthentication::Token](https://api.rubyonrails.org/classes/ActionController/HttpAuthentication/Token.html)
-   [Blueprinter github](https://github.com/procore/blueprinter)

### Videos

-   [Sidekiq and Redis](https://www.youtube.com/watch?v=aaGSh38nzq8&ab_channel=GoRails)
-   [What is an API?](https://www.youtube.com/watch?v=s7wmiS2mSXY&ab_channel=MuleSoftVideos)
-   [The Complete Guide to Ruby on Rails Encrypted Credentials](https://www.youtube.com/watch?v=c1sQVXU5PBM&ab_channel=Web-Crunch)
-   [What is an API? (Application Programming Interface)](https://www.mulesoft.com/resources/api/what-is-an-api)
    [Basic Authentication in Five Minutes](https://www.youtube.com/watch?v=rhi1eIjSbvk&ab_channel=OktaDev)

### Articles

-   [Rails encrypted credentials on 6.2](https://www.engineyard.com/blog/rails-encrypted-credentials-on-6-2/)
-   [Encrypted Credentials in Ruby on Rails](https://medium.com/craft-academy/encrypted-credentials-in-ruby-on-rails-9db1f36d8570)
-   [Evolution of Encrypted Credentials in Rails 6.2](https://faun.pub/evolution-of-encrypted-credentials-in-rails-6-2-666ff5884628)
-   [What are indexes and how to add them to your rails app](https://medium.com/@mera.stackhouse/what-are-indexes-and-how-to-add-them-to-your-rails-app-dc066d538771)
-   [How to Use Scopes in Ruby on Rails](https://www.rubyguides.com/2019/10/scopes-in-ruby-on-rails/)
-   [Creating a Simple Rest Api with Rails](https://medium.com/@SJTGs/creating-a-simple-rest-api-with-rails-2e913acfc46)
-   [Building a RESTful API in a Rails Application]()
-   [How to add Basic HTTP Authentication to Sidekiq UI mounted on a Rails application](https://www.aloucaslabs.com/miniposts/how-to-add-basic-http-authentication-to-sidekiq-ui-mounted-on-a-rails-application)
-   [Scope vs namespaces in Rails 5](https://devblast.com/b/rails-5-routes-scope-vs-namespace)
-   [Versioning a Rails API](https://chriskottom.com/blog/2017/04/versioning-a-rails-api/)
-   [Token Based Authentication in Rails](https://www.pluralsight.com/blog/tutorials/token-based-authentication-rails)
-   [Authentication vs Authorization](https://medium.datadriveninvestor.com/authentication-vs-authorization-716fea914d55)
-   [Rails Logger and Rails Logging Best Practices](https://stackify.com/rails-logger-and-rails-logging-best-practices/)
-   [HTTP headers | WWW-Authenticate](https://www.geeksforgeeks.org/http-headers-www-authenticate/)
-   [500 Internal Server Error](https://www.lifewire.com/500-internal-server-error-explained-2622938#:~:text=The%20500%20Internal%20Server%20Error,what%20the%20exact%20problem%20is.)
-   [Serializing Data in Rails](https://medium.com/@stvik2/serializing-data-in-rails-a46cb16e0c2d#:~:text=What%20is%20serialization%3F,front%20end%20can%20read%20it.)

---

### Other Resources

-   [Episode 100 - Basic Testing Introduction in Rails](https://www.youtube.com/watch?v=jQvB0QWe5Bs&ab_channel=DriftingRuby)
-   [RSpec TDD - How To Unit Test Ruby On Rails 6 Apps For Absolute Beginners | 20in20 - Week 14](https://www.youtube.com/watch?v=AAqPc0j_2bg&t=20s&ab_channel=Deanin)
-   [Client and Server side application](https://learn.co/lessons/dsc-2-15-04-clients-and-servers)


## Exercises 

Here is the [remote repository](https://github.com/leehodges/CodeLabsApi) 

Use postman to test your endpoints.

**Exercise 1** Add an endpoint that will allow a user to update their information. 

**Exercise 2** 

Add the following roles "admin", "teacher" and "student" in the rails console or the seed file. 

Make sure there are at least 3 users, an admin, a teacher and a student. 

Keep track of how many courses a student can have and how many a teacher can host. 

A course can have many students and there can only be one teacher. 

**Exercise 3** 

Create an endpoint that will allow a teacher and student to fetch his or her courses. 

**Exercise 4** 

Create endpoints that will allow an admin to create, update, and delete a course. 

Teachers and students should not be able to do this, if so, send an unauthorized response.

**Exercise 5** 

Create an endpoint that will allow students to enroll in a course. A student cannot enroll in a course more than once. A teacher and admin cannot enroll in a course.

**Exercise 6** 

Create an endpoint that will allow admin and teachers to view a list of students by course. Students are not allowed.

**Exercise 7**

Allow admins to delete user accounts. 



