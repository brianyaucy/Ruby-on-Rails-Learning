# Ruby on Rails Notes - OOP

- [Ruby on Rails Notes - OOP](#ruby-on-rails-notes---oop)
- [OOP](#oop)


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