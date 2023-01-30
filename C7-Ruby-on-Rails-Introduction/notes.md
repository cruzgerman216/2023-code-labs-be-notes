## Introduction

### What is Ruby on Rails?

Ruby on Rails is a web application framework written in the Ruby programming language. It is designed for building web applications quickly and with less code, using conventions and best practices to automate common tasks.

### What is the internet? 

The internet is a global network of interconnected computers and servers that communicate with each other using standardized protocols. It allows for the sharing of information and resources, and enables communication and collaboration between users all over the world.

### DNS & IP Addresses

DNS stands for Domain Name System. It is a system that translates domain names (such as www.example.com) into IP addresses (such as 192.0.2.1) that computers use to identify each other on the internet. DNS is often referred to as the "phonebook of the internet." It is an essential service that allows users to access websites and other resources using easy-to-remember names rather than hard-to-remember IP addresses.

### What is HTTP

HTTP stands for Hypertext Transfer Protocol. It is the protocol used to transfer data over the web. HTTP is a request-response protocol, meaning that a client (such as a web browser) sends a request to a server (such as a website), and the server responds with the requested data. HTTP is used to transfer data for the World Wide Web, as well as for other applications such as RESTful web services.

HTTP uses a simple, text-based format to transmit data. This format makes it easy for humans to read, but it also makes it easy for computers to parse and understand. HTTP is also a stateless protocol, which means that it does not keep track of the client's previous requests.

HTTP uses TCP/IP layer, and that makes it a reliable protocol, it can detect errors and retransmit lost packets.

There are also other versions of HTTP like HTTP/2 and HTTP/3 that have been developed to improve upon the original HTTP protocol, providing faster and more efficient data transfer.

### REST

Representational State Transfer (REST) is an architectural style for building web services. It is based on a set of principles that define how web services should be designed and used. RESTful web services are designed to work with the HTTP protocol, which is used by the World Wide Web.

The main principles of REST are:

Statelessness: Each request from a client to a server must contain all of the information necessary to understand and fulfill the request. The server should not maintain any information about previous requests.
Client-Server architecture: The client and server are separate entities that communicate over a network. The server is responsible for storing and managing data, while the client is responsible for displaying and interacting with that data.
Cacheability: Responses from the server should indicate whether they can be cached by the client, so that the client can avoid making unnecessary requests.
Layered System: A RESTful architecture is typically composed of multiple layers, each with a specific responsibility.
RESTful web services are accessed using the standard HTTP methods (GET, POST, PUT, DELETE, etc.) and can return data in a variety of formats such as JSON or XML. RESTful web services are often used to create APIs (Application Programming Interfaces) that allow different applications to communicate and share data with each other.

The advantage of REST is that it is simple to understand and easy to implement, it uses standard HTTP methods and it is lightweight, thus making it suitable for Web and mobile applications.

A Restful state is a standard that Rails heavily follows in the act of resources. Think of a resource as an object we will perform actions upon. A resource describes any object, document or thing that you may need to store, update, delete or send to other services like your Front End Application. In a REST architecture, clients send requests to retrieve or modify resources, and servers send responses to these requests.

There are 7 operations to be made through a RESTful state.

- A get request to show all the cars in the browser. This action is called index.
- A get request to see an individual car in the browser. This action is called show.
- A get request to access a page to create a car. This action is called new.
- A post request to create a car. This action is called create.
- A get request to edit the car. This action is called edit.
- A put request to update the data of the cart. This action is called update.
- A delete request to delete car. This action is called delete.

This convention Rails utilizes makes it easier for us to know the specific operations to be made on the resource. Every resource is generally going to have these very common actions in a RESTful state. FE applications can expect the outcome of responses. It's a standard that is popular to follow. Rails heavily follows the principles of REST by encapsulating CRUD (create, read, update, delete) operations into models.

### URLS

A URL stands for Uniform Resource Locator. It is a string of text that specifies the location of a resource on the internet, such as a website or a specific web page. URLs are used by web browsers and other internet-enabled applications to access resources on the web.

A URL typically has the following format:

```
[protocol]://[domain name or IP address]/[path to resource]
```

- The protocol (e.g., "http", "https", "ftp") specifies how the resource should be accessed.
- The domain name or IP address specifies the location of the server that stores the resource.
- The path to the resource (e.g., "/about", "/contact") specifies the location of the resource within the server.

For example, the URL "https://www.example.com/about" specifies a resource on the server located at "www.example.com" that is accessed using the "https" protocol and is located at the path "/about"

URLs can also include additional information such as query parameters, that are used to specify additional information to the server, this information is usually passed using the "?" character, for example: "https://www.example.com/search?q=example" where "q" is the parameter and "example" is the value passed.

URLs are an important aspect of the web and are used by web browsers, search engines and other applications to access resources on the internet.

### The Path Through MVC

Ruby on Rails is a popular web application framework that is built on the Model-View-Controller (MVC) architectural pattern. In this video, we will explore the basics of the MVC pattern and how it is implemented in Ruby on Rails.

MVC is a software design pattern that separates an application into three main components: the model, the view, and the controller. These components are responsible for different aspects of the application, and they work together to provide a flexible and modular structure for web applications.

The model component of an MVC application is responsible for managing the data and business logic of the application. It is the central component of the application, and it defines the data structures and algorithms that the application uses to store and manipulate data. In a Ruby on Rails application, the model is typically implemented as a class that inherits from the ActiveRecord base class. This provides a convenient way to define and manipulate data stored in a database, and to apply business logic and validation rules to the data.

The view component of an MVC application is responsible for presenting the user interface (UI) of the application. It is the part of the application that the user sees and interacts with, and it is typically implemented as a template that contains HTML, CSS, and JavaScript code. In a Ruby on Rails application, the view is typically implemented using the ERB (Embedded Ruby) templating language, which allows you to embed Ruby code within HTML templates. This allows you to easily generate dynamic and interactive UI elements based on the data and logic in your model.

The controller component of an MVC application is responsible for handling user input and requests, and for coordinating the interactions between the model and the view. It is the link between the model and the view, and it is responsible for applying the business logic of the application and for rendering the appropriate view for each request. In a Ruby on Rails application, the controller is implemented as a class that inherits from the ApplicationController base class. This provides a convenient way to define the routes and actions that handle user requests, and to pass data between the model and the view.

In summary, the MVC pattern provides a powerful and flexible way to structure.

### APIs

APIs, or Application Programming Interfaces, are a set of protocols, routines, and tools for building software applications. An API specifies how software components should interact with each other, and it provides a way for developers to access the functionality of a system or library from within their own applications.

APIs can be used to enable communication and data exchange between different software systems. For example, an API could allow a web-based application to access data from a database, or it could allow a mobile app to access the features of a device's operating system. APIs can also be used to expose the functionality of a system or library to other developers, allowing them to build new applications or features on top of the existing system.

In general, APIs are an important tool for enabling software interoperability and integration. They allow developers to build applications that take advantage of the capabilities of other systems and libraries, and they make it easier to develop complex and powerful software applications.

### HTTP Status Codes: What They Are and Why They Matter

When you make a request to a web server, have you ever wondered what happens behind the scenes? How does the server know what you're asking for, and how does it decide what to send back?

One key part of this process is the HTTP status code. This is a three-digit number that the server sends back to you along with the data you requested. It provides important information about the result of your request, and it helps you understand what to do next.

So what exactly are HTTP status codes, and why are they important? Let's take a closer look.

When you make a request to a web server, you're asking the server to provide you with some data or perform some action on your behalf. This could be anything from loading a web page to submitting a form, or even just checking the time.

When the server receives your request, it processes it and generates a response. This response contains the data you requested, along with some additional information. This information includes the HTTP status code, which is a three-digit number that provides information about the result of your request.

There are many different HTTP status codes, and each one has a specific meaning and significance. Some of the most common codes are:

200 OK: This is the most common code, and it indicates that the request was successful and the server was able to provide the requested data.

301 Moved Permanently: This code indicates that the requested resource has been permanently moved to a new location. The client should use the new URL provided in the response to access the resource in the future.
404 Not Found: This code indicates that the requested resource could not be found on the server. This may mean that the resource does not exist, or that the client does not have permission to access it.
500 Internal Server Error: This code indicates that the server encountered an unexpected error while processing the request. This may be due to a bug in the server code, or to a problem with the server configuration or environment.
These are just a few examples of the many different HTTP status codes that exist. Each code has a specific meaning and significance, and it provides important information to the client about the result of their request.

So why are HTTP status codes important? Well, for one thing, they help clients understand the result of their request. If the server sends back a 200 OK code, the client knows that the request was successful and that it can proceed to use the data that was returned. If the server sends back a 404 Not Found code, the client knows that the resource they were looking for could not be found, and they can take appropriate action, such as displaying an error message or redirecting to a different page.

Status codes are also important for developers who are building web applications. They provide a standard way for servers to communicate with clients, and they allow developers to create applications that can handle different types of responses in a consistent and predictable way.

If you want to learn more about HTTP status codes, or if you're a developer who wants to create web applications that use status codes effectively, there are many resources available online. You can find detailed information about the different codes, their meanings, and their significance, as well as tips and best practices for using them in your own projects.

So remember, next time you make a request to a web server, take a look at the status code that comes back. It may not seem like much, but it can provide valuable insights and information that can help you understand what's happening behind the scenes.

### Authentication

Web authentication is a method of verifying the identity of a user or device that is accessing a website or web application. It is a process that typically involves the use of credentials, such as a username and password, to prove that the user or device is authorized to access the site or application.

## Creating a Rails Project

Create a new Rails Project called byte_size_news.

```
rails new byte_size_news
```

### Byte Size News Todos

The imaginable Client wants the following:

- [ ] About page
- [ ] Terms & Conditions Page
- [ ] Home Page
- [ ] Search Bar

### Static Pages

**config/routes.rb**

- Define the routes for the about page, terms and conditions page and the home page

```ruby
Rails.application.routes.draw do
  root 'pages#home'
  get '/about', to: 'pages#about'
  get '/terms', to: 'pages#terms'
end
```

- run rails routes in the terminal to see all three defined routes

### Pages Controller

- Under **app/controllers/**, create a file called pages_controller.rb
  - Define the class PagesController that inherits from ApplicationController
  - Define instance methods home, about and terms

```ruby
class PagesController < ApplicationController
  def home
  end

  def about
  end

  def terms
  end
end
```

### Views

In **app/views**, create folder called pages.

- create home.html.erb, about.html.erb and terms.html.erb
- **app/views/pages/home.html.erb**

```html
<h1>Byte Size News: Your Daily Source for Tech News & Trends</h1>
<p>
  Stay ahead of the curve with Byte Size News, the go-to destination for all
  things programming and technology. From the latest advancements in software
  development to insightful analysis of the industry, we bring you the news and
  trends that matter most. Keep up-to-date with the fast-paced world of tech,
  only on Byte Size News.
</p>
```

**app/views/pages/about.html.erb**

```html
<h1>About Us</h1>
<p>
  Welcome to Byte Size News, your daily source for bite-sized technology updates
  and insights. We believe that staying informed should be quick, easy, and
  accessible to everyone. That's why we've created a platform that delivers the
  most important news and trends in a compact and to-the-point format. Our team
  of experts and passionate tech enthusiasts work tirelessly to bring you the
  latest and greatest in the world of technology. Join us on this journey of
  discovery, and stay ahead of the curve with Byte Size News.
</p>
```

**app/views/pages/terms.html.erb**

```html
<h1>Terms and Conditions</h1>
<p>
  These terms and conditions govern your use of the Byte Size News website and
  its services. By accessing and using our site, you agree to be bound by these
  terms and conditions, as well as our privacy policy:
</p>
<ul>
  <ol>
    1. Intellectual Property: Lorem ipsum dolor sit amet, consectetur adipiscing
    elit.
  </ol>
  <ol>
    1. User Conduct: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
  </ol>
  <ol>
    1. Liability Disclaimer: Lorem ipsum dolor sit amet, consectetur adipiscing
    elit.
  </ol>
</ul>
```

Run `rails server` in the terminal to check the results.

### Navbar

**views**

- Create a folder called shared
  - create \_nav.html.erb

```html
<ul>
  <li><%= link_to 'Home', root_path %></li>
  <li><%= link_to 'About', about_path %></li>
  <li><%= link_to 'Terms', terms_path%></li>
</ul>
```

**views/layouts/application.html.erb**

```html
<body>
  <%= render 'shared/nav'%> <%= yield %>
</body>
```

### Search Bar

**config/routes.rb**

- add a namespace called news
  - _A namespace is a way to group similar controllers and routes together._
  - In the namespace, create a route for search

```ruby
Rails.application.routes.draw do
  root 'pages#home'
  get '/about', to: 'pages#about'
  get '/terms', to: 'pages#terms'

  namespace :news do
    get '/search', to: 'search#search_news'
  end
end
```

**app/controllers**

- Create a folder called news
  - Inside news, create a folder called search
    - Define a module called news (namespaces require a module)
      - Define the search class in news and search_news action

```ruby
module News
  class SearchController < ApplicationController
    def search_news
    end
  end
end
```

**views/shared/\_nav.html.erb**

- Add a form to search for news
  - Use the form_with method, be sure the url is targeting "news/search".

```html
<ul>
  <li><%= link_to 'Home', root_path %></li>
  <li><%= link_to 'About', about_path %></li>
  <li><%= link_to 'Terms', terms_path%></li>
  <li>
    <%= form_with url: "/news/search", method: :get do |form| %> <%= form.label
    :query, "Search for:" %> <%= form.text_field :query %> <%= form.submit
    "Search" %> <% end %>
  </li>
</ul>
```

**controllers/news/search**

- Set an instance variable to the query the user entered from the search form

```ruby
module News
  class SearchController < ApplicationController
    def search_news
      @search = params[:query]
    end
  end
end
```

**views**

- Create a folder called news
  - In news, create an additional folder called search
    - In news/search, create a file called search_news.html.erb

```html
<h1>Search</h1>
<p>This is what you searched for <b><%= @search%></b></p>
```

- Test out the search

# Exercises

**Exercise 1.1: Job Board**

1.  Generate a new rails app called rails_job_board_exercise
2.  Create a GET request route with the path '/jobs

    1. Target a controller called jobs.
    2. The action to be triggered should be called index
       1. Imagine we have the following job postings

    ```ruby
    [
     { company: "Stark Enterprises", position: "Ruby Developer", location: "St. Louis, MO" },
     { company: "WayneEnterprises", position: "Ruby on Rails Engineer", location: "Kansas City, MO" },
     { company: "OsCorp", position: "Full Stack Ruby Developer", location: "Springfield, MO" }, { company: "Hydra", position: "Ruby Engineer", location: "Columbia, MO" },
     { company: "S.H.I.E.L.D.", position: "Ruby on Rails Developer", location: "St. Joseph, MO" },
    ]
    ```

    Set this to an instance variable

    3.  Render the contents of the instance variable in a template

3.  The root path of the app should redirect the user to '/jobs'

**Exercise 1.2: Learning Platform**

1. Generate a rails application called rails_learning_platform_exercise
2. This application should have the following pages
   1. Homepage
   2. About Us
   3. Contact Us
   4. FAQ
   5. Terms of Service
   6. Privacy Policy
   7. Course catalog
   8. Testimonials
   9. Blog
      1.  For this page, make sure the route is targeting a controller called blogs. Trigger an action called index.
      2.  Here is an array of blogs 
      ```ruby 
       [  "Introduction to Ruby on Rails",  "The Benefits of Pair Programming",  "How to Use Git for Version Control",  "A Guide to Test-Driven Development",  "The Future of Web Development: React vs Angular",  "Best Practices for Designing User Interfaces",  "How to Optimize Your Website for Speed and Performance",  "The Importance of Accessibility in Web Design",  "How to Build Secure Web Applications",  "Exploring the Latest Trends in Web Development"]
      ```
      declare an instance variable and set it to this array 
    3. Render the instance variable contents in a view template.

3. Create a navbar that will link you to these pages 

**Exercise 1.3: Fast Food Customer Satisfaction Survey**
1. Generate a new project called rails_fast_food_exercise
2. Define 3 routes of the following
  - /survey/rating
  - /survey/multiple-choice-questions 
  - /survey/open-ended-feedback
  - /end

All routes should handle GET requests and target a controller called "Survey". Add a namespace for the survey path.

Define each action and render the related view templates. 

3. Each path except 'end' will include a form in the view templates. Do this in order

**rating**
- Allow the user to rate the overall experience they had from 1 - 10. 

After the user rates his/her overall experience, allow the user to submit and target the `multiple-choice-questions` controller. 

**multiple-choice-questions**
In the controller action, for multiple-choice-questions, use the session instance to store information of the user input. Here's an example, 

```ruby 
  def multiple_choice_question
    session[:rating] = params[:rating] 
  end
```

A session is a way to store information that can persist across multiple requests. It's used to maintain state between requests made by the same user. 

Follow the same process for the rest of the actions. 

In the template, 
- Allow the user to rate the quality and how likely they are likely to recommend to a friend. 

**open-ended-feedback**
- Allow the user to include any feedback. 

**end**
In the `end` action, render a template that will show all the information of the previous input of what the user entered.

**Exercise 1.4: Errors**
- Fix the [Rails project](https://github.com/cruzgerman216/CL-Rails-error-1)

You should be able to navigate from page to page by click on each link. 

# Project Brainstorming 

![project planning](../assets/images/C6/project.webp)

Here are examples of projects you may be interested in building.

```
Blog: Create a blogging platform where users can create, edit, and delete posts.

Social Network: Build a social network for users to connect, post updates, and share content.

E-commerce Store: Develop an e-commerce store with shopping cart functionality and payment processing.

Recipe App: Create a recipe app where users can search, save, and rate recipes.

Task Manager: Build a task manager where users can create, assign, and track tasks.

Online Marketplace: Create an online marketplace for buying and selling goods or services.

News Aggregator: Build a news aggregator that collects and organizes articles from multiple sources.

Bookmark Manager: Create a bookmark manager where users can save, organize, and categorize their favorite web pages.

Real Estate Listing: Develop a real estate listing platform where users can search and save properties.

Fitness Tracker: Build a fitness tracker where users can log their workouts, track their progress, and compare with others.
```

Here's a todo list 

- [ ] Name your App
- [ ] Create an ER Diagram to keep tack of what data you will track 
- [ ] Generate a series of static pages, here are examples: 

```
About Us: A page that provides information about the company or organization, its mission, and history.

Privacy Policy: A page that explains how the website collects, uses, and protects the user's personal information.

Terms of Service: A page that outlines the rules and guidelines for using the website.

FAQ: A page that lists and answers frequently asked questions about the website or its services.

Team: A page that introduces the members of the company or organization and their roles.

Careers: A page that provides information about job opportunities and how to apply.

Press: A page that includes press releases, media coverage, and other news related to the company or organization.

Blog: A page that showcases the company or organization's latest blog posts.

Donate: A page that provides information on how to support the company or organization through donations.
```
