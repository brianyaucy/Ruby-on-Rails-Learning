# Ruby on Rails Notes

- [Ruby on Rails Notes](#ruby-on-rails-notes)
- [Basic](#basic)
- [If else](#if-else)
- [Array](#array)
- [Hash (Dictionary)](#hash-dictionary)

# Basic

```ruby
def ask
  puts 'Enter your first name:'
  first_name = gets.chomp
  puts 'Enter your last name:'
  last_name = gets.chomp
  puts "Your full name is #{first_name} #{last_name}"
  puts "Your full name reverse is #{last_name.reverse!} #{first_name.reverse!}"
  puts "Your name has #{first_name.length + last_name.length} characters in it"
end

def multiply(n1, n2)
  n1.to_f * n2.to_f
end

def add(n1, n2)
  n1.to_f + n2.to_f
end

def sub(n1, n2)
  n1.to_f - n2.to_f
end

def div(n1, n2)
  n1.to_f / n2.to_f
end

def mod(n1, n2)
  n1.to_f % n2.to_f
end

def number()
  puts 'Simple calculator'
  25.times {print "-"}
  puts
  puts "Enter the first number: "
  num_1 = (gets.chomp).to_i
  puts "Enter the second number: "
  num_2 = (gets.chomp).to_i
  puts "#{num_1} * #{num_2} = #{multiply(num_1, num_2)}"
  puts "#{num_1} - #{num_2} = #{sub(num_1, num_2)}"
  puts "#{num_1} + #{num_2} = #{add(num_1, num_2)}"
  puts "#{num_1} / #{num_2} = #{div(num_1, num_2)}"
  puts "#{num_1} mod #{num_2} = #{mod(num_1, num_2)}"
end

number()
```


# If else

```ruby
def op_cal
  puts 'What do you want to do?'
  puts '(1 = add, 2 = substract, 3 = multiply)'
  option = gets.chomp.to_i

  if option != 1 && option != 2 && option != 3
    puts 'Bastard!'
    return 0
  else
    puts 'Enter the 1st number: '
    num_1 = gets.chomp.to_f
    puts 'Enter the 2nd number: '
    num_2 = gets.chomp.to_f
  end

  if option == 1
    print "#{num_1} + #{num_2} = #{num_1 + num_2}"
  elsif option == 2
    print "#{num_1} - #{num_2} = #{num_1 - num_2}"
  elsif option == 3
    print "#{num_1} * #{num_2} = #{num_1 * num_2}"
  end
end

op_cal

```

# Array

```ruby
def mutate
  a = (1..9).to_a
  p a
  p a.reverse
  p a.reverse!
  p a
  p ("a".."z").to_a
  p ("a".."z").to_a.shuffle
end

def add_element
  a = ("a".."z").to_a

  # add to last
  p a
  a = a.append("last item")
  p a

  # add to first
  a = a.unshift("first item")
  p a

  # dedup
  a << "last item"
  p a
  a.uniq!
  p a

  # Check empty
  p a.empty?

  # Check exist
  p a.include?("first item")

  # array -> string
  p a.join
  p a.join("-")
  b = a.join("-")
  p b.split("-")

  # String -> array
  w = %w(Hello world Ruby is on9)
  p w

  # Dictation
  for i in w
    p i
  end

  10.times { print "-" }
  puts

  w.each {|item| p item}

  10.times { print "-" }
  puts

  # Print odd only
  z = (1..100).to_a.shuffle
  p z, "Length of array: #{z.length}"
  z = z.select {|num| num.odd?}
  p z, "Length of array: #{z.length}"
end

add_element()
```

# Hash (Dictionary)

```ruby
# Hash

def simple
  h = { 'a' => 1, 'b' => 2, 'c' => 3 }
  p h
  p h['a']

  guy = { 'first_name' => 'brain', 'last_name' => 'you' }
  p guy
  p guy['first_name'], guy['last_name']
end

def another_simple
  h = { a: 1, b: 2, c: 3 }
  p h
  p h[:a]

  h.each {|k,v| puts "Class: #{k} is a #{k.class} | #{v} is an #{v.class}"}
  puts

  h = { 'a' => 1, 'b' => 2, 'c' => 3 }
  p h
  h.each {|k,v| puts "Class: #{k} is a #{k.class} | #{v} is an #{v.class}"}

  puts

  # Add element
  h = { a: 1, b: 2, c: 3 }
  p h
  h[:d] = 4
  p h
  h[:c] = 3.5
  p h

  # Conditional
  h[:e] = "First string"
  h[:f] = "2nd string"
  p h.select { |k,v| v.is_a?(String)}
  puts

  # Conditional Remove
  p h
  h.each { |k,v| h.delete(k) if !v.is_a?(Integer)} # Get integer only
  p h
end

another_simple
```

<br/>

