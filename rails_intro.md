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

    ```
    rails new blog
    ```

blog will be the root folder in a directory structure representing the Ruby on Rails webapp.

The app file will contain the main code (controllers, models, views, helpers, mailers, channels, jobs and assets).

![Base Contents of every Ruby on Rails application](https://d2mxuefqeaa7sj.cloudfront.net/s_B9EA5557BBFC2DFE5DC9010F9057162E0E800B1DE390866B4AB78189AF25BFE8_1536090372226_image.png)



Starting Up

To start the rails server run the command in /blog (directory root of project):

    ```
    bin/rails server
    ```

After this, the page should be online.

Access the page at:
http://localhost:3000

