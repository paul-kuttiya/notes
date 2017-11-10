[float and integer](#float-and-integer)  
[string](#string)  
[array](#array)  
[hash](#hash)  
[symbol](#symbol)  
[iterators](#iterators)  

## float and integer  
* useful methods  
```ruby
-123.abs #=> absolute number 123
200.next #=> return next num 201
1234.1234.round(2) #=> 1234.12
1234.to_i #=> 1234
1234.123.floor # round down
1234.123.ceil # round ceil
```

## string
```ruby
'1' * 5 #=> '11111'
.reverse
.capitalize
.downcase
.upcase
.length
```

## array  
```ruby
.join(', ')
.uniq
.sort
.shift()
.unshift(1)
.empty?
.include?(value)
[1] + [1, 2] 
[1, 2] - [1]
```

## hash  
```ruby
# assign
hash['key'] = "value"

# check and assign if not yet exists
hash['key'] = hash['key'] || "new value"

# find value
hash['key']

# find key
hash.index('value')

# find keys array
hash.keys

# find values array
hash.values

# find length
hash.length

# array key, value sub-array
hash.to_a

hash.has_key?(:k)
hash.has_key?("k")

hash.has_value?("k")
```

## symbol
* symbol will store in the same object memory unlike variable  

## iterators  
* integers/float: `times, upto, downto, step`  
* range: `each, step`  
* string: `each, each_line, each_byte`  
* array: `each, each_index, each_with_index`  
* hash: `each, each_key, each_value, each_pair`  

