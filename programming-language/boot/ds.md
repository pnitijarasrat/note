# Data Structure

## Stack

A stack is an abstract data type that serves as a collection of elements. Our stack will have several operations:

- stack.push(item) -> places a new item on top of the stack
- stack.pop() -> removes the top item from the stack and returns it
- stack.peek() -> returns the top item from the stack without modifying the stack
- stack.size() -> returns the number of items in the stack
- O(1)

- Calling a function pushes a call frame onto the runtime stack
- Returning from a function pops the top frame off the stack.

## Queue

A queue is an abstract data type that serves as an ordered collection of elements. A simple queue typically has several operations:

- queue.push(item) -> adds an item to the tail of the queue
- queue.pop() -> removes and returns an item from the head of the queue
- queue.peek() -> returns an item from the head of the queue
- queue.size() -> returns the number of items in the queue
- O(1)

### The Yield Keyword

The yield keyword allows us to return a value from a function with the ability for the caller to resume the called function where it left off, that is, directly after the yield. A function that uses the yield keyword is called a "generator". The values generated from a generator can be iterated over using the in keyword.

```python
def number_generator():
    yield 1
    yield 2
    yield 3

for value in number_generator():
    print(value)
```

## end
