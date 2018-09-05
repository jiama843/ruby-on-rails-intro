https://paper.dropbox.com/doc/Intro-to-Rails--AL6yJn3N7qvkIzmZioh_Za~EAg-Dgeo1UjYWtzrhCyOo3e6I

# Intro to Rails

----------

# Description

A web application development framework written in Ruby. Designed in such a way as to increase productivity.

2 Major Principles:

- DRY → Don’t Repeat Yourself

DRY is a principle of software development in which every piece of knowledge must have one distinct representation on a system.

- Convention Over Configuration

Rails will by default follow it’s own set of conventions to prevent users from having endless configuration files.


# Simple Rails Project - Blog

To create a new rails application, in terminal enter the command:

   
    rails new blog
   

blog will be the root folder in a directory structure representing the Ruby on Rails webapp.

The app file will contain the main code (controllers, models, views, helpers, mailers, channels, jobs and assets).

![Base Contents of every Ruby on Rails application](https://d2mxuefqeaa7sj.cloudfront.net/s_B9EA5557BBFC2DFE5DC9010F9057162E0E800B1DE390866B4AB78189AF25BFE8_1536090372226_image.png)



# Starting Up

To start the rails server run the command in /blog (directory root of project):

    
    bin/rails server
  

After this, the page should be online.

Access the page at:
http://localhost:3000


Creating a Controller, Action and View - Hello World

To create a controller, run the “controller generator”:

    bin/rails generate controller Welcome index


![Log of files created after running generate controller](https://d2mxuefqeaa7sj.cloudfront.net/s_B9EA5557BBFC2DFE5DC9010F9057162E0E800B1DE390866B4AB78189AF25BFE8_1536095805566_image.png)

![Resulting controller created by the script](https://d2mxuefqeaa7sj.cloudfront.net/s_B9EA5557BBFC2DFE5DC9010F9057162E0E800B1DE390866B4AB78189AF25BFE8_1536095863977_image.png)


# Initializing a Webpage

To tell rails where the actual home page location is, we modify the config/routes.rb file:

    Rails.application.routes.draw do
      get 'welcome/index'
      
      root 'welcome#index'
    end

root 'welcome#index' tells Rails to map requests to the root of the application to the welcome controller’s index action.

get ‘welcome/index’ tells Rails to map requests to http://localhost:3000/welcome/index to the welcome controller's index action.


![Now the root is index.html](https://d2mxuefqeaa7sj.cloudfront.net/s_B9EA5557BBFC2DFE5DC9010F9057162E0E800B1DE390866B4AB78189AF25BFE8_1536155408387_image.png)


Editing a Webpage
Editing is just a matter of understanding html, how you can make it say hello world!

- Creating a Resource (Article)

A resource is a collection of similar objects, such as articles, people or animals. 

You can:

- Create
- Read
- Update
- Destroy 

these items (referred to as CRUD).

Rails provides a resources method that you can use to declare a standard REST resource.

You need to add the article resource to the config/routes.rb:

    Rails.application.routes.draw do
      get 'welcome/index'
      
      resources :articles
      
      root 'welcome#index'
    end

After setting resources to article, an article controller needs to be defined in order to serve the request.


    bin/rails generate controller Articles


# Routing

The rails router recognizes URLs and dispatches them to a controller’s action, or to a Rack application.

To see the routes for the application run:

    bin/rails routes


- Connecting URLs to Code

When receiving a GET request, use the router to match it to a controller action

GET Request:

    GET /patients/17

Router Entry:

    get '/patients/:id', to: 'patients#show'

The request is dispatched to the patients controller’s show action with {  id: ’17’ } in params.

- Generating Paths and URLs from Code

If the route above is modified to be:

    get '/patients/:id', to 'patients#show', as: 'patient'

Controller code:

    @patient = Patient.find(params[:id])

View code:

    <%= link_to 'Patient Record', patient_path(@patient) %>

Then, the router will generate the path /patients/17.

- Configuring the Rails Router

All routes are located in config/routes.rb and it will typically have the form:

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

