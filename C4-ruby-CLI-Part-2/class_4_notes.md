# Ruby - Command Line Interface Project


Let's incorporate a user system to our CLI using BCrypt

Bcrypt is a Ruby gem that provides a simple wrapper for securely hashing passwords using the bcrypt algorithm. The bcrypt algorithm is a password hashing function that is designed to be secure and slow, making it difficult for attackers to use brute-force methods to guess a password. When a user's password is hashed with bcrypt, the resulting hash is unique for that password and cannot be reversed to reveal the original password. The bcrypt gem also includes a function for checking if a given password matches a previously hashed password, making it a useful tool for implementing secure user authentication in Ruby applications.

## Adding BCrpyt to Gemfile

Add bcrypt to gemfile.

```ruby
# frozen_string_literal: true

source "https://rubygems.org"

# Specify your gem's dependencies in oscar_winning_films_cli.gemspec
gemspec

gem "rake", "~> 13.0"

gem 'nokogiri'
gem 'open-uri'

gem 'bcrypt'
gem 'pry'
```

## User Class

Create user.rb under the lib directory.

- require bcrypt at the top so we can hash passwords
- (OPTIONAL) I've included pry to debug the file for any potential mistakes
- Define a user class
  - Define a class variable called users and set that to an empty array
  - Include attributes username, password
  - define initialize and include two parameters username and password
    - set each user attribute to their respective parameters
    - push each newly created user to users
  - Define a class method called all that returns the users array

```ruby
require "bcrypt"
require 'pry'

class User
  @@users = []
  attr_accessor :username, :password
  def initialize(username, password)
    @username = username
    @password = password
    @@users << self
  end

  def self.all
    @@users
  end
end
```

## Hashing passwords

In the user class, let's define a class method called hash_password

- Use BCrypt to hash the password given by the user

```ruby
  def self.hash_password(password)
    BCrypt::Password.create(password)
  end
```

In the initialize method, use hash_password for the given password parameter

```ruby
  def initialize(username, password)
    @username = username
    @password = User.hash_password(password)
    @@users << self
  end
```

## Populate Users 

Define a class method called seed. 
- Declare a users variable and set that to an array of hashes that include properties username and password
- Iterate through users and create a user instance for every hash in the users array

```ruby 
  def self.seed
    users = [
      {
        username: "johndoe123",
        password: "password",
      },
      {
        usernaem: "amy123",
        password: "password",
      },
    ]

    users.each do |user|
      User.new(user[:username], user[:password])
    end
  end
```


## Authenticating Users 
Let's now authenticate a user when 'logging in'. 

- Define a class method called authenticate_user with parameters username and password
  - declare a variable called authenticate_user and set to nil. We will use this as our indicator of whether we found a user match. 
  - Iterate through the users array and then check if a user matches the parameters username and password
    - If a match was found, set authenticate_user to the user that was found. Then call break to stop the loop as it is no longer necessary. 

  - return authenticate_user (two possible outcomes: nil or a user instance)


```ruby 
  def self.authenticate_user(username, password)
    authenticate_user = nil
    @@users.each do |user| 
      if user.username == username && user.password == password 
        authenticate_user = user 
        break;
      end
    end
    authenticate_user
  end
```

Full code below: 

```ruby
require "bcrypt"
require 'pry'
class User
  @@users = []
  attr_accessor :username, :password

  def initialize(username, password)
    @username = username
    @password = User.hash_password(password)
    @@users << self
  end

  def self.authenticate_user(username, password)
    authenticate_user = nil
    @@users.each do |user| 
      if user.username == username && user.password == password 
        authenticate_user = user 
        break;
      end
    end
    authenticate_user
  end

  def self.hash_password(password)
    BCrypt::Password.create(password)
  end

  def self.seed
    users = [
      {
        username: "johndoe123",
        password: "password",
      },
      {
        usernaem: "amy123",
        password: "password",
      },
    ]

    users.each do |user|
      User.new(user[:username], user[:password])
    end
  end
  
  def self.all 
    @@users
  end
end
```

## Adding Authentication setup to CLI 
Navigate to oscar_winning_films_cli.rb, require user.rb at the top. 

```ruby
# frozen_string_literal: true

require_relative "oscar_winning_films_cli/version"
require_relative 'cli.rb'
require_relative 'scraper.rb'
require_relative 'user.rb'
```

Navigate to cli.rb. Call seed and at the very beginning of the run method.
- call signup_or_login method. We will define this. 

```ruby 
  def run
    User.seed
    signup_or_login
    menu
  end
```

In the cli class, define a method called signup_or_login. 

- Declare a variable called user_input that is set to an empty string. We will user this to keep track of the user status in a while loop.
- Call a while loop and include as it's condition to keep loop until user_input is equal to exit. 
  - Within the loop
    - Print "Please enter login or signup"
    - Get user input and set that to user_input 
    - Include an if else statement
      - if user input is login, 
        - call login and break(we will define login soon)
      - otherwise if the user input is signup
        - call signup and break (we will define sign up soon)

```ruby
  def signup_or_login
    user_input = ""
    while user_input != "exit"
      puts "Please enter login or signup"
      user_input = gets.chomp
      if user_input == "login"
        login
        break;
      elsif user_input == "signup"
        signup
        break;
      end
    end
  end
```

Let's define login in the cli class
- Declare a variable called authenticate and set it to false 
- Call a while loop and loop while authenticate is equal to false 
  - Within the loop
    - Print "Please enter your username"
    - Get user input
    - Print "Please enter your password
    - Include a conditional to see if both inputs match any user credentials
      - Call User.authenticate_user to do just this.
      - If successful, set authenticate to true to stop the loop
      - Print "Login successful


```ruby 
  def login
    authenticate = false
    while authenticate == false
      puts "Please enter your username."
      username = gets.chomp
      puts "Please enter your password"
      password = gets.chomp

      if User.authenticate_user(username, password)
        authenticate = true
        puts "Login successful."
      end
    end
  end
```

Let's now define the signup method in the cli class. Signing up involves creating a user instance with the given information the user entered.

- In signup, get user input for both username and password 
- Create a user instance by the information the user entered 
- Then call login to allow the user to login after signing up


```ruby 
  def signup
    puts "Please enter a username"
    username = gets.chomp
    puts "Please enter a password"
    password = gets.chomp
    puts "Sign up successful. Please login."
    User.new(username, password)
    login
  end
```

Here is the full code. 

```ruby 
class CLI
  def run
    User.seed
    signup_or_login
    menu
  end

  def menu
    user_input = ""
    while user_input != "exit"
      puts "Request movies Oscar Award Winning movies by year "
      puts "2015, 2014, 2013, 2012, 2011, 2010"
      puts "Please enter a year"
      user_input = gets.chomp
      break if user_input == 'exit'
      Scraper.scrape_and_print_movies(user_input)
    end
  end

  def signup_or_login
    user_input = ""
    while user_input != "exit"
      puts "Please enter login or signup"
      user_input = gets.chomp
      if user_input == "login"
        login
        break;
      elsif user_input == "signup"
        signup
        break;
      end
    end
  end

  def login
    authenticate = false
    while authenticate == false
      puts "Please enter your username."
      username = gets.chomp
      puts "Please enter your password"
      password = gets.chomp

      if User.authenticate_user(username, password)
        authenticate = true
        puts "Login successful."
      end
    end
  end

  def signup
    puts "Please enter a username"
    username = gets.chomp
    puts "Please enter a password"
    password = gets.chomp
    puts "Sign up successful. Please login."
    User.new(username, password)
    login
  end
end
```
