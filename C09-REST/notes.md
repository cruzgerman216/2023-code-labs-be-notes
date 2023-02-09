## Representational State Transfer

### Todos

- [ ] Create a simple Ruby on Rails application with a "Product" resource. The "product" resource should have a name, description, stock, price and image url
- [ ] Use RESTful routes to map the CRUD operations to the appropriate actions and views.

### Database and Models

**Terminal**

```
  rails g model Product name:string description:string price:decimal image_url:string stock:integer
```

Run 
```
  rails db:migrate
```

**app/models/product.rb**

```ruby
class Product < ApplicationRecord
  validates :name, :description, :stock, :price, :image_url, presence: true
end
```

### Defining RESTful routes

**config/routes.rb**

```ruby
Rails.application.routes.draw do
  root to: "products#index"
  resources :products
end
```

### Index Action

- Create a file called products_controller.rb in app/controllers

**app/controllers/products_controller.rb**

```ruby
class ProductsController < ApplicationController
  # GET /products
  def index
    @products = Product.all
  end
end
```

- create a file called index.html.erb in app/views/products

**app/views/products/index.html.erb**

```html
<h1>Products</h1>

<div id="products">
  <% @products.each do |product| %>
    <%= render product %>
    <p><%= link_to "Show this product", product %></p>
  <% end %>
</div>

<%= link_to "New product", new_product_path %>
```

- Create a file in app/views/products called _product.html.erb as a partial

```html
<div id="<%= dom_id product %>">
  <p>
    <strong>Name:</strong>
    <%= product.name %>
  </p>

  <p>
    <strong>Description:</strong>
    <%= product.description %>
  </p>

  <p>
    <strong>Price:</strong>
    <%= product.price %>
  </p>

  <p>
    <strong>Image url:</strong>
    <%= image_tag product.image_url %>
  </p>

  <p>
    <strong>Stock:</strong>
    <%= product.stock %>
  </p>
</div>
```

- Create a product record in the Rails console to showcase your creation in the index page.
  - Navigate to `localhost:3000/products`

### Show Action

**app/controllers/products_controller.rb**

```ruby
class ProductsController < ApplicationController

  # GET /products
  def index
    @products = Product.all
  end

  # GET /products/1
  def show
      @product = Product.find(params[:id])
  end
end
```

- create show.html.erb in app/views/products

**app/views/products/show.html.erb**

```html
<%= render @product %>

<div>
  <%= link_to "Edit this product", edit_product_path(@product) %> |  <%= link_to "Back to products", products_path %> 
   <%= button_to "Destroy this product", @product, method: :delete %>
</div>

```

- Navigate to the show page for product

### New Action

**app/controllers/products_controller.rb**

```ruby
class ProductsController < ApplicationController

  # GET /products
  def index
    @products = Product.all
  end

  # GET /products/1
  def show
      @product = Product.find(params[:id])
  end

    # GET /products/new
  def new
    @product = Product.new
  end
end
```

- create new.html.erb in app/views/products

**app/views/products/new.html.erb**

```html
<h1>New product</h1>

<%= render "form", product: @product %>

<br />

<div><%= link_to "Back to products", products_path %></div>
```

In the products directory, create the partial for form called _form.html.erb.

```html
<%= form_with(model: product) do |form| %> <% if product.errors.any? %>
<div style="color: red">
  <h2>
    <%= pluralize(product.errors.count, "error") %> prohibited this product from
    being saved:
  </h2>

  <ul>
    <% product.errors.each do |error| %>
    <li><%= error.full_message %></li>
    <% end %>
  </ul>
</div>
<% end %>

<div>
  <%= form.label :name, style: "display: block" %> <%= form.text_field :name %>
</div>

<div>
  <%= form.label :description, style: "display: block" %> <%= form.text_field :description %>
</div>

<div>
  <%= form.label :price, style: "display: block" %> <%= form.text_field :price%>
</div>

<div>
  <%= form.label :image_url, style: "display: block" %> 
  <%= form.text_field :image_url %>
</div>

<div>
  <%= form.label :stock, style: "display: block" %> <%= form.number_field :stock%>
</div>

<div><%= form.submit %></div>
<% end %>
```

- Navigate to new page and check if no errors arise when the page has been brought

### Create Action

**app/controllers/products_controller.rb**

```ruby
class ProductsController < ApplicationController

  # GET /products
  def index
    @products = Product.all
  end

  # GET /products/1
  def show
      @product = Product.find(params[:id])
  end

    # GET /products/new
  def new
    @product = Product.new
  end

    def create
    @product = Product.new(product_params)

      if @product.save
        flash[:notice] = "saved successfully"
        redirect_to @product
      else
        render :new, status: :unprocessable_entity
      end
  end
end
```

- Define a private method called product_params that will essentially check to see if the request body meets the criteria of information for a product record

```ruby
  private
    # Only allow a list of trusted parameters through.
    def product_params
      params.require(:product).permit(:name, :description, :price, :image_url, :stock)
    end
```

**app/views/layouts/application.html.erb**

- Check to see if the flash notice exists if so, print the notice.

```html
<% if flash[:notice] %> 
  <%= flash[:notice] %>
 <% end %>
```

- Test out the new page in creating a form

### Edit Action

**app/controllers/products_controller.rb**

```ruby
class ProductsController < ApplicationController

  # GET /products
  def index
    @products = Product.all
  end

  # GET /products/1
  def show
      @product = Product.find(params[:id])
  end

    # GET /products/new
  def new
    @product = Product.new
  end

    def create
    @product = Product.new(product_params)

      if @product.save
        flash[:notice] = "saved successfully"
        redirect_to @product
      else
        render :new, status: :unprocessable_entity
      end
  end

    # GET /products/1/edit
  def edit
      @product = Product.find(params[:id])
  end

    private
    # Only allow a list of trusted parameters through.
    def product_params
      params.require(:product).permit(:name, :description, :price, :image_url, :stock)
    end
end
```

**app/views/products/edit.html.erb**

```html
<h1>Editing product</h1>

<%= render "form", product: @product %>

<br>

<div>
  <%= link_to "Show this product", @product %> |
  <%= link_to "Back to products", products_path %>
</div>
```

### Update Action 

**app/controllers/products_controller.rb**

```ruby
class ProductsController < ApplicationController

  # GET /products
  def index
    @products = Product.all
  end

  # GET /products/1
  def show
      @product = Product.find(params[:id])
  end

    # GET /products/new
  def new
    @product = Product.new
  end

    def create
    @product = Product.new(product_params)

      if @product.save
        flash[:notice] = "saved successfully"
        redirect_to @product
      else
        render :new, status: :unprocessable_entity
      end
  end

    # GET /products/1/edit
  def edit
      @product = Product.find(params[:id])
  end

    # PATCH/PUT /products/1 or /products/1.json
  def update
      @product = Product.find(params[:id])

      if @product.update(product_params)
        flash[:notice] = "Updated Successfully"
        redirect_to product_url(@product)
      else
         render :edit, status: :unprocessable_entity 
      end
  end

  private
    # Only allow a list of trusted parameters through.
    def product_params
      params.require(:product).permit(:name, :description, :price, :image_url, :stock)
    end
end
```

- Test out by editing a form


### Destroy Action

**app/controllers/products_controller.rb**

```ruby
class ProductsController < ApplicationController

  # GET /products
  def index
    @products = Product.all
  end

  # GET /products/1
  def show
      @product = Product.find(params[:id])
  end

    # GET /products/new
  def new
    @product = Product.new
  end

    def create
    @product = Product.new(product_params)

      if @product.save
        flash[:notice] = "saved successfully"
        redirect_to @product
      else
        render :new, status: :unprocessable_entity
      end
  end

    # GET /products/1/edit
  def edit
      @product = Product.find(params[:id])
  end

    # PATCH/PUT /products/1 or /products/1.json
  def update
      @product = Product.find(params[:id])
      if @product.update(product_params)
        flash[:notice] = "Updated Successfully"
        redirect_to product_url(@product)
      else
         render :edit, status: :unprocessable_entity 
      end
  end

    def destroy
      @product = Product.find(params[:id])
      @product.destroy
      flash[:notice] = "Product was successfully destroyed." 
      render redirect_to products_url
    end

    private
    # Only allow a list of trusted parameters through.
    def product_params
      params.require(:product).permit(:name, :description, :price, :image_url, :stock)
    end
end
```

- Test out by navigating to show page and deleting a product

### Refactor

**app/controllers/product_controllers.rb**

- Define a private method called set_product. This method will essentially declare an instance variable for certain actions. 

```ruby
  private
      # Only allow a list of trusted parameters through.
    def product_params
      params.require(:product).permit(:name, :description, :price, :image_url, :stock)
    end

    # Use callbacks to share common setup or constraints between actions.
    def set_product
      @product = Product.find(params[:id])
    end
```

- Call before_action to execute set_product for specific actions 
  - this will trigger set_product before the action is executed
  
```ruby 
class ProductsController < ApplicationController
  before_action :set_product, only: %i[ show edit update destroy ]
.
.
.
```

- Remove the line from show, edit, update and destroy

```ruby
      @product = Product.find(params[:id])
```

```ruby
class ProductsController < ApplicationController
  before_action :set_product, only: %i[ show edit update destroy ]

  # GET /products
  def index
    @products = Product.all
  end

  # GET /products/1
  def show
  end

    # GET /products/new
  def new
    @product = Product.new
  end

    def create
    @product = Product.new(product_params)

      if @product.save
        flash[:notice] = "saved successfully"
        redirect_to @product
      else
        render :new, status: :unprocessable_entity
      end
  end

    # GET /products/1/edit
  def edit
  end

    # PATCH/PUT /products/1 
  def update
      if @product.update(product_params)
        flash[:notice] = "Updated Successfully"
        redirect_to product_url(@product)
      else
         render :edit, status: :unprocessable_entity 
      end
  end

    def destroy
      @product.destroy
      flash[:notice] = "Product was successfully destroyed." 
      render redirect_to products_url
    end
  end

    private
    # Only allow a list of trusted parameters through.
    def product_params
      params.require(:product).permit(:name, :description, :price, :image_url, :stock)
    end
end
```

### Exercises

<hr />

**Exercise 1.1: Posts**

- Create a simple Ruby on Rails application with a "Posts" resource. The "Posts" resource should have a title and a body. Use RESTful routes to map the CRUD operations to the appropriate actions and views. Do this manually without the scaffold generator.
- Title and body should never be empty for a given post record.
- Error messages should prompt the user when there is a problem saving an invalid post 
- Use partials to refactor the view templates 
  
- Use the faker gem and the seeds file to populate the database with more than 50 post records
- https://github.com/faker-ruby/faker

**Exercise 1.2: Comments** 
In continuation from exercise 1.1,

- Create a resource called comment. A comment should have attributes content and a post_id. 
- An association should be developed in which a comment belongs to a post and a post can have many comments
  - https://guides.rubyonrails.org/association_basics.html
- RESTful routes should be defined to map CRUD operations except for index, show
- Here is a resource to help along this relationship between posts and comments. 
  - https://guides.rubyonrails.org/routing.html#nested-resources
- When navigating to a post page, you should see all the comments that belong to that post 

- Use the faker gem and the seeds file to populate the database with comments that target a post randomly. 
  - For instance, a post can have 5 comments whereas another post can have 10 comments

**Exercise 1.3: Basic Search**
Implement a custom action that allows one to search for posts. 

I would suggest creating a new erb file to display these search results. 

**Exercise 1.4: Pagination**
- Implement Pagination. Limit 10 posts per page for index. 
  - Gems are not permitted. 

**Exercise 1.5: Bootstrap**
- Install Bootstrap and style each post and comment 

**Exercise 2.1: Movies** 
- Create a simple Ruby on Rails application with a "Movies" resource. The "Movies" resource should have a title, director, and release year. 
- Add validation to the "Movies" model to ensure that the title, director, and release year are all present. 
- Use RESTful routes to map the CRUD operations to the appropriate actions and views.

**Exercise 2.2: Movies Search** 
- Implement a custom action on the "Movies" resource to allow users to search for movies by title or director.

**Exercise 2.3: Review**
- Add a ratings resource to the application, and allow users to rate movies.
