# Authentication 

## Incorporating authentication to a rails app

Authentication in Ruby on Rails refers to the process of verifying the identity of a user by checking their credentials, such as username and password. It is used to determine if a user is who they claim to be and to grant or restrict access to certain parts of an application based on the user's role or permissions. Rails provides a variety of authentication solutions through gems and built-in methods, including Devise, Sorcery, and Authlogic.

**Using BCrypt for authentication**
Yes, bcrypt is a popular encryption library used for password hashing in Ruby on Rails. It is designed to be slow and computationally expensive, which makes it resistant to brute-force attacks and other types of password cracking. When a user creates an account or changes their password, the password is hashed using bcrypt and the hash is stored in the database. When the user logs in, the entered password is hashed and compared to the stored hash to verify the user's identity.


## Adding Users

```
rails g migration CreateUsers email:string password_digest:string
```

- Install BCrypt 
**gemfile**
```ruby 
gem 'bcrypt'
```

- Add has_secure_password
**models/user.rb**
```ruby
class User < ApplicationRecord
  validates :email, :password_digest, presence: true 
  has_secure_password
end
```

## Adding Associations to Users

```
rails g migration AddForeignKeyToBookAndReview
```

```
class AddForeignKeyToBookAndReview < ActiveRecord::Migration[7.0]
  def change
    add_column :books, :user_id, :integer
    add_column :reviews, :user_id, :integer
  end
end
```

```ruby
class Review < ApplicationRecord
  belongs_to :book
  belongs_to :user
end
```

```ruby
class Book < ApplicationRecord
  has_and_belongs_to_many :categories 
  has_many :reviews, dependent: :destroy
  belongs_to :user
end
```

```ruby
class User < ApplicationRecord
  validates :email, :password_digest, presence: true 
  has_many :books 
  has_many :reviews, through: :books 
end
```

## Sign Up 

**routes.rb**
```
  get '/sign-up', to: 'users#new'
  post '/users', to: 'users#create'
```

**users_controller.rb**

```ruby
class UsersController < ApplicationController 
  before_action :set_user, only: %i[ show edit update destroy ]
  def new 
    @user = User.new
  end

  def create 
    @user = User.new(user_params)
    if @user.save 
      flash[:notice] = "You have signed up successfully."
      redirect_to root_path
    else 
      flash[:notice] = "There was a problem signing you up."
      render :new 
    end
  end

  def show  
  end

  private
  
  def user_params
    params.require(:user).permit(:email, :password)
  end

  def set_user 
    @user = User.find(params[:id])
  end
end
```

***shared/_nav.html.erb**
```html
<ul>
  <li><%= link_to "Home", root_path%></li>
  <li><%= link_to "List of Books", books_path%></li>
  <li><%= link_to "Categories", categories_path%></li>
  <li><%= link_to "Sign Up", sign_up_path%></li>
</ul>
```

**users/new.html.erb**
```html
<%= form_with(model: @user) do |form| %>
  <div>
    <%= form.label :email %>
    <%= form.text_field :email%>
  </div>
    <div>
    <%= form.label :password %>
    <%= form.password_field :password%>
  </div>
  <div>
    <%= form.submit "Sign Up"%>
  </div>
<% end %>
```

### Login 
**routes.rb**
```ruby
  get '/login', to: 'sessions#new'
  post '/login', to: 'sessions#create'
```

**_nav.html.erb**
```html
  <li><%= link_to "Sign Up", sign_up_path%></li>
  <li><%= link_to "Login", login_path%></li>
</ul>
```

**sessions_controller.rb**
```rb
class SessionsController < ApplicationController
  def new
  end

  def create 
    @user = User.find_by(email: params[:email])

    if @user && @user.authenticate(params[:password])
      session[:user_id] = @user.id
      redirect_to root_path, notice: "Logged in!"
    else 
      render :new, notice: "Invalid email or password"
    end
  end
end
```

**new.html.erb**
```html
<%= form_with(model: @user) do |form| %>
  <div>
    <%= form.label :email %>
    <%= form.text_field :email%>
  </div>
    <div>
    <%= form.label :password %>
    <%= form.text_field :password%>
  </div>
  <div>
    <%= form.submit "Sign Up"%>
  </div>
<% end %>
```

### Adjusting UI 

**application_helper.rb**
```rb
module ApplicationHelper
  def current_user 
    @current_user ||= User.find(session[:user_id]) if session[:user_id]
  end

  def logged_in?
    !!current_user
  end
end
```

**_nav.html.erb**
```html
<ul>
  <li><%= link_to "Home", root_path %></li>
  <% if logged_in? %>
    <li>Welcome <%= current_user.email %> </li>
    <li><%= link_to "List of Books", books_path %></li>
    <li><%= link_to "Categories", categories_path %></li>
  <% else %>
    <li><%= link_to "Sign Up", sign_up_path %></li>
    <li><%= link_to "Login", login_path %></li>
  <% end %>
</ul>
```

### Logout

**routes.rb**
```ruby
  get '/login', to: 'sessions#new'
  post '/login', to: 'sessions#create'
  delete '/logout', to: 'sessions#destroy'
end
```

**sessions_controller.rb**
```ruby
class SessionsController < ApplicationController
  def new
  end

  def create 
    @user = User.find_by(email: params[:email])
    if @user && @user.authenticate(params[:password])
      session[:user_id] = @user.id
      redirect_to root_path, notice: "Logged in!"
    else 
      render :new, notice: "Invalid email or password"
    end
  end

  def destroy
    session[:user_id] = nil 
    flash[:notice] = "Logged out!"
    redirect_to root_path 
  end
end
```

**_nav.html.erb**
```html
<ul>
  <li><%= link_to "Home", root_path %></li>
  <% if logged_in? %>
    <li>Welcome <%= current_user.email %> </li>
    <li><%= link_to "List of Books", books_path %></li>
    <li><%= link_to "Categories", categories_path %></li>
    <li><%= link_to "Logout", logout_path, data: {'turbo-method': :delete}%></li>
  <% else %>
    <li><%= link_to "Sign Up", sign_up_path %></li>
    <li><%= link_to "Login", login_path %></li>
  <% end %>
</ul>
```

### Allow users to create a book

**books_controller.rb**
```rb
  # POST /books or /books.json
  def create
    @book = helpers.current_user.books.new(book_params)

    respond_to do |format|
      if @book.save
        format.html { redirect_to book_url(@book), notice: "Book was successfully created." }
        format.json { render :show, status: :created, location: @book }
      else
        format.html { render :new, status: :unprocessable_entity }
        format.json { render json: @book.errors, status: :unprocessable_entity }
      end
    end
  end
```

**_book.html.erb**
```html
<div id="<%= dom_id book %>">
  <% if book.user %>
    <div>By: <%= book.user.email%> </div>
  <% end %>
  
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
    <%= image_tag book.image_path  %>
  </p>

</div>
```

## Reviews 

**reviews_controller.rb**
```rb
  def create 
    @book = Book.find(params[:book_id])
    @review = @book.reviews.new(permit_review_params)
    @review.user_id = helpers.current_user.id
    if @review.save 
      redirect_to book_path(@book)
    else 
      render :new, status: :unprocessable_entity
    end
  end
```

**books/show.html.erb**
```html
<% @book.reviews.each do |review| %>
  <div>
    <b><%= review.user.email if review.user%></b>
  </div>
  <div>
    <% (0..review.rating-1).each do |i| %>
      &#9733;
    <% end %>
  </div>
  ```

### Preventing Access for Guests

**application_controller.rb**
```ruby 
class ApplicationController < ActionController::Base
  def redirect_if_guest 
    !helpers.logged_in? ? redirect_to(root_path, notice: "Must login first") : true
  end
end
```

**books_controller.rb**
```ruby
class BooksController < ApplicationController
  before_action :set_book, only: %i[ show edit update destroy ]
  before_action :redirect_if_guest
```

**categories_controller.rb**
```ruby
class CategoriesController < ApplicationController
  before_action :set_category, only: %i[ show edit update destroy ]
  before_action :redirect_if_guest
```

--- 
---

## Project Requirements
You are now ready to start on a brand new journey. Below is listed information required to complete the Full Stack Rails Project. 

- **Project Theme**: Pick a project theme here are some examples 
  - Task Manager
  - Recipe Book 
  - Social Network
  - University App 
  - Etzy clone
  - Job Board
  - Chat Application 
  - Online Educational Platform 
  - Chess

  - Suggestions 
    1. What is this application about?
    2. What types of features belong to this app? What's a reasonable amount of work I can do in a few weeks? 
    3. Design (optional). You are able to use an application like figma to come up with a quick mockup of what your app may look like.
    4. ER Diagram to plan out your DB

### Technical Requirements

- **User authentication**: The project should have a user authentication system that allows users to sign up, log in, and log out. Users should also be able to reset their passwords if they forget them.

- **Database**: The project should use a database to store and retrieve data. The database should have at least three tables. An ER Diagram should be provided.

- **CRUD functionality**: The project should implement CRUD (create, read, update, delete) functionality for at least two of the database tables. This should include the ability to create, read, update, and delete records from the database.

- **Associations**: Associations must be utilized. 

- **RESTful routes**: The project should follow RESTful routes for all CRUD operations. This means that each action should correspond to a specific HTTP verb (GET, POST, PUT, DELETE).

- **Error handling:** The project should handle errors gracefully and provide useful error messages to the user.

- **Security**: The project should follow best practices for security, such as using strong passwords, encrypting sensitive data, and protecting against common vulnerabilities such as SQL injection and cross-site scripting (XSS).

- **Restrictions** - Blogging platform
