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
