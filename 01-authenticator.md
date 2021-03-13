# Ruby on Rails Notes - Authenticator

- [Ruby on Rails Notes - Authenticator](#ruby-on-rails-notes---authenticator)
- [Project: Authenticator](#project-authenticator)

# Project: Authenticator

Homework:

```ruby
def init
  puts 'Welcome to Authenticator'
  25.times { print '-' }
  puts
end

def main
  users = [
    { "username": 'ada', "password": 'john' },
    { "username": 'bard', "password": 'support' },
    { "username": 'chris', "password": 'jill' },
    { "username": 'dick', "password": 'ass' }
  ]
  out = {}

  puts 'Please enter a username: '
  i_user = gets.chomp
  puts 'Please enter a password: '
  i_pass = gets.chomp

  users.each { |d| out = d if i_user == d[:username] && i_pass == d[:password] }
  if out.length != 0
    puts out
  else
    puts 'Wrong password!'
  end
end

init
time = 0
while time < 3
  time += 1
  main
  puts 'Enter q to quit or any other key to continue:'
  option = gets.chomp
  break if option == 'q'
end

puts 'You have exceeded the number of attempts!' if time >= 3

puts
```

Solution:
```ruby
puts 'Welcome to Authenticator'
25.times { print '-' }
puts

users = [
  { "username": 'ada', "password": 'john' },
  { "username": 'bard', "password": 'support' },
  { "username": 'chris', "password": 'jill' },
  { "username": 'dick', "password": 'ass' }
]

def auth_user(username, password, users)
  users.each do |user|
    if user[:username] == username && user[:password] == password
      return user
    end
  end
  return "Credentials were not correct"
end

attempt = 0
while attempt < 3
  # Get input from the user
  print "Username: "
  username = gets.chomp
  print "Password: "
  password = gets.chomp

  # Compare db
  puts auth_user(username, password, users)

  # Option to quit or continue
  puts "Press n to quit or any other key to continue: "
  input = gets.chomp.downcase
  break if input == "n"

  attempt += 1
end
puts "You have exceeded the number of attempts" if attempt >= 3
```

<br/>
