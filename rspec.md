## RSpec Notes
Summarized content from: [TutorialsPoint](http://www.tutorialspoint.com/rspec/)

[Basic Example](#basic-illustrated-example)  
[Equality and Identity Matchers](#equality-and-identity-matchers)  
[Comparison Matchers](#comparison-matchers)  
[Class and Type Matchers](#class-and-type-matchers)  
[True/False/Nil Matchers](#true-false-nil-matchers)  
[Error Matchers](#error-matchers)  
[Test Doubles (Mocks)](#test-doubles)  
[Stubs](#stubs)  

### Basic Illustrated Example

```ruby
describe HelloWorld do
   context “When testing the HelloWorld class” do

      it "The say_hello method should return 'Hello World'" do
         hw = HelloWorld.new
         message = hw.say_hello
         expect(message).to eq "Hello World!"
      end

   end
end
```

**describe** : defines an "Example Group," or collection of tests
+ Can take a class name and/or string argument
+ Must pass a block argument to describe, containing the examples

**context** : similar to describe; encloses tests of a certain type
+ Can take a class name and/or string argument
+ Not mandatory, but adds more details about the underlying examples

**it** : contains the individual example
+ Can take a class name and/or string argument
+ String argument often uses the word "should" to describe the expected behavior

**expect** : checks that a specific condition has been met
+ Usually read like normal english

**to** : method used with `expect` statements
+ Can also use `not_to` to express the opposite

**eql** : RSpec keyword called a "Matcher"
+ Specifies which type of condition you are testing to be true (or false)

### Additional Keywords

#### Equality and Identity Matchers
Matcher | Description | Example
--- | --- | ---
eq | Passes when actual == expected | expect(actual).to eq expected
eql | Passes when actual.eql?(expected) | expect(actual).to eql expected
be | Passes when actual.equal?(expected) | expect(actual).to be expected
equal | Also passes when actual.equal?(expected) | expect(actual).to equal expected

**Example**
```ruby
describe "An example of the equality Matchers" do

   it "should show how the equality Matchers work" do
      a = "test string"
      b = a

      # The following Expectations will all pass
      expect(a).to eq "test string"
      expect(a).to eql "test string"
      expect(a).to be b
      expect(a).to equal b
   end

end
```

#### Comparison Matchers
Matcher	| Description	| Example
--- | --- | ---
>	| Passes when actual > expected	| expect(actual).to be > expected
>=	| Passes when actual >= expected	| expect(actual).to be >= expected
<	| Passes when actual < expected	| expect(actual).to be < expected
<=	| Passes when actual <= expected	| expect(actual).to be <= expected
be_between inclusive	| Passes when actual is <= min and >= max	| expect(actual).to be_between(min, max).inclusive
be_between exclusive	| Passes when actual is < min and > max	| expect(actual).to be_between(min, max).exclusive
match	| Passes when actual matches a regular expression	| expect(actual).to match(/regex/)

**Example**
```ruby
describe "An example of the comparison Matchers" do

   it "should show how the comparison Matchers work" do
      a = 1
      b = 2
      c = 3		
      d = 'test string'

      # The following Expectations will all pass
      expect(b).to be > a
      expect(a).to be >= a
      expect(a).to be < b
      expect(b).to be <= b
      expect(c).to be_between(1,3).inclusive
      expect(b).to be_between(1,3).exclusive
      expect(d).to match /TEST/i
   end

end
```

#### Class and Type Matchers
Matcher | Description | Example
--- | --- | ---
be_instance_of	| Passes when actual is an instance of the expected class.	| expect(actual).to be_instance_of(Expected)
be_kind_of	| Passes when actual is an instance of the expected class or any of its parent classes.	| expect(actual).to be_kind_of(Expected)
respond_to	| Passes when actual responds to the specified method.	| expect(actual).to respond_to(expected)

**Example**
```ruby
describe "An example of the type/class Matchers" do

   it "should show how the type/class Matchers work" do
      x = 1
      y = 3.14
      z = 'test string'

      # The following Expectations will all pass
      expect(x).to be_instance_of Fixnum
      expect(y).to be_kind_of Numeric
      expect(z).to respond_to(:length)
   end

end
```

#### True False Nil Matchers
Matcher | Description | Example
--- | --- | ---
be true	| Passes when actual == true	| expect(actual).to be true
be false	| Passes when actual == false	| expect(actual).to be false
be_truthy	| Passes when actual is not false or nil	| expect(actual).to be_truthy
be_falsey	| Passes when actual is false or nil	| expect(actual).to be_falsey
be_nil	| Passes when actual is nil	| expect(actual).to be_nil
**Example**
```ruby
describe "An example of the true/false/nil Matchers" do
   it "should show how the true/false/nil Matchers work" do
      x = true
      y = false
      z = nil
      a = "test string"

      # The following Expectations will all pass
      expect(x).to be true
      expect(y).to be false
      expect(a).to be_truthy
      expect(z).to be_falsey
      expect(z).to be_nil
   end
end
```

#### Error Matchers
Matcher | Description | Example
--- | --- | ---
raise_error(ErrorClass)	| Passes when the block raises an error of type ErrorClass.	| expect {block}.to raise_error(ErrorClass)
raise_error("error message")	| Passes when the block raise an error with the message “error message”.	| expect {block}.to raise_error(“error message”)
raise_error(ErrorClass, "error message")	| Passes when the block raises an error of type ErrorClass with the message “error message”	| expect {block}.to raise_error(ErrorClass,“error message”)
**Example**
```ruby
describe "An example of the error Matchers" do
   it "should show how the error Matchers work" do

      # The following Expectations will all pass
      expect { 1/0 }.to raise_error(ZeroDivisionError)
      expect { 1/0 }.to raise_error("divided by 0")
      expect { 1/0 }.to raise_error("divided by 0", ZeroDivisionError)
   end
end
```

#### Test Doubles
+ RSpec Doubles, also known as RSpec Mocks, are objects that can "stand in" for another object.
+ This can come in handy when you have a class of objects, but you want to isolate just the class for testing.
+ Allows you to test your code even when it relies on a class that is undefined or unavailable.

**Example**
```ruby
class ClassRoom
   def initialize(students)
      @students = students
   end

   def list_student_names
      @students.map(&:name).join(',')
   end
end

describe ClassRoom do
   it 'the list_student_names method should work correctly' do
      student1 = double('student')
      student2 = double('student')

      allow(student1).to receive(:name) { 'John Smith'}
      allow(student2).to receive(:name) { 'Jill Smith'}

      cr = ClassRoom.new [student1,student2]
      expect(cr.list_student_names).to eq('John Smith,Jill Smith')
   end
end
```

#### Stubs
+ Often called a Method Stub
+ Special type of method that "stands in" for an existing method, or a method that doesn't exist yet
+ In the above example, the `allow()` method provides the method stubs that we need to test the ClassRoom class
