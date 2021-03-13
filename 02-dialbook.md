# Ruby on Rails Notes - Dial Book

- [Ruby on Rails Notes - Dial Book](#ruby-on-rails-notes---dial-book)
- [Project: Dial book](#project-dial-book)

# Project: Dial book

Assignment:
```ruby
dial_book = {
  "newyork" => "212",
  "newbrunswick" => "732",
  "edison" => "908",
  "plainsboro" => "609",
  "sanfrancisco" => "301",
  "miami" => "305",
  "paloalto" => "650",
  "evanston" => "847",
  "orlando" => "407",
  "lancaster" => "717"
}
 
# Get city names from the hash
def get_city_names(dial_book)
  puts "Here is the list of cities available:"
  dial_book.each { |k, v| puts k }
  puts
end
 
# Get area code based on given hash and key
def get_area_code(dial_book, key)
  if dial_book.include?(key)
    puts "The area code of #{key} is #{dial_book[key]}"
  else
    puts "The inputted city name does not exist!"
  end
  puts
end
 
# Execution flow
loop do
  option = ''
  while option != 'y' || option != 'n'
    puts "Do you want to look for your city area code? (Y/N)"
    option = gets.chomp.downcase
    break if option == 'y'
    return 0 if option == 'n'
  end
  get_city_names(dial_book)
  puts "Which city's code would you like to get?"
  input_city_name = gets.chomp.downcase.delete(' ')
  get_area_code(dial_book, input_city_name)
end
```

Solution:
```ruby
dial_book = {
  "newyork" => "212",
  "newbrunswick" => "732",
  "edison" => "908",
  "plainsboro" => "609",
  "sanfrancisco" => "301",
  "miami" => "305",
  "paloalto" => "650",
  "evanston" => "847",
  "orlando" => "407",
  "lancaster" => "717"
}
 
def get_city_names(somehash)
  somehash.keys
end
 
def get_area_code(somehash, key)
  somehash[key]
end
 
loop do
  puts "Do you want to lookup an area code based on a city name?(Y/N)"
  answer = gets.chomp.downcase
  break if answer != "y"
  puts "Which city do you want the area code for?"
  puts get_city_names(dial_book)
  puts "Enter your selection"
  prompt = gets.chomp
  if dial_book.include?(prompt)
    puts "The area code for #{prompt} is #{get_area_code(dial_book, prompt)}"
  else
    puts "You entered a city name not in the dictionary"
  end
end
```