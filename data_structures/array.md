# Arrays

Arrays are the simplest and most common data structure. The provide easy access of the elements by index. Elements' values are placed in order and accessed by their index from 0 to the length of the array - 1 (since the first element is stored at index 0). An array is a continuous block of memory.

An array can be a list of integers, strings, or mixed data structures. An array is very easy to add to, remove from, and perform simple methods on.

- Examples of arrays
```ruby
integer_array = [1, 2, 3, 4, 5]
sting_array = ['hello', 'world']
mixed_data_array = [1, 'hello', {key => value}, [1, 2]]
```

- Accessing elements in an array
```ruby
numbers = [1, 2, 3, 4, 5]
first_number = numbers[0] # 1
last_number = numbers[-1] # 5
```

- Add elements to an array
```ruby
numbers << 6    # Will append 6 to the end of the array
numbers.push(7) # another way to add to the end of an array
```

- Remove elements from an array
```ruby
numbers.pop   # Removes and returns the last element (7)
numbers.shift # Removes and returns the first element (1)
```

- Modify elements in an array
```ruby
numbers[0] = 10 # Change the first element to 10
```

- Check the size of an array
```ruby
puts number.size # Outputs the current size of the array
```

- Iterate over an array
```ruby
numbers.each do |num|
  puts num * 2     # Prints each number doubled
end
```

- Filter elements in an array
```ruby
even_numbers = numbers.select { |num| num.even? }
```

- Transformm the elements in an array into a new array
```ruby
squared_numbers = numbers.map { |num| num ** 2 }
```

### Exmple Usage

```ruby
numbers = [1, 2, 3, 4, 5]
numbers << 6       # [1, 2, 3, 4, 5, 6]
numbers.pop        # [1, 2, 3, 4, 5] (returns 6)
numbers.shift      # [2, 3, 4, 5] (returns 1)
numbers[0] = 10    # [10, 3, 4, 5]
```

