# Project - Basic CLI starter notes

By learning the basics of Ruby, we will be equipped to build a Command Line Interface (CLI) program that operates in the terminal and prompts the user for input. Our CLI will feature data scraping functionality, giving the user the ability to select the specific information they wish to view. We will begin the project by creating a gem.

<div id="what-is-a-gem"></div>

## What is a Gem?

A ruby [gem](https://rubygems.org/) is simply a library or package that contain Ruby code. You can also think of gems as "tools" to be used. A gem is a contains a collection of Ruby code and other files, such as documentation or test files. Gems can be used to extend the functionality of a Ruby application or to add features to the Ruby language itself. They can be easily installed, updated, and managed using the RubyGems package manager. Gems can include anything from simple command line utilities to complex web frameworks.Here is a list of the most popular gems:

- With over 800 million downloads, [Bundler](https://rubygems.org/gems/bundler) tracks and manages all gem versions that are needed. Bundler is also used to create gems.
- [Minitest](https://rubygems.org/gems/minitest) provides a testing suit for your project applications
- By using [Nokogiri](https://rubygems.org/gems/nokogiri), you are easily able to scrape data from websites.

<div id="creating-a-gem"></div>

## Creating a Gem

In this lesson, we will create our own Ruby Gem. While we will not be publishing it in this curriculum, the process will give you a clear understanding of how to create open-source projects for other developers to use.

You can create the project in any Ruby development environment. We will be using Replit or a local IDE for this purpose. To create a Gem, we must use the Bundler Gem. To check if you have Bundler already installed, you can run the following command in your command line:

```
bundler -v
```

In case you do not have Bundler installed, enter `gem install bundler`.

Let's go ahead and generate a Gem from scratch by entering the following in the command line:

`bundle gem oscars_winning_films_cli`<br>

<div id="gem-setup">

## Gem setup

You might then get a series of questions.

1. `Do you want to generate tests with your gem?` no <br>
   We are not concern with testing our application at this moment of time. Of course, in future project we will welcome them.

2. `Do you want to license your code permissively under the MIT license?` yes <br>
   By including an MIT license, you are allowing any developer to use the gem however they like as long as they give you credit. On another note, this furthers [open source development](https://blog.jcoglan.com/2010/08/15/what-i-mean-when-i-use-the-mit-license/).

```
Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated
documentation files (the “Software”), to deal in the Software without restriction, including without
limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the
Software, and to permit persons to whom the Software is furnished to do so, subject to the following
conditions...
```

3. `Do you want to include a code of conduct in gems you generate?` yes <br>

<div id="folder-structure"></div>

## Folder Structure

After these series of questions, bundler will create a project folder with numerous of sub folders and files.

```
oscar_winning_films_cli
    bin
    lib
    .gitignore
    CODE_OF_CONDUCT.md
    oscar_winning_films_cli.gemspec
    gemfile
    gemfile.lock
    license.txt
    Rakefile
    README.md
```

Before explaining each folder and file, let's navigate to `oscar_winning_films_cli.gemspec`. Let's go ahead and make some adjustments. Please see the block below. We aren't concerned, at this moment of time, with the details of gem.

```ruby
spec.authors = [""]
spec.email = [""]

spec.summary = "" # SET TO EMPTY STRING
spec.description = "" # SET TO EMPTY STRING
spec.homepage = "" # SET TO EMPTY STRING
spec.license = "MIT"
spec.required_ruby_version = ">= 2.6.0"

spec.metadata["allowed_push_host"] = "" # SET TO EMPTY STRING

# comment out these lines of code
# spec.metadata["homepage_uri"] = spec.homepage
# spec.metadata["source_code_uri"] = ""
# spec.metadata["changelog_uri"] = ""
```

### Bin Folder

Back to the folder structure. The bin folder contains two files: console and setup. Console is used for `experimentation`. Here you can test out specific features/code/issues. By executing this file, it will automatically start IRB. We can include variables, logic in our existing code to test the features.

```ruby
#!/usr/bin/env ruby
# frozen_string_literal: true

require "bundler/setup"
require "oscar_winning_films_cli"

# You can add fixtures and/or initialization code here to make experimenting
# with your gem easier. You can also use a different console, if you like.

# (If you use this, don't forget to add pry to your Gemfile!)
# require "pry"
# Pry.start

require "irb"
IRB.start(__FILE__)
```

The setup file allows us to automate any other setup.

### Bin Folder

Mostly all of our file creation will happen in the bin folder.

### .gitignore

Files that are left untracked or "ignored" when committing code to GitHub.

### gemfile

The gemfile is a list of gems that are necessary to execute the program. Soon, we will be adding more gems.

<div id="getting-started"></div>

## Getting Started

In the terminal, let's <em>**change directory**</em> or cd into the project folder if you haven't already. To check the available files and folders that exist in the current directory you are in, enter `ls`. Create a file called <em>**tracker**</em> inside of the bin folder. Tracker will be our main executable file and act as our start place.

## CLI class

Create a file called cli.rb in lib.

Define a class and a run method.

```ruby
class CLI
  def run
    puts "Greetings"
  end
end
```

Navigate to oscar_winning_films_cli.rb and use require_relative to execute the cli.rb file.

NOTE: you might get an issue with

```ruby
require "oscar_winning_films_cli/version"
```

change that to the follow:

```ruby
# frozen_string_literal: true
require_relative "oscar_winning_films_cli/version"
require_relative 'cli.rb'
```

Navigate to tracker and add the following code

```ruby
require './lib/oscar_winning_films_cli.rb'
CLI.new.run
```

## Scraper class

Create scraper.rb in lib and define the Scraper class. Add a class method called scrape_movies

add nokogiri and open-uri to your gemfile. You may need to also add pry in case for debugging.

```ruby
# frozen_string_literal: true

source "https://rubygems.org"

# Specify your gem's dependencies in oscar_winning_films_cli.gemspec
gemspec

gem "rake", "~> 13.0"

gem 'nokogiri'
gem 'open-uri'
```

Run bundle install in the terminal.

Require both nokogiri and open-uri at the top of scraper.rb.

```ruby
require "open-uri"
require "nokogiri"

class Scraper
  def self.scrape_and_print_movies
    puts "Fetching movies..."

  end
end
```

## Scraping Data

Navigate to scraper.rb.

The website we will be scraping data from will be https://www.scrapethissite.com/pages/ajax-javascript. Because this does not give us data information, we actually use the ajax request url instead of what you see in the browser url as they are interpreted differently.

Define a class property and set that to this link.

![where to find the ajax request url](../assets/oscar_winning_movies.png).

```ruby
class Scraper
  # https://www.scrapethissite.com/pages/ajax-javascript to scrape
  # AJAX request
  URL = "https://www.scrapethissite.com/pages/ajax-javascript/?ajax=true&year="
```

In scrape_and_print_movies, use nokogiri and open.uri to parse the incoming file from the server.

```ruby
require 'nokogiri'
require 'open-uri'
# Parse payload to hash
require 'json'
  def self.scrape_and_print_movies(year)
    puts "Fetching movies..."
    # use URL and the user input which will be year to grab the payload of the response
    # To parse the payload, be sure to use nokogiri to parse this into url. We can use text to receive the json object. Use JSON.parse to do just this by passing in doc.text as an argument
    doc = Nokogiri::HTML(URI.open("#{URL}#{year}"))
    scraped_movies = JSON.parse(doc.text)
  end
```

Iterate through each movie and print.

```ruby
  def self.scrape_articles
    puts "Fetching movies..."
    doc = Nokogiri::HTML(URI.open("#{URL}#{year}"))
    scraped_movies = JSON.parse(doc.text)

  # print each movie
    scraped_movies.each do |movie|
      puts "| #{movie["title"]} | #{movie["year"]} | #{movie["nominations"]} | #{movie["best_picture"]}"
    end
  end
```

Adjust oscar_winning_films_cli.rb by adding require_relative to scraper.rb.

```ruby
# frozen_string_literal: true

require_relative "oscar_winning_films_cli/version"
require_relative 'cli.rb'
require_relative 'scraper.rb'

module JavascriptArticlesCli
  class Error < StandardError; end
  # Your code goes here...
end
```

### Creating the menu

Let's create the cli menu. Navigate to cli.rb.

Define a method called menu.

While user input is not exit, keep executing the code block. This will ensure the user wants to keep interacting with the code block.

```ruby
  def menu
    user_input = ""

    while user_input != "exit"

    end
  end
```

Call print_articles from the Article class. Then ask the user to enter a number of the article they like to read.

```ruby

    while user_input != "exit"
      puts "Request movies Oscar Award Winning movies by year "
      puts "2015, 2014, 2013, 2012, 2011, 2010"
      puts "Please enter a year"
      # get user input
      user_input = gets.chomp
      # exit if user input is exit
      break if user_input == 'exit'
      # print movies requested by user 
      Scraper.scrape_and_print_movies(user_input)
    end

```

Add menu to run method 

```ruby
  def run
    puts "Greetings"
    menu 
  end
```

In the terminal run ruby bin/tracker.

```
Greetings
Request movies Oscar Award Winning movies by year 
2015, 2014, 2013, 2012, 2011, 2010
Please enter a year
2015
Fetching movies...
| Spotlight   | 2015 | 6 | true
| Mad Max: Fury Road  | 2015 | 10 | 
| The Revenant    | 2015 | 12 | 
| Bridge of Spies | 2015 | 6 | 
| The Big Short   | 2015 | 5 | 
| The Danish Girl | 2015 | 4 | 
| Room    | 2015 | 4 | 
| Ex Machina  | 2015 | 2 | 
| The Hateful Eight   | 2015 | 2 | 
| Inside Out  | 2015 | 2 | 
| Amy | 2015 | 1 | 
| Bear Story  | 2015 | 1 | 
| A Girl in the River: The Price of Forgiveness   | 2015 | 1 | 
| Son of Saul | 2015 | 1 | 
| Spectre | 2015 | 1 | 
| Stutterer   | 2015 | 1 | 
```
