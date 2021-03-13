# Ruby on Rails Notes - OOP

- [Ruby on Rails Notes - OOP](#ruby-on-rails-notes---oop)
- [OOP](#oop)
- [Authentication system - BCrypt Algorithm](#authentication-system---bcrypt-algorithm)
  - [Authentication POC](#authentication-poc)
  - [Module](#module)


# OOP

Student class example:

```ruby
class Student
  attr_accessor :first_name, :last_name, :email, :username, :password
  @first_name
  @last_name
  @email
  @username
  @password

  def initialize(first_name, last_name, email, username, password)
    @first_name = first_name
    @last_name = last_name
    @email = email
    @username = username
    @password = password
  end

  def set_password(password)
    @password = password
  end

  def print_password
    "The password of the user account \"#{@username}\" is \"#{@password}\""
  end

  def to_s
    "\{\"First Name\": \"#{@first_name}\", \"Last Name\": \"#{@last_name}\", \"Email\": \"#{@email}\", \"Username\": \"#{@username}\""
  end
end

brainyou = Student.new("Brain", "You", "brain.you@localhost", "brain.you", "Password123")
adajohn = Student.new("Ada", "John", "ada.john@localhost", "ada.john", "Password456")

puts brainyou.print_password
brainyou.set_password("ChangeMe!")
puts brainyou.print_password
```

<br/>

----

# Authentication system - BCrypt Algorithm

```ruby
require 'bundler/inline'

gemfile true do
 source 'http://rubygems.org'
 gem 'bcrypt'
end

require 'bcrypt'

# Note each time you run, the hashes will be different
# The only way is to retrieve with the actual plaintext using BCrypt::Password.create("xxxx")
my_password = BCrypt::Password.create("password")
my_password_2 = BCrypt::Password.create("password")
my_password_3 = BCrypt::Password.create("password")
my_password_4 = BCrypt::Password.create("password")
puts my_password, my_password_2, my_password_3, my_password_4

# puts my_password

my_password = BCrypt::Password.new("$2a$12$cpI9bg2jQGL/XGh/LL53IOE6S7lc2xNTwK9O5n5EhMnJhWqRu2/qe")
puts my_password == "password"
# puts my_password.version
# puts my_password.cost
puts my_password == "password1"
# puts my_password == "password"

# For example, if we want to make a "Craete User" function, which saves the user's password in salted-MD5 format:
user_pass = BCrypt::Password.create("thisistheuserpass")
puts user_pass
# => $2a$12$FdHfcydiOOv7VgqU8dLoTOnAC3h3v1K/yDZLC6zWGzEL901UG5ErC

# When the user logins, we can verify the user password:
user_db_pass = BCrypt::Password.new("$2a$12$FdHfcydiOOv7VgqU8dLoTOnAC3h3v1K/yDZLC6zWGzEL901UG5ErC")
user_input = "thisistheuserpass"
puts user_db_pass == user_input
```

<br/>

```ruby
require 'bundler/inline'

gemfile true do
 source 'http://rubygems.org'
 gem 'bcrypt'
end

require 'bcrypt'

def create_hash_digest(password)
  BCrypt::Password.create(password)
end

def verify_hash(password)
  Bcrypt::Password.new(password)
end

def create_user_hash(user_list)
  user_list.each do |user_record|
    user_record[:password] = create_hash_digest(user_record[:password])
  end
  user_list
end

users = [
  { "username": 'ada', "password": 'john' },
  { "username": 'bard', "password": 'support' },
  { "username": 'chris', "password": 'jill' },
  { "username": 'dick', "password": 'ass' }
]

create_user_hash(users)
puts users
```

<br/>

---

## Authentication POC

```ruby
require 'bundler/inline'

gemfile true do
 source 'http://rubygems.org'
 gem 'bcrypt'
end

require 'bcrypt'

def create_hash_digest(password)
  BCrypt::Password.create(password)
end

def verify_hash(password)
  BCrypt::Password.new(password)
end

def create_user_hash(user_list)
  user_list.each do |user_record|
    user_record[:password] = create_hash_digest(user_record[:password])
  end
  user_list
end

def authenticate_user(user, pass, user_list)
  user_list.each do |user_record|
    if user_record[:username] == user && verify_hash(user_record[:password]) == pass
      return user_record
    end
  end
  "Credentials were not correct!"
end

users = [
  { "username": 'ada', "password": 'john' },
  { "username": 'bard', "password": 'support' },
  { "username": 'chris', "password": 'jill' },
  { "username": 'dick', "password": 'ass' }
]

create_user_hash(users)
puts authenticate_user("ada", "john2", users)
```

<br/>

---

## Module

To pack into module:

`crub.rb`:
- Note the `self.` added

```ruby
require 'bundler/inline'

gemfile true do
 source 'http://rubygems.org'
 gem 'bcrypt'
end

module Crud

  require 'bcrypt'

  def self.create_hash_digest(password)
    BCrypt::Password.create(password)
  end

  def self.verify_hash(password)
    BCrypt::Password.new(password)
  end

  def self.create_user_hash(user_list)
    user_list.each do |user_record|
      user_record[:password] = create_hash_digest(user_record[:password])
    end
    user_list
  end

  def self.authenticate_user(user, pass, user_list)
    user_list.each do |user_record|
      if user_record[:username] == user && verify_hash(user_record[:password]) == pass
        return user_record
      end
    end
    "Credentials were not correct!"
  end

end
```

<br/>

`main.rb`:

```ruby
require_relative 'crud'

# $LOAD_PATH << "."
# require 'crud'

users = [
  { "username": 'ada', "password": 'john' },
  { "username": 'bard', "password": 'support' },
  { "username": 'chris', "password": 'jill' },
  { "username": 'dick', "password": 'ass' }
]

Crud.create_user_hash(users)
puts Crud.authenticate_user("ada", "john", users)
```