# Rails as an API

**Web API (Application Programming Interface)**
A web API is a tool for software applications to communicate and exchange data with each other over the internet. APIs are a set of protocols, routines, and tools for building software and applications.

-   Web APIs allow communication between two applications such as how requests and responses are structured and how data should be formatted.

**Ruby on Rails as an API**
Ruby on Rails is a popular framework for building APIs. In the context of Rails, the framework provides a set of tools and conventions that make it easy to create and manage API endpoints.
When a given Rails application is configured as an API, it includes limited set of middleware than normal:

-   Does not include any middleware that involves a Front End tooling like cookies.
-   Rails as an API is more lightweight, skipping views, helpers and assets when you generate a new Rails App.
-   Main building blocks are routes, controllers and models as well the connection point to the DB.

**Postman**

-   Postman is a popular collaboration platform for building and testing APIs.
-   When building a Ruby on Rails API, developers can use Postman to test and debug their API endpoints, allowing them to easily see the requests and responses, as well as any errors or issues that may arise.
-   Postman's built-in testing framework can be used to create and run tests for a Ruby on Rails API, helping to ensure that the API is working correctly and meeting the desired requirements.

**RSwag**
RSwag is a gem for Ruby on Rails applications that provides a simple and convenient way to document APIs.

-   With RSwag, developers can easily create API documentation for their endpoints, including request and response payloads, parameters, headers, and examples.
-   RSwag supports testing of API endpoints by generating request and response examples that can be used in tests, helping to ensure that the API documentation and the actual API implementation remain in sync.
-   RSwag is a valuable tool for Ruby on Rails developers who want to create high-quality, well-documented APIs that are easy to maintain and understand.

## Building an API

Create a new Rails API

```
rails new learning_resource_api --api
```

Create a Resource model

```
rails g model resource content:string link:string
```

```
rails db:migrate
```

### Define Routes

```rb
Rails.application.routes.draw do
  resources :resources, except: [:new, :edit]
end
```

## Create a resource with Postman
**app/controllers/resources_controller.rb**

```ruby 
class ResourcesController < ApplicationController
    def create
      resource = Resource.new(content: params[:content], link: params[:link])

      # define response
      if resource.save
        render json: resource, status: :created
      else
        render json: {errors: resource.errors}, status: :unprocessable_entity
      end
    end
end
```

Use postman to create a resource.

1. Create a workspace
2. Create a Collection
3. Add a request
4. Change HTTP method to POST
5. Attach the following to the body request.

```json
{
    "content": "Next.js Refreshing Server-Side Props",
    "link": "https://www.joshwcomeau.com/nextjs/refreshing-server-side-props/"
}
```

You should get the following as the response body.

```json
{
    "id": 1,
    "content": "Next.js Refreshing Server-Side Props",
    "link": "https://www.joshwcomeau.com/nextjs/refreshing-server-side-props/",
    "created_at": "2023-03-08T06:52:41.275Z",
    "updated_at": "2023-03-08T06:52:41.275Z"
}
```

### Get all Resources using Postman

**app/controllers/resources_controller.rb**

```ruby
class ResourcesController < ApplicationController


    def index
      resources = Resource.all
      render json: resources, status: :ok
    end

  end
```

Use postman to send a request to get all resources.

The expected response body should be

```json
[
    {
        "id": 1,
        "content": "Next.js Refreshing Server-Side Props",
        "link": "https://www.joshwcomeau.com/nextjs/refreshing-server-side-props/",
        "created_at": "2023-03-08T06:58:23.099Z",
        "updated_at": "2023-03-08T06:58:23.099Z"
    }
]
```

### Get a specific Resource using Postman

```ruby
    def show
      resource = Resource.find(params[:id])
      render json:resource, status: :ok
    end
```

### Update a specific resource using Postman

```ruby
    def update
      resource = Resource.find(params[:id])

      if resource.update(content: params[:content], link: params[:link])
        render json: resource, status: :ok
      else
        render json: {errors: resource.errors}, status: :unprocessable_entity
      end
    end
```

### Destroy a specific Resource using Postman

```ruby
    def destroy
      resource = Resource.find(params[:id])
      resource.destroy
      render json: {message: "resource deleted"}, status: :ok
    end
```

### Rack Corse

Install rack-cors

```ruby
# Use Rack CORS for handling Cross-Origin Resource Sharing (CORS), making cross-origin AJAX possible
gem "rack-cors"
```

**app/config/cors.rb**

```ruby
Rails.application.config.middleware.insert_before 0, Rack::Cors do
  allow do
    origins "*"

    resource "*",
      headers: :any,
      methods: [:get, :post, :put, :patch, :delete, :options, :head]
  end
end
```

To allow your FE app to send requests to your app.

## FE App

Create a new directory outside of the Rails app called `Learning-Resources-Client`

**Learning-Resources-Client/index.html**

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Learning Resources</title>
        <link rel="stylesheet" href="./assets/styles/main.css" />
    </head>
    <body>
        <h1 style="text-align: center">List of Resources</h1>
        <div class="resources-container"></div>
    </body>

    <script src="./src/helpers.js"></script>
    <script src="./api/resources.js"></script>
    <script src="./main.js"></script>

    <script></script>
</html>
```

- Create a resource in Postman.

**Learning-Resources-Client/main.js**

```js
getResources().then((data) => {
    console.log(data);
    data.forEach((resource) => {
        appendResourceToDOM(resource);
    });
});
```

**assets/styles/main.css**

```css
.container {
    width: 80%;
    margin: 0 auto;
    display: flex;
    flex-wrap: wrap;
}
.card {
    border: 1px solid black;
    margin: 10px;
    padding: 10px;
    display: inline-block;
}

.card a:hover {
    background: rgb(139, 139, 223);
    cursor: pointer;
}


```

**Learning-Resources-Client/src/helpers.js**

```js
function appendResourceToDOM(resource) {
    const container = document.querySelector(".resources-container");
    const card = document.createElement("div");
    const contentElem = document.createElement("a");

    card.classList.add("card");

    contentElem.href = resource.link
    contentElem.target = "_blank";
    contentElem.textContent = resource.content;
    
    card.appendChild(contentElem);
    container.appendChild(card);
}

```



### Create Resource

**Learning-Resources-Client/index.html**
```html
        <div><b>Create Resource</b></div>
        <form id="form-resource">
            <input type="text" name="content" placeholder="Content" />
            <input type="text" name="link" placeholder="Image link" />
            <button type="submit" value="continue">Create Resource</button>
        </form>
```

**main.js**

```js
const form = document.querySelector("#form-resource");
form.addEventListener("submit", (e) => onCreateResource(e));
```

**helpers.js**

```js
const onCreateResource = (e) => {
    debugger
    e.preventDefault();
    const content = e.target.content.value;
    const link = e.target.link.value;
    const resource = { link, content };
    createResource(resource).then((data) => {
        if (data.errors) {
            console.log(data.errors);
        } else {
            appendResourceToDOM(data);
        }
    });
}
```

**api/resources.js**

```js
function createResource(resource) {
    return fetch("http://localhost:3000/resources", {
        method: "POST",
        headers: {
            "Content-Type": "application/json",
        },
        body: JSON.stringify(resource),
    }).then((res) => res.json())
}
```

### Updating a Resource

**helpers.js**


```js

function appendResourceToDOM(resource) {
.
.
.
    const editBtn = document.createElement("button");
    editBtn.textContent = "Edit";
    editBtn.addEventListener("click", () => { onEditResource(resource, card, {contentElem, link: resource.link}) });
    card.appendChild(editBtn);
.
.
.
}
const onEditResource = (resource, card, cardElements) => {
    const editForm = document.createElement('form');
    const contentInput = document.createElement("input");
    const linkInput = document.createElement("input");
    const submitBtn = document.createElement("button");
    submitBtn.textContent = "Submit";
    contentInput.value = resource.content;
    linkInput.value = resource.link;
    editForm.appendChild(contentInput);
    editForm.appendChild(linkInput);
    editForm.appendChild(submitBtn);
    card.appendChild(editForm);
    submitBtn.addEventListener("click", (e) => {
        e.preventDefault();

        const content = contentInput.value;
        const link = linkInput.value;
        const updatedResource = { link, content };
        updateResource(resource.id, updatedResource).then((data) => {
            if (data.errors) {
                console.log(data.errors);
            } else {
                card.removeChild(editForm);
                cardElements.contentElem.textContent = data.content;
                cardElements.contentElem.href = data.link;
            }
        })
    });
}
```

**api/resources.js**

```js
function updateResource(id, updated_resource) {
    return fetch(`http://localhost:3000/resources/${id}`, {
        method: "PUT",
        headers: {
            "Content-Type": "application/json",
        },
        body: JSON.stringify(updated_resource),
    }).then((res) => res.json())
}
```


## Delete Resource 

**helpers.js**

```js 
function appendResourceToDOM(resource) {
.
.
.
    const deleteBtn = document.createElement("button");
    deleteBtn.textContent = "Delete";
    deleteBtn.addEventListener("click", () => {
        deleteResource(resource.id).then((data) => {
            card.remove();
        });
    });
    card.appendChild(deleteBtn);
.
.
.
```

**api/resources.js**

```js

function deleteResource(id) {
    return fetch(`http://localhost:3000/resources/${id}`, {
        method: "DELETE",
    }).then((res) => res.json())
}
```


Wallah! Now we have a small full stack web app that can perform all CRUD operations.

**Step by Step on how to Build a Rails API**

1. `rails new my_api —api`
2. Create an ER diagram
3. Define the schema of the Database
4. Create Models
5. Decide what sort of requests can an application send to the API
6. Define endpoints by creating routes a given application can request
7. Create controllers to perform an action that will respond to given requests
8. Use Postman to test out your endpoints
9. After creating successful endpoints, consider creating documentation if you are in a team environment.
10. Enable CORS to allow your web app to communicate with your API.
11. Create a FE application that is able to send requests to your API.
12. As you continue adding more additional services to this API, continue to repeat steps 3-9

**Recap**

-   A web API is a tool for software applications to communicate and exchange data with each other over the internet.
-   Ruby on Rails as an API is a framework for building APIs that enables developers to create web applications that can communicate with other software applications, exchange data, and perform various operations over the internet in a standardized way.
-   Postman is a tool for testing and documenting APIs that simplifies the process of sending HTTP requests, receiving responses, and debugging API calls during the development and testing of web applications.
    RSwag is a gem for Ruby on Rails that generates Swagger documentation for API endpoints, making it easier for developers to document and test their APIs.
-   The combination of Ruby on Rails and front-end frameworks is a powerful tool for building modern, responsive, and user-friendly web applications


### Exercises

**Warmup** - Read through the notes and recreate the Learning Resource App.

**1 Job Posting Web App**

API
- Create a Back End Rails API to serve a Front End Job Posting Web App 
  - This API should create the given resource: Job Posting 
A job posting can either be full time or part time.
A job posting should have a job description as well as qualifications.
A job posting should include the name of the company offering the job(a model isn't needed). 

- This API should be able to perform all CRUD operations on a job posting, use postman to test this. 

FE 
- Create a Front End in Vanilla JavaScript that will allow you to create, update, delete and get job postings. 
