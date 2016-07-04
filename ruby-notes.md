## Ruby Notes

[Basics](#basics)  
[Methods](#methods)  
[Conditionals](#conditionals)  

### Basics

#### Variables
```ruby
cat = "Hamlet"  # variable assignment. so simple!

# conditional assignment
cat ||= "Luna"  # only assigns if previously unassigned

# string interpolation
"here's how you add a #{variable} to a string"
```
#### User Input
```ruby
gets        # this will include a newline after the response
gets.chomp  # this will not include a newline
```
#### Printing
```ruby
print   # will print without newline
puts    # will print with newline
```
#### Arithmetic
```ruby
2 * 2     # multiplication
2 / 2     # division
2 + 2     # addition
2 - 2     # subtraction
2 % 2     # remainder
2 ** 2    # exponent
x.abs     # absolute value of variable x
rand      # random number between 0 and 1
rand(11)  # random number from 1 to 10
```
#### Comparison Operators
```ruby
==  # equal
!=  # not equal
>   # greater than
<   # less than
>=  # greater than or equal to
<=  # less than or equal to
&&  # and - true if both are true
||  # or - true if one is true
```
#### Symbols
```ruby
# primarily used as hash keys or for referencing method names
# immutable - can't be changed once created
# only one copy of the symbol exists at a time
# symbols as keys are faster than strings as keys
"string".to_sym   # converts to symbol
"string".intern   # converts to symbol
:symbol.to_s      # converts to string
```
#### Arrays
```ruby
stuff = []    # create array

# appending arrays
stuff.push("string")    # adds "string" to the end of array
stuff << "string"   # concatenation operator "the shovel"
```
#### Hash
```ruby
pets = Hash.new             # create hash
pets = {}                   # create hash
pets = {                    # create old style hash
  :Hamlet => "cat",
  :Luna => "cat"
}
pets = {                    # create new style hash
  Hamlet: "cat",
  Luna: "cat"
}
pets["Hamlet"] = "cat"      # add to hash
my_hash = Hash.new("oops")  # create hash with default value
```
### Methods

#### Type Conversions
```ruby
variable.to_f   # converts to float
variable.to_i   # converts to integer
variable.to_s   # converts to string
```
#### String Methods
```ruby
"string".reverse      # reverses string
"string".length       # returns length of string
"string".upcase       # upper case
"string".downcase     # lower case
"string".swapcase     # reverses capitalization
"string".capitalize   # capitalizes first character
```
#### String Alignment
```ruby
lineWidth = 50              # example line width for below
"string".center(lineWidth)  # centers string in line width
"string".ljust(lineWidth)   # aligns string to left in line width
"string".rjust(lineWidth)   # aligns string to right in line width
```
#### each
```ruby
example_array.each { |i|      # iterates over each item in array
  puts i
}
example_hash.each_key { |k|   # iterates over each key
  puts k
}
example_hash.each_value { |v| # iterates over each value
  puts v
}
```
#### times
```ruby
20.times { puts "I love repetition!" }
# Prints string 20 times
```
#### upto & downto
```ruby
95.upto(100) { |num| print num, " " }
# Prints 95 96 97 98 99 100
```
#### respond_to?
```ruby
# check if a method will work
[1, 2, 3].respond_to?(:push)
# returns true, because you can push array to an object
```
#### select
```ruby
sample = {alix: 100, hilary: 40, hamlet: 120}
sample.select {|name, points| points > 50}
# ==> {:alix=>100, :hamlet=>120}
winners = sample.select {|name, points| points > 50}
# creates new hash with results of select method
```
### Conditionals
#### if statements
```ruby
if condition                # conditional
  # do something!
elsif condition
  # something else!
else
  # leftover thing
end

puts "It's true!" if true   # prettier conditional

# ternary conditional expression
puts 3 < 4 ? "3 is less than 4!" : "3 is not less than 4."
```
#### unless
```ruby
unless garbage                      # unless
  # do the thing
end

puts "Not garbage!" unless garbage  # prettier unless
```
#### case
```ruby
puts "What's your favorite food?"
food = gets.chomp
case food
when "Pizza"
  puts "Excellent Choice!"
when "Nachos"
  puts "Splendiferous!"
when "Chicken Nugs"
  puts "You're a genius!"
else
  puts "Eew y?"
end
```
#### Notes on true / false / nil
```ruby
# false and nil are the only two non-true values in ruby
if "bacon" # if statement will run, because it is true

# if a key doesn't exist in a hash, it will
# return nil instead of an error
```
