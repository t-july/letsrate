# Letsrate Rating Gem

Provides the best way to add rating capabilites to your Rails application with jQuery Raty plugin.

[![Build Status](https://secure.travis-ci.org/muratguzel/letsrate.png)](http://travis-ci.org/muratguzel/letsrate)
[![Dependency Status](https://gemnasium.com/muratguzel/letsrate.png)](https://gemnasium.com/muratguzel/letsrate)
[![Code Climate](https://codeclimate.com/badge.png)](https://codeclimate.com/github/muratguzel/letsrate)

## Repository

Forked from [github.com/muratguzel/letsrate](https://github.com/muratguzel/letsrate)

## Fixes bug on migrations generation, adds STI support and several options
```ruby
read_only: Boolean
star_img: String
```


## Instructions

### Install

Add the letsrate gem into your Gemfile

```ruby
gem 'letsrate'
```

### Generate

```
rails g letsrate User
```

The generator takes one argument which is the name of your existing devise user model UserModelName. This is necessary to bind the user and rating datas.
Also the generator copies necessary files (jquery raty plugin files, star icons and javascripts)

Example:

Suppose you will have a devise user model which name is User. The devise generator and letsrate generator should be like below

```
rails g devise:install
rails g devise user

rails g letsrate user # => user is the model generated by devise
```

This generator will create Rate and RatingCache models and link to your user model.

### Prepare

I suppose you have a car model

```
rails g model car name:string
```

You should add the letsrate_rateable function with its dimensions option. You can add multiple dimensions.

```ruby
class Car < ActiveRecord::Base
  letsrate_rateable "speed", "engine", "price"
end
```

Then you need to add a call letsrate_rater in the user model.

```ruby
class User < ActiveRecord::Base
  letsrate_rater
end
```

### Using

There is a helper method which name is rating_for to add the star links. By default rating_for will display the average rating and accept the
new rating value from authenticated user.

```erb
<%# show.html.erb -> /cars/1 %>

Speed : <%= rating_for @car, "speed" %>
Engine : <%= rating_for @car, "engine" %>
Price : <%= rating_for @car, "price" %>
```

If you need to change the star number, you should use star option like below.

```erb
Speed : <%= rating_for @car, "speed", :star => 10 %>
Speed : <%= rating_for @car, "engine", :star => 7 %>
Speed : <%= rating_for @car, "price" %>
```

You can use the rating_for_user helper method to show the star rating for the user.

```erb
Speed : <%= rating_for_user @car, current_user, "speed", :star => 10 %>
```


## Feedback
If you find bugs please open a ticket at [https://github.com/muratguzel/letsrate/issues](https://github.com/muratguzel/letsrate/issues)
