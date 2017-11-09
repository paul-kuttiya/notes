[puts and p](#puts-and-p)  
[string](#string)  
[methods argument](#methods-argument)  
[array](#array)  
[hash](#hash)  
[compound condition](#compound-condition)  
[working with file](#working-with-file)  
[error handling](#error-handling)  
[regex](#regex)  
[gem dish](#gem-dish)  
[metaprogramming](#metaprogramming)  
[working with api][#working-with-api]  


## puts and p  
* puts return `nil` and print out value  
* p call inspect method on object and return the object value  

## string  
* use `split` to split in array  
* use `strip` to clear white space before and after string

## methods argument  
* passing named argument as hash value  
```ruby
def something(arg1:, arg2: "default")
#...
end

# order does not matter can be arg2:, arg1:
something(arg1: "something", arg2: "another")
```

* splat argument  
```ruby
def something(*args)
#...
end

#splat will take all args and passed in as array  
something(1, 2, 3)
```

* optional arguments, passed as any key value, and grab from key  
```ruby
def something(options={})
#...
end

something(key1: "1", key2: "2")
```

## array  
* creat array  
```ruby
x = [1, 2, 3]

Array.new(n) #=> [nil * n]
```

* delete item in array  
```ruby
array.delete(element_value) #=> return deleted value

array.delete_at(index) #=> return deleted value

array.delete_if {|element| ..} #=> return remaining array

#delete empty space in array after split  
array - [" "]
```

* search array with `grep`
```ruby
array = [1, 2, 3, 4, 1]
array.grep(1) #=> [1, 1]
array.grep(/(.*)\.rb/){ $1 } #grep group element end with .rb
```

## hash  
* create hash  
```ruby
hash = {}
hash[:key] = "value"
```

* deleting hash element  
```ruby
hash.delete(:key) #=> return deleted value  
```  

* iterate hash  
```ruby
hash.each_key {|key| p key} #=> iterates all keys

hash.each_value {|value| p value} #=> iterates all values
```

* other useful methods  
```ruby
#swap all value with key in hash
#value will be symbol
hash.invert

#merge hash
hash.merge(hash_2)

#array of nested key, value sub array
hash.to_a

#array of keys
hash.keys

#array of values
hash.values
```

## compound condition
* nested if condition  
```ruby
if something
  if another
    #..
  end
end

#turns to
#needs to be both truthy to execute
if something && another
  #..
end
```

* or condition  
```ruby
#check truthy for the first condition then the following condition
#execute whatever comes truthy first
if something || another
 #...
end
```

## working with file
* create file  
```ruby
# options:
# w => write
# w+ => writing and reading
# r => reading
# r+ => open for update
# a => appending to file  
# a+ => open for reading and appending
File.open("path/filename.ext", "option") do |f| 
  f.write("string_arg")
end

file = File.new("path/filename.ext", "option")
file.puts("string_arg")
file.close
```

* read file  
```ruby
file = File.read("path/file.ext") #=> returns string
```

* delete file  
```ruby
File.delete("path/file.ext")
```

* append file/update file  
```ruby
File.open("path/file.ext", "a") {|f| f.puts("string")}
```

## error handling  
* `begin and rescue`  
```ruby
# other will execute if begin block errors
begin
  something
rescue
  other 
end
```

## regex
* use `=~` to check for regex match  
```ruby
'abC' =~ /c/i #=> returns match index
'abC'.scan(/c/i) #=> returns array of matched
/y/.match('haystack') #=> returns enum #<MatchData "y">
```

## gem dish
* use gem `dish` to convert json to ruby hash obj  
```ruby
require 'dish'

hash = {
  movie: "star wars",
  actor: [
    { age: 22, name: "L" }
  ]
}

hash[:movie] #=> "star wars"
dish = Dish(hash)
dish.movie #=> "star wars"
```

## metaprogramming
* overwrite or create class and methods for ruby  
* creating code that dynamically write code in ruby program  

##working with api
* use gem `httparty` and require in the file  
```ruby
require 'httparty'  

clas SomeApi
  include HTTPARTY
  base_uri = "someapi.com"

  def initialize(site_name, page)
    @options = { query: { site: site_name } }
  end

  def getData(endpoint)
    self.class.get(endpoint, @options)
  end
end

call_api = SomeApi.new("stackoverflow", 1)
call_api.getData("/2.2/users")

#some other methods  
response = HTTPARTY.get('http://api.somewebsite.com/api')

response.body #=> body of the response
response.code #=> 200 ok 
respones.message #=> ok
response.headers.inspect #=> response header
```