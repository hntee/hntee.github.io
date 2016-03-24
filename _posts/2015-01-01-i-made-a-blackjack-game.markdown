---
layout: post
title: "I made a blackjack game"
date: 2014-04-04 09:23:15 +0800
comments: true
categories: 
---

For the last three weeks, I've been learning ruby on [Tealeaf Academy][1]. It is a great site for learning ruby on rails. The instructors are so nice and the course materials are easy to understand. However the first course only covers Sinatra and Rails will be covered in the next course. So I only used Sinatra to develop this app.

<!-- more -->

Here's what I have learnt in these days.

### Basic Ruby Syntax 

 Ruby has a clean and amazing syntax. When I first saw the syntax, it's a **WOW**. For example:
```ruby
3.times do
  puts 'Hi!"
end
```
The code above calls `puts "Hi!"` three times. It is super clear, right?

### Some <abbr title="Object Oriented Programming">OOP</abbr> knowledge

  Everything is an object, and 3 is a `Fixnum`, as what you will get when calling `3.class`. When I call `3.methods`, I can see all the methods that a `Fixnum` object has, which are
```
3.methods
 => [:to_s, :inspect, :-@, :+, :-, :*, :/, :div, :%, :modulo, :divmod, :fdiv, :**, :abs, :magnitude, :==, :===, :<=>, :>, :>=, :<, :<=, :~, :&, :|, :^, :[], :<<, :>>, :to_f, :size, :bit_length, :zero?, :odd?, :even?, :succ, :ord, :integer?, :upto, :downto, :times, :next, :pred, :chr, :to_i, :to_int, :floor, :ceil, :truncate, :round, :gcd, :lcm, :gcdlcm, :numerator, :denominator, :to_r, :rationalize, :singleton_method_added, :coerce, :i, :+@, :eql?, :remainder, :real?, :nonzero?, :step, :quo, :to_c, :real, :imaginary, :imag, :abs2, :arg, :angle, :phase, :rectangular, :rect, :polar, :conjugate, :conj, :between?, :nil?, :=~, :!~, :hash, :class, :singleton_class, :clone, :dup, :taint, :tainted?, :untaint, :untrust, :untrusted?, :trust, :freeze, :frozen?, :methods, :singleton_methods, :protected_methods, :private_methods, :public_methods, :instance_variables, :instance_variable_get, :instance_variable_set, :instance_variable_defined?, :remove_instance_variable, :instance_of?, :kind_of?, :is_a?, :tap, :send, :public_send, :respond_to?, :extend, :display, :method, :public_method, :singleton_method, :define_singleton_method, :object_id, :to_enum, :enum_for, :equal?, :!, :!=, :instance_eval, :instance_exec, :__send__, :__id__]
```
And I can define an object by `class` too.
```ruby
class Dog
  def sit
    puts "Master, I am sitting!"
  end
end
```
I can initialize an instance of `Dog` by calling `dog = Dog.new`. Then I can call `dog.sit` and I will get `Master, I am sitting!` as output.

### HTTP

   A typical HTTP request line is
   
   ` GET /path/to/index.html HTTP/1.1`
   
   - *GET* is a common HTTP method. Other methods include *POST* and *HEAD*.
   - The path is a *URL*.
   - The last part is the HTTP version.

 Typical response lines are
 
   `HTTP/1.0 200 OK`
   `HTTP/1.1 404 Not Found `

  - The status code indicates the general category of the response
  - ** 1xx ** : an informational message only
  - ** 2xx ** : success
  - ** 3xx ** : redirect
  - ** 4xx ** : an error on the client's side
  - ** 5xx ** : an error on the server's side

### Basic Sinatra

 Sinatra is a light-weight web framwork based on Ruby. 
 
 It contains HTTP request and response, 
 so one can build a web application as long as he can implement his logic of the app.
 
 A simple Helloworld page is
```ruby
get '/' do
  'Hello World.'
end
```
After runing the `.rb` file, a `Hello World.` string can be seen on the browser.

 Sinatra also has some built-in features, like `sessions` and `helpers`.
 
 Because HTTP is a stateless protocol, we can't have continuous variables without sending extra information in each HTTP header.
 
 So we need `sessions` to store the information that we want to access during the whole process.
 
 We can define some methods in `Helpers` body so that we can access them in the ruby file.
 
 With these gears, we are able to build a simple web app.
 
### Ajax
 
Ajax is a powerful tool, without which our web world may be directed to a different path.

In this course, I have learned to use Ajax for getting a smoother user experience.
 
The Ajax sample code is as follows:
 
```javascript
$(document).on('click', '#hit input', function() {
  $.ajax({
    type: 'POST',
    url: '/game/player/hit'
    }).done(function(msg) {
      $('#game').replaceWith(msg);
    });
  return false;
});
```

It selects the `input` element, whose ancestor's id is `hit` and then bind a function on its  `onclick` event.
 
The `ajax` function is implemented in `jQuery`.
 
My final project is deployed onto [Heroku][2] and code can be viewed on [my Github Repo][3].
 
 

[1]: http://gotealeaf.com
[2]: http://blackjack-t.herokuapp.com
[3]: https://github.com/hntee/Blackjack-Webapp
