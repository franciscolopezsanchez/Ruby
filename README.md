## Blocks

- A block is a collection of code to be executed
- Must be attached to a method call
- Alter the execution of a method
- A block is **not** a method/parameter to the method
- Are defined with { } or **do** **end**
- A block can get or update the value of local variables within the block

## Methods vs Blocks

- a method can be called over an over
- a block disappear after it is called
- a block isolates actions away from the method

```ruby
[3,5,7,9].each { |num| puts num ** 2}
```

### yield

- can't include a **return** statement, only implicit return
- it is mandatory to pass a block -> if not, will get an error
- error can be avoided checking for `block_given?` method

```ruby
def pass_control
    puts "this is inside the method!"
    yeld #pass control from the method to the block
    puts "now I'm back inside of the method!"
end

pass_control {puts "Now I'm inside of the block!!!"}
```

## Procs

- A proc is a type of object
- define a proc with `Proc.new <block>`
- Use it with `&`
- can also be called with `.call`

```ruby
cubes = Proc.new { |number| number ** 3 }

a = [1,2,3,4,5]
b = [6,7,8,9,10]
c = [11,12,13,14,15]

a.map(&cubes)
b.map(&cubes)
c.map(&cubes)
```

```ruby
["1","2","3"].map(&:to_i)
```

### methods with procs as parameter

```ruby
def talk_about(name, &myprc)
    puts "let me talk you about #{name}"
    myprc.call(name)
end

good_things = Proc.new do |name|
    puts "#{name} is a genius!"
end

talk_about("pepe", &good_things)
```

## Lambdas

- similar to proc in definition and use
- with the difference that Lambdas will fail if called with more arguments than expected
- other difference is that a `return` within a proc will be the returned value for that method, but a `return` within a lamdba will give the control back to the method

```ruby
some_proc = Proc.new {|name, age| "Your name is #{name} and your age is #{age}."}

puts some_proc.call("Paco", 145)
# Your name is Paco and your age is 145.
puts some_proc.call("Paco")
# Your name is Paco and your age is .

some_lambda = lambda {|name, age| "Your name is #{name} and your age is #{age}."}

puts some_lambda.call("Paco", 145)
# Your name is Paco and your age is 145.
puts some_lambda.call("Paco")
# ERROR: wrong number of arguments
```

## Classes

```ruby
puts "Hello class".class # String
puts 5.class # Fixnum
puts [1,2,3].class # Array
puts Hash.new(0).class # Hash
puts true.class # TrueClass
puts false.class # FalseClass
puts nil.class # NilClass
puts (0..9).class # Range
puts /*.class # Regexp
puts Proc.new {}.class # Proc
puts lambda {}.class # Proc
puts Time.new.class # Time
```

### Classes and superclasses

- The object class itself is another class
- The **superclass** is the class that a current class inherits from.

```ruby
class.superclass
```

```ruby
puts 5.class # Fixnum
puts 5.class.superclass # Integer
puts 5.class.superclass.superclass # Numeric
puts 5.class.superclass.superclass.superclass # Object
puts 5.class.superclass.superclass.superclass.superclass # BasicObject
```

- BasicObject is the class at the top of the hierarchy
- **.ancestors** give a list of all classes and models that an object inherits from in order of inheritance.

```ruby
p 5.class.ancestors
# [Fixnum, Integer, Numeric, Comparable, Object, Kernel, BasicObject]
```

- **.methods** will give back an array of all available methods on that object

- **.instance_variables** will give back an array of all instance variables of an object

- Protected method can be accessed by other objects of the same class family

```ruby
class Car
    def initialize(value)
        @value = value
    end

    def compare_car_with(car)
        self.value > car.value ? true : false
    end

    protected

    def value
        @value
    end
end

civic = Car.new(20000)
fiat = Car.new(30000)

civic.compare_car_with(fiat) # false
puts
```

- Class variables are written with **@@** and they will be accessible by all instances of that class

- Class methods are prefixed with **self.** and they will be accessible by all instances of that class

```ruby
class Bike
    @@maker = "bycicle"
    @@count = 0

    def self.count
        @@count
    end
end

puts Bike.count
# 0
```

## Struct

- A Struct is a convenient way to bundle a number of attributes together, using accessor methods, without having to write an explicit class.

- It is a lightweight representation of data.

```ruby
Customer = Struct.new(:name, :address) do
  def greeting
    "Hello #{name}!"
  end
end

dave = Customer.new("Dave", "123 Main")
dave.name     #=> "Dave"
dave.greeting #=> "Hello Dave!"
```
