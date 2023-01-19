# Dictionary


### Gems 
In Ruby, a gem is a package of code that can be shared, reused, and distributed among different projects and applications. Gems are used to add functionality to a Ruby application, and they typically include one or more Ruby files, as well as any necessary files such as documentation, tests, and binary files.

A gem typically provides a specific set of functionality, such as an HTTP client library, a web framework, or a testing framework. Many gems are open-source and maintained by the Ruby community. They can be easily installed, updated, and managed using Ruby's built-in package manager, gem. You can find the ruby gems by searching in the rubygems.org.

Creating a ruby gem involves following the steps like creating a project structure, creating a gemspec file, Building the gem and then publishing it to rubygems.org.


### BCrypt
Bcrypt is a Ruby gem that provides a simple wrapper for securely hashing passwords using the bcrypt algorithm. The bcrypt algorithm is a password hashing function that is designed to be secure and slow, making it difficult for attackers to use brute-force methods to guess a password. When a user's password is hashed with bcrypt, the resulting hash is unique for that password and cannot be reversed to reveal the original password. The bcrypt gem also includes a function for checking if a given password matches a previously hashed password, making it a useful tool for implementing secure user authentication in Ruby applications.

### Rails 

Rails is a web development framework written in the programming language Ruby. It is designed to make building web applications easier and more efficient. One of the key features of Rails is that it is a Full Stack framework, which means that it provides everything you need to build a complete web application. This includes tools for handling the front-end (HTML, CSS, and JavaScript) and the back-end (server-side logic and databases).

Rails is known for its convention over configuration approach, which means that it has a set of default conventions for building web applications. This makes it easier to get started with Rails and allows developers to focus on writing code for their specific application, rather than having to configure a lot of low-level details.

Overall, Rails is a powerful and popular tool for building web applications, and it is used by many successful companies and websites, such as Airbnb, GitHub, and Shopify.

### REST 
REST, or Representational State Transfer, is a set of guidelines for building web services that allow for the creation, retrieval, updating, and deletion of resources. In Ruby on Rails, this can be implemented using various HTTP methods such as GET, PUT, PATCH, DELETE, and POST to interact with the resources.

### Resource
In the context of Ruby on Rails, a resource refers to a data object that can be accessed through a web application. For example, a resource could be a database record of a user, a blog post, or a product in an online store.

In RESTful web design, resources are typically accessed and manipulated through a series of HTTP requests, with each request corresponding to a specific action such as creating a new resource, retrieving an existing resource, updating an existing resource, or deleting a resource. In Ruby on Rails, these actions are implemented using controller actions, which handle the incoming HTTP requests and direct them to the appropriate model or view. The model is responsible for interacting with the database to create, retrieve, update, or delete the resource, while the view is responsible for rendering the resource in a user-friendly format, such as HTML or JSON.

### Controller Actions 
In the context of a Ruby on Rails application, an action is a public method defined in a controller class that is responsible for handling a specific request from the web server. When a request is made to a Rails application, the routing system determines which controller and action should be responsible for handling the request, and invokes the corresponding action method.

### Rails Views 
In Ruby on Rails, views are the part of your application that displays information to the user. They are responsible for generating the HTML that your application sends to the client when a user navigates to a specific page.


