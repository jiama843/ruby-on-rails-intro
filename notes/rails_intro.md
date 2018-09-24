https://paper.dropbox.com/doc/Intro-to-Rails--AL6yJn3N7qvkIzmZioh_Za~EAg-Dgeo1UjYWtzrhCyOo3e6I

# Intro to Rails

----------
![Image result for Ruby on Rails workflow](https://chetankalore.files.wordpress.com/2010/12/ruby-on-rails-application-workflow.png?w=672)




## Description

A web application development framework written in Ruby. Designed in such a way as to increase productivity.

2 Major Principles:

**DRY → Don’t Repeat Yourself**

DRY is a principle of software development in which every piece of knowledge must have one distinct representation on a system.

**Convention Over Configuration**

Rails will by default follow it’s own set of conventions to prevent users from having endless configuration files.


# Simple Rails Project - Blog

To create a new rails application, in terminal enter the command:

    rails new blog

**blog** will be the root folder in a directory structure representing the **Ruby on Rails webapp**.

The **app** file will contain the main code (controllers, models, views, helpers, mailers, channels, jobs and assets).

![Base Contents of every Ruby on Rails application](https://d2mxuefqeaa7sj.cloudfront.net/s_B9EA5557BBFC2DFE5DC9010F9057162E0E800B1DE390866B4AB78189AF25BFE8_1536090372226_image.png)


From a glance it appears that to learn how an existing Rails application works, you need to understand the **app/, bin/, config/ and db/** folders

## Starting Up

To start the rails server run the command in /blog (directory root of project):

    bin/rails server

After this, the page should be online.

Access the page at:
http://localhost:3000

## Creating a Controller, Action and View - Hello World

To create a controller, run the “controller generator”:

    bin/rails generate controller Welcome index


![Log of files created after running generate controller](https://d2mxuefqeaa7sj.cloudfront.net/s_B9EA5557BBFC2DFE5DC9010F9057162E0E800B1DE390866B4AB78189AF25BFE8_1536095805566_image.png)

![Resulting controller created by the script](https://d2mxuefqeaa7sj.cloudfront.net/s_B9EA5557BBFC2DFE5DC9010F9057162E0E800B1DE390866B4AB78189AF25BFE8_1536095863977_image.png)


**Initializing a Webpage**

To tell rails where the actual home page location is, we modify the **config/routes.rb** file:

    Rails.application.routes.draw do
      get 'welcome/index'
      
      root 'welcome#index'
    end

**root 'welcome#index'** tells Rails to map requests to the root of the application to the welcome controller’s index action.

**get ‘welcome/index’** tells Rails to map requests to http://localhost:3000/welcome/index to the welcome controller's index action.


![Now the root is index.html](https://d2mxuefqeaa7sj.cloudfront.net/s_B9EA5557BBFC2DFE5DC9010F9057162E0E800B1DE390866B4AB78189AF25BFE8_1536155408387_image.png)


**Editing a Webpage**
Editing is just a matter of understanding html, how you can make it say hello world!

## Creating a Resource (Article)

A **resource** is a collection of similar objects, such as articles, people or animals. 

You can:

- **C**reate
- **R**ead
- **U**pdate
- **D**estroy 

these items (referred to as **CRUD**).

Rails provides a **resources** method that you can use to declare a standard REST resource.

You need to add the article resource to the **config/routes.rb**:

    Rails.application.routes.draw do
      get 'welcome/index'
      
      resources :articles
      
      root 'welcome#index'
    end

After setting resources to article, an **article controller** needs to be defined in order to serve the request.


    bin/rails generate controller Articles
# Controllers (Application Controller)

https://guides.rubyonrails.org/action_controller_overview.html

## Description

A controller in RoR is defined as a class which inherits from **ApplicationController**. It is possible to override/add methods to the this class for custom features.

## Methods and Actions

A controller class should contain methods and perform actions.

For example:

    class ClientsController < ApplicationController:
      def new
        @Clients = Clients.new
      end
    end

If the a user goes to the extension **/clients/new** to add a new client, Rails will create a new instance of **ClientsController** and call its **new** method.

## Parameters

https://api.rubyonrails.org/classes/ActionController/Parameters.html

There are 2 types of parameters:

- query string → Everything after ? in a URL
- POST data → Usually from an html form that comes from the user

Both of these parameters are available in a **param** object.

Case 1: Query String → Depending on the URL, we can access elements of the **params** (appears to be a map structure) with appropriate arguments

    class ClientsController < ApplicationController
      # clients: /clients?status=activated
      def index
        if params[:status] == "activated"
          @clients = Client.activated
        else
          @clients = Client.inactivated
        end
      end
    end

Case 2: POST Parameters → 

    class ClientsController < ApplicationController
      # POST data stored in /clients
      def create
        @client = Client.new(params[:client])
        if @client.save
          redirect_to @client
        else
          # This line overrides the default rendering behavior, which
          # would have been to render the "create" view.
          render "new"
        end
      end
    end


# Models (Active Record)

https://guides.rubyonrails.org/active_record_basics.html

## Object Relational Mapping (ORM)

A direct mapping between the objects in an application and the relational database.

***The important thing to note about Ruby on Rails is that objects are represented as entries in the database.***

## CRUD: Reading and Writing Data

**Create**
Active record API supports easy creation of a database entry

**Read**
Active record API supports easy reading of databases

**Update**
Active record API supports easy updating of databases

**Destroy**
Active record API supports easy destroying of databases

## Validations


## Callbacks

https://api.rubyonrails.org/classes/ActiveRecord/Callbacks.html

Usually the first lines of code of a controller. The 

# Routing

https://guides.rubyonrails.org/routing.html

## Description

The rails router recognizes URLs and dispatches them to a controller’s action, or to a Rack application.

To see the routes for the application run:

    bin/rails routes


## Connecting URLs to Code

When receiving a GET request, use the router to match it to a controller action

GET Request:

    GET /patients/17

Router Entry:

    get '/patients/:id', to: 'patients#show'

The request is dispatched to the **patients** controller’s **show** action with {  id: ’17’ } in **params.**

## Generating Paths and URLs from Code

If the route above is modified to be:

    get '/patients/:id', to 'patients#show', as: 'patient'

Controller code:

    @patient = Patient.find(params[:id])

View code:

    <%= link_to 'Patient Record', patient_path(@patient) %>

Then, the router will generate the path **/patients/17**.

## Configuring the Rails Router

All routes are located in **config/routes.rb** and it will typically have the form:

    Rails.application.routes.draw do
      resources :brands, only: [:index, :show] do
        resources :products, only: [:index, :show]
      end
    
      resource :basket, only: [:show, :update, :destroy]
      resolve("Basket") { route_for(:basket) }
    end

Typically, you would need a route for each action. 

Considering you may have all of the following routes for any given controller:

- index
- show
- new
- edit
- create
- update
- destroy

it is effective to use resource routing since you can declare them all in a single line of code.

e.g:

    resource :basket, only: [:show, :update, :destroy]

e.g:

    resources :photos

will create the following routes:

![](https://d2mxuefqeaa7sj.cloudfront.net/s_B9EA5557BBFC2DFE5DC9010F9057162E0E800B1DE390866B4AB78189AF25BFE8_1536162884056_image.png)

## Controller Namespaces and Routing

For organization purposes, you may wish to organize groups of controllers under a namespace.

The corresponding router entry for **app/controllers/admin** which contains **articles/** and **comments/** is:

    namespace :admin do
      resources :articles, :comments
    end

To route **/articles** to **Admin::ArticlesController** without constantly writing the **/admin** prefix

    scope module: 'admin' do
      resources :articles, :comments
    end

To route /**admin/articles** to **ArticlesController** without constantly writing the **Admin::** module prefix

    scope '/admin' do
      resources :articles, :comments
    end


## Nested Routing

Often times, resources will have children:

    class Magazine < ApplicationRecord
      has_many :ads
    end
    
    class Ad < ApplicationRecord
      belongs_to :magazine
    end

As a result, you can encompass nesting when routing:

    resources :magazines do
      resources :ads
    end

This corresponds to:

![](https://d2mxuefqeaa7sj.cloudfront.net/s_B9EA5557BBFC2DFE5DC9010F9057162E0E800B1DE390866B4AB78189AF25BFE8_1536168073924_image.png)


Although you can nest as many resources as you want, it is best practice to implement **shallow nesting**.

**Shallow Nesting**
There is a keyword called **shallow** which will tell rails to implicitly handle routing for nested resources in a certain way.

## Creating Paths and URLs From Objects

It is possible to create a path or URL from an array of parameters.

routes.rb code:

    resources :magazines do
      resources :ads
    end

View code:

    <= link_to 'Ad details', magazine_ad_path(@magazine, @ad) %>

When running **magazine_ad_path**, you can pass in instances of objects instead of numeric IDs.


## HTTP Verb Constraints (match keyword)

Usually, you use verbs GET, POST, PUT, PATCH, … to match routes with the given verb, but it is possible to match multiple verbs at once by using the **match** and **via** keywords.

Example of **match/via**:

    match 'photos', to: 'photos#show', via: [:get, :post] 

To match all verbs:

    match 'photos', to: 'photos#show', via: :all
# Mailing (Action Mailer)

https://guides.rubyonrails.org/action_mailer_basics.html
Action mailer is a ruby library that allows an application to send emails via mailer classes and views.

Mailer classes inherit from `ActionMailer::Base` and live in `app/mailers`, and they have associated views that appear in `app/views`.

## Sending Emails

To create a user mailer, run the following script:

     bin/rails generate mailer UserMailer

This is very similar to creating controllers. To create one without the shell script, just create a class that inherits from Action Mailer.

## Welcome email

In the **user_mailer.rb** file, add the following code:

    class UserMailer < ApplicationMailer
      default from: 'notifications@example.com'
     
      def welcome_email
        @user = params[:user]
        @url  = 'http://example.com/login'
        mail(to: @user.email, subject: 'Welcome to My Awesome Site')
      end
    end

We can call the **welcome_email** method to mail to a user with a defined **email**.

**default from:** states the email address that sent the message
**mail** will represent the actual message, with **to:** and **subject:** headers.

The **Mailer View** is an html file that represents the message being sent. 

A basic **Mailer View** (**welcome_email.html.erb** located in **app/views/user_mailer/**):

    <!DOCTYPE html>
    <html>
      <head>
        <meta content='text/html; charset=UTF-8' http-equiv='Content-Type' />
      </head>
      <body>
        <h1>Welcome to example.com, <%= @user.name %></h1>
        <p>
          You have successfully signed up to example.com,
          your username is: <%= @user.login %>.<br>
        </p>
        <p>
          To login to the site, just follow this link: <%= @url %>.
        </p>
        <p>Thanks for joining and have a great day!</p>
      </body>
    </html>

Some clients will prefer text over html, so it is general practice to send a textual representation as well.

A basic **Text File** (**welcome_email.text.erb** located in **app/views/user_mailer/**) would be:

    Welcome to example.com, <%= @user.name %>
    ===============================================
     
    You have successfully signed up to example.com,
    your username is: <%= @user.login %>.
     
    To login to the site, just follow this link: <%= @url %>.
     
    Thanks for joining and have a great day!

**Calling the mailer**

Create a **User** scaffold if it hasn’t already been done yet:

    bin/rails generate scaffold user name email login
    bin/rails db:migrate

Edit **users_controller.rb** to make a call to User Mailer after account creation (Typically in **create**):

    class UsersController < ApplicationController
      # POST /users
      # POST /users.json
      def create
        @user = User.new(params[:user])
     
        respond_to do |format|
          if @user.save
            # Tell the UserMailer to send a welcome email after save
            UserMailer.with(user: @user).welcome_email.deliver_later
     
            format.html { redirect_to(@user, notice: 'User was successfully created.') }
            format.json { render json: @user, status: :created, location: @user }
          else
            format.html { render action: 'new' }
            format.json { render json: @user.errors, status: :unprocessable_entity }
          end
        end
      end
    end
# Migrations
## Description

Convenient method of altering databases in a structured and organized manner. **Active Record** will automatically work out what migrations need to be run and it tracks which migrations have already been run.

## Structure of a Migration

The following is the general structure of what a migration looks like:

    class CreateProducts < ActiveRecord::Migration
      def up
        create_table :products do |t|
          t.string :name
          t.text :description
          t.timestamps
        end
      end
      def down
        drop_table :products
      end
    end
## Creating Migrations

Run the following line of code to generate a new migration

    rails generate migration MIGRATION_NAME

Afterwards, you can edit the migration:

    class MIGRATION_NAME < ActiveRecord::Migration[5.0]
      def change
        #insert database changes
      end
    end

Then you can apply the migration by running the following script and it will modify the existing database:

    bin/rails db:migrate
# Configuring Rails Components

https://guides.rubyonrails.org/v4.2/configuring.html
There are 4 standard ways to initialize code in Rails:

- **config/application.rb**
- Environment-specific configuration files
- Initializers
- After-initializers
## General Configuration


# SQL and Rails

https://medium.freecodecamp.org/understanding-the-basics-of-ruby-on-rails-sql-databases-and-how-they-work-7a628cd42073

# Spec
## spec_helper


## rails_helper


# Helpful Links

https://stackoverflow.com/questions/4836820/what-is-the-meaning-of-do-in-ruby

