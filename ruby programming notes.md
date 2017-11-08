[puts and p](#puts-and-p)  
[string](#string)  
[methods argument](#methods-argument)  
[array](#array)  
[hash](#hash)  
[compound condition](#compound-condition)   

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