# Crimson University


## Tables

```
rails g migration CreateCourses
```

```rb
class CreateCourses < ActiveRecord::Migration[7.0]
  def change
    create_table :courses do |t|
      t.references :professor, null: false, foreign_key: { to_table: :users }
      t.string :name

      t.timestamps
    end
  end
end
```

```
rails g migration CreateCoursesUsers
```

```rb
class CreateCoursesUsers < ActiveRecord::Migration[7.0]
  def change
    create_table :courses_users do |t|
      t.references :course, null: false, foreign_key: true
      t.references :user, null: false, foreign_key: true
      
      t.timestamps
    end
  end
end
```

Enter 
```
rails db:migrate
```

## Models 

Create a course.rb file under models 

```rb
class Course < ApplicationRecord
  belongs_to :professor, class_name: "User"
  has_and_belongs_to_many :students, class_name: 'User', join_table: :courses_users, association_foreign_key: 'user_id'
end
```

## Concerns 
Concern files are used to extract methods or logic from the model. 

In `models/concerns`, create a admin_methods.rb file 

```rb 
module AdminMethods
  extend ActiveSupport::Concern

  included do
    def admin?
      roles.exists?(slug: "student")
    end

    def self.admin_all
      User.joins(:roles).where("roles.slug = ?", "admin")
    end
  end
end
```

In `models/concerns`, create a professor_methods.rb file 

```rb
module ProfessorMethods
  extend ActiveSupport::Concern

  included do
    has_many :instructing_courses, class_name: "Course", foreign_key: "professor_id"
    def professor?
        roles.exists?(slug: "professor")
      end

    def self.professors
        User.joins(:roles).where("roles.slug = ?", "professor")
      end
  end
end
```

In `models/concerns`, create a student_methods.rb file 

```rb 
module StudentMethods
    extend ActiveSupport::Concern
  
    included do
        has_and_belongs_to_many :courses
      def student?
        roles.exists?(slug: "student")
      end
  
      def self.students
        User.joins(:roles).where("roles.slug = ?", "student")
      end
    end
  end
```

In the `models/user.rb` file, include all three concern methods 

```rb
class User < ApplicationRecord
  include ProfessorMethods
  include StudentMethods
  include AdminMethods
.
.
.
```

## Seed 

In ```models/roles```, 

```ruby 
# frozen_string_literal: true

# Model that stores all of the available roles
class Role < ApplicationRecord
  # cannot reassign known_roles to another value 
  # freeze method makes the object immutable
  KNOWN_ROLES = ["admin", "professor", "student"].freeze
  def self.create_roles 
    KNOWN_ROLES.each do |role|
      Role.find_or_create_by(slug: role)
    end
  end

  .
  .
  .
end
```


**seeds.rb**
```rb 
Role.create_roles
User.create(first_name: Faker::Name.first_name, last_name: Faker::Name.last_name,  email: "admin@admin.com", phone: Faker::PhoneNumber.phone_number, password: "password",  password_confirmation: "password", roles: [Role.find_by(slug: "admin")])
User.create(first_name: Faker::Name.first_name, last_name: Faker::Name.last_name,  email: "professor@professor.com", phone: Faker::PhoneNumber.phone_number, password: "password",  password_confirmation: "password", roles: [Role.find_by(slug: "professor")])
User.create(first_name: Faker::Name.first_name, last_name: Faker::Name.last_name,  email: "student@student.com", phone: Faker::PhoneNumber.phone_number, password: "password",  password_confirmation: "password", roles: [Role.find_by(slug: "student")])

professor = User.second
student = User.third 
student.courses << Course.create(name: "Ruby", professor: professor)
```

## Define Routes

**config/routes.rb**
```rb
.
.
.
  namespace :api, defaults: { format: :json } do
    namespace :v1 do
      namespace :users do
        post :login
        delete :logout
        get :me
        post :create
      end

      namespace :professors do 
        get :instructing_courses
      end

      namespace :students do 
        get :my_courses
      end

      namespace :admin do 
        get :professor_index
        get :student_index
      end
      
    end
  end
  .
  .
  .
```

## professor controller
In `controllers/api/v1` , create professors_controller.rb 

```rb
# frozen_string_literal: true

module Api
    module V1
      # Handles endpoints related to users
      class ProfessorsController < Api::V1::ApplicationController
        def instructing_courses
          render_success(payload: CourseBlueprint.render_as_hash(@current_user.instructing_courses), status: 200)
        end
      end
    end
  end
```

in `app/blueprints` create course_blueprint.rb 

```rb 
# frozen_string_literal: true

# Defines the JSON blueprint for the User model
class CourseBlueprint < Blueprinter::Base
    identifier :id
    fields :name, :professor, :students
  end
```

Test in postman. Be sure to login first because these requests need a token

## students controller
In `controllers/api/v1` , create professors_controller.rb 

```rb
# frozen_string_literal: true

module Api
    module V1
      # Handles endpoints related to users
      class StudentsController < Api::V1::ApplicationController
        def my_courses
          render_success(payload: CourseBlueprint.render_as_hash(@current_user.courses), status: 200)
        end
      end
    end
  end
  
```

Test in postman. Be sure to login first because these requests need a token


## admin controller
In `controllers/api/v1` , create professors_controller.rb 

```rb
# frozen_string_literal: true

module Api
    module V1
      # Handles endpoints related to users
      class AdminController < Api::V1::ApplicationController
        def professor_index
          render_success(payload: UserBlueprint.render_as_hash(User.professors, view: :professor), status: 200)
        end
        def student_index
            render_success(payload: UserBlueprint.render_as_hash(User.students, view: :student), status: 200)
          end
      end
    end
  end
```

in `app/blueprints/user_blueprint.rb` 

```rb 
# frozen_string_literal: true

# Defines the JSON blueprint for the User model
class UserBlueprint < Blueprinter::Base
.
.
.
  view :professor do 
    association :instructing_courses, blueprint: CourseBlueprint
  end

  view :student do 
    association :courses, blueprint: CourseBlueprint
  end

end
```

Test in postman. Be sure to login first because these requests need a token

**Warm Up**
Need a warm up? Go through the notes step by step and if you have any questions, ask your Code Coach!

## Full Stack Project

[Click here to see project requirements](../projects/FS-project.md)
