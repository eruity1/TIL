# Stacks

A stack is a linear data structure that follows the LIFO (Last In, First Out) rule. The last element added to a stack will be the first element you remove from it, think of it as a pile of plates, you wouldn't remove the bottom one.

A stack uses two main methods to manipulate data:

1. `push` adds a new piece of data in the stack. Time Complexity: `O(1)`

```ruby
def push(element)
  @stack << element
end
```

2. `pop` removes the last piece of data added. Time Complexity: `O(1)`

```ruby
def pop
  @stack.pop
end
```

Other useful methods that are typically used in a stack:

- `peek` will return the top element if the stack without removing it. Time Complexity: `O(1)`

```ruby
def peek
  @stack.last
end
```

- `is_empty?` will return a boolean if the stack is empty or not

```ruby
def is_empty?
  @stack.empty?
end
```

- `display` will print the stack

```ruby
def display
  puts @stack.inspect
end
```

### Exmple Usage

```ruby
stack = Stack.new
stack.push(1)
stack.push(2)
stack.push(3)
stack.dsiplay # [1, 2, 3]
puts stack.peak # 3
stack.pop
stack.display # [1, 2]
puts stack.is_empty? # false
```
