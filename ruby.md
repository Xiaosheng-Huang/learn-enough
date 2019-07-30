## Hello, world!

### Introduction to Ruby

You can check to see if Ruby is already installed by running `ruby -v`

### Ruby in a REPL

```
$ irb
>> puts "hello, world!"	# the same as print "hello, world!\n"
hello, world!
=> nil
```

simplify the irb prompt as above while suppressing some annoying auto-indent behavior.

```
$ atom ~/.irbrc
```

```ruby
IRB.conf[:PROMPT_MODE] = :SIMPLE
IRB.conf[:AUTO_INDENT_MODE] = false
```

### Ruby in a file

```ruby
puts "hello, world!", "how's it going?"
```

### Ruby in a shell script

```ruby
#!/usr/bin/env ruby

puts "hello, world!"
```

### Ruby in a web browser

```
$ gem install sinatra
```

更换RubyGems 镜像

```
$ gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/
```

```
$ touch hello_app.rb
```

```ruby
require 'sinatra'

get '/' do
  'hello, world!'
end
```

```
$ ruby hello_app.rb
```

you can view the app by visiting [localhost:4567](http://localhost:4567/)

#### Deployment

using a hosting platform called [Heroku](https://www.heroku.com/). visit the [installation site](https://toolbelt.heroku.com/) and follow the download instructions there

```
$ heroku --version
```

https://help.github.com/en/articles/connecting-to-github-with-ssh

```
$ heroku login
$ heroku keys:add
```

 create a place on the Heroku servers for the sample app to live

```
$ heroku create
Creating app... done, ⬢ protected-plains-49855
https://protected-plains-49855.herokuapp.com/ | https://git.heroku.com/protected-plains-49855.git
```

```
$ touch config.ru Gemfile
```

```ruby
require './hello_app'
run Sinatra::Application
```

```shell
source 'https://rubygems.org'
gem 'sinatra'
```

*bundle* our gems using [*Bundler*](https://bundler.io/)

```
$ gem install bundler
$ bundle install
$ git add -A
$ git commit -m "Add deployment configuration"
```

```
$ bundle config mirror.https://rubygems.org https://gems.ruby-china.com
```

这样就不需要修改`Gemfile`中的`source`

```
$ git push -u heroku master
```

## Strings

### Concatenation and interpolation

```
>> first_name = "Michael"
>> last_name  = "Hartl"
>> first_name + " " + last_name
=> "Michael Hartl"
>> "#{first_name} is my first name."
```

#### Single-quoted strings

single-quoted strings are what are known as *raw strings*. For example, Ruby won’t interpolate into single-quoted strings

```
>> '\n'
=> "\\n"
```

### Printing

