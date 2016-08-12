## Ruby Notes
Notes taken during [CodeCademy](https://www.codecademy.com/learn/ruby) tutorial

[Basics](#basics)  
[Methods](#methods)  
[Conditionals](#conditionals)  
[Classes](#classes)  
[Modules](#modules)  
[Mixins](#mixins)

### Basics

#### Variables
- **Global Variables** are accessible from everywhere
  + Indicated by $ (e.g., `$total`)
  + Note that the '$' actually makes the variable global (not just a convention)
- **Class Variables** are accessible in certain classes
  + Indicated by @@ (eg., `@@total`)
  + Only one copy of a class variable shared by all instances of a class
- **Instance Variables** are accessible in a specific instance of a class
  + Indicated by @ (e.g., `@total`)

```ruby
cat = "Hamlet"  # variable assignment. so simple!

# conditional assignment
cat ||= "Luna"  # only assigns if previously unassigned

# string interpolation
"here's how you add a #{variable} to a string"

# use underscores for large numeric literals (ruby ignores them)
balance = 1_000_000
# => 1000000
```
#### Constants
+ The convention when defining a constant is to use ALL_CAPS with words separated by underscores  

```ruby
PI = 3.141592653589793
```
#### User Input
```ruby
gets  # this will include a newline after the response
gets.chomp  # this will not include a newline
```
#### Printing
```ruby
print # will print without newline
puts  # will print with newline
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
:symbol.to_s    # converts to string
```
#### Arrays
```ruby
stuff = []    # create array

# appending arrays
stuff.push("string")  # adds "string" to the end of array
stuff << "string" # concatenation operator "the shovel"
```
#### Hash
```ruby
pets = Hash.new     # create hash
pets = {}           # create hash
pets = {            # create old style hash
  :Hamlet => "cat",
  :Luna => "cat"
}
pets = {          # create new style hash
  Hamlet: "cat",
  Luna: "cat"
}
pets["Hamlet"] = "cat"      # add to hash
my_hash = Hash.new("oops")  # create hash with default value
```
#### Blocks
```ruby
# blocks are a chunk of code to be run
# indicated by {} or do/end
# can be combined with methods like each
[1, 2, 3].each { |num| puts num }

# create methods that accept blocks with yield!
def example
	puts "first part"
	yield
end
example { puts "block part" } # puts both strings

# more complicated version
def example
	puts "first part"
	yield("example")
end
example { |x| puts "#{x} block part" }
# returns both, but second one is "example block part"
```
#### Procs
```ruby
# procs are like blocks you can save!
# '&' converts proc into a block
multiples_of_5 = Proc.new do |n|
  n % 5 == 0
end
(1..50).to_a.select(&multiples_of_5) # call with &
# ==> [5, 10, 15, 20, 25, 30, 35, 40, 45, 50]

# you can call a proc by itself using call
hi = Proc.new {puts "Hello!"}
hi.call
# ==> Hello!

# convert symbols to procs using &
strings = ["1", "2", "3"]
nums = strings.map(&:to_i)
# ==> [1, 2, 3]
```
#### Lambdas
```ruby
# differences from proc:
# 1. lambda will throw an error if you pass it the wrong number of arguments,
# whereas a proc will ignore unexpected arguments and assign nil to any missing
# 2. when a lambda returns, it passes control back to the calling method,
# whereas a proc returns immediately, without going back to the calling method

# similarities to proc
# use & to covert to block and use call to call

# define lambdas using the following:
lambda { |param| block }
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
example_array.each { |i|  # iterates over each item in array
  puts i
}
example_hash.each_key { |k| # iterates over each key
  puts k
}
example_hash.each_value { |v| # iterates over each value
  puts v
}
```
#### collect & map
```ruby
# collect is like each, but it will save returned values
# note that this is the same as map
nums.collect { |n| n * 2 } # will make temporary copy * 2
nums.collect! { |n| n * 2 } # will actually update array

# or use to make a new version of an array
double_nums = nums.collect { |n| n * 2 }
```
#### times
```ruby
20.times { puts "I love repetition!" }
# Prints string 20 times
```
#### upto & downto
```ruby
95.upto(100) { |num| print num, " " }
# ==> 95 96 97 98 99 100
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
if condition
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
unless garbage
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
### Classes
+ **definition**: a class is a way of organizing and producing objects with similar attributes and methods
+ **conventions**: class names start with capital letter and use CamelCase  

#### Create a class!
```ruby
class Person
  # make it werk here!
  def initialize(name, age)
    @name = name  # use @ to signify an instance variable
    @age = age
  end
end

me = Person.new("Alix",25)  # create new instance of class

# Shortcut
class Person; end # End a Ruby statement without a new line by using a semicolon
```
#### Inheritance
+ Note: Ruby disallows multiple inheritance  

```ruby
class Parent
  def say_stuff
    puts "stuff!"
  end
end

class Child < Parent
  # the child class will inherit everything from the parent class
  # even if you don't put anything in here!

  def say_stuff   # explicitly create the same method again to overwrite
    puts "other stuff!"

    # use the super keyword to access what's inside the parent's method
    super() # pass arguments if the parent's methods take arguments
  end
end
```
#### Class Methods
+ Class Methods belong to the class itself, as opposed to instance methods, which work on a particular instance/object.  

```ruby
class Tester
  def Tester.hello
    puts "Hey, it's me - the tester!"
  end
end
```
#### Public vs. Private Methods
+ **Public Methods** can be called inside and outside of the object where they are defined  
+ **Private Methods** cannot be called outside of the object where they are defined  
+ You can explicitly define methods as public and private  
+ If you do not specify, methods will default to public  

```ruby
class Person
  def initialize(name)
    @name = name
  end

  public    # this is the default
  def introduction
    puts "Hi I'm #{name}!"
  end

  private   # this method will not work when called outside the function
  def credit_card_number
    @account_number = 253108623
    puts "Here, have my credit card number! #{@account_number}"
  end
end
```
#### attr  
+ Use `attr` to read and write instance variables outside the class  
+ Think of this like using `public` and `private` for methods  
+ Use `attr_reader` to read, `attr_writer` to write, or `attr_accessor` for both  

```ruby
class Person
  attr_writer :name
  def initialize(name)
    @name = name
  end
end
```
### Modules
+ Can't create instances and can't have subclasses  
+ Convention is to name with CapitalizedCamelCase like Classes  
+ One of the main purposes is to separate methods and constants into named spaces (*namespacing*)

```ruby
module Circle
  PI = 3.141592653589793
end

Cirle::PI # tells ruby to look specifically in Circle for PI
# the :: is called the scope resolution operator
```
#### require
```ruby
require 'date' # bring in modules using require

puts Date.today
```
#### include
+ Use a module's methods at the instance level
```ruby
class Angle
  include Math
  attr_accessor :radians

  def initialize(radians)
    @radians = radians
  end

  def cosine
    cos(@radians) # can use constants and method without prepending method name
  end
end
```
### Mixins
+ Include modules in class definition to avoid repeating code (DRY!)
+ A way of using multiple inheritance, since ruby doesn't allow it
```ruby
module Firsties
	def methodator
		puts "This is the first method!"
	end
end

module Secondsies
	def methodontist
		puts "Woah a second method?"
	end
end

class Combinatro
	include Firsties
	include Secondsies
end

example = Combinatro.new

example.methodator
example.methodontist

# => This is the first method!
# => Woah a second method?
```
