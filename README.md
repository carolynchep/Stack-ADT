
# Stack Data Structure 

A stack is a collection og elements similar to a stack of plates, where insertions and deletions are LIFO(Last in first out)

Direct operations include page-visited history in a web browser, undo or redo
sequence in a text editor

Indirect applications include auxiliary data structure used in some algorithms
and an internal component of other data structures


This repository contains an implementation of a generic stack data structure in Python, leveraging type hints and a custom linked list. The stack supports typical operations such as push, pop, top, and checking if the stack is empty.

## Overview
This repository contains an implementation of a generic stack data structure in Python, leveraging type hints and a custom linked list. The stack supports typical operations such as push, pop, top, and checking if the stack is empty.

The `Stack` class uses a linked list to store its elements, providing an example of how to use generics in Python to create a type-safe data structure. The implementation includes custom error handling for stack-specific exceptions.

## Features

- **Push**: Add an element to the top of the stack.
- **Pop**: Remove and return the top element of the stack.
- **Top**: Retrieve the top element without removing it.
- **Is Empty**: Check if the stack is empty.
- **Len**: Get the number of elements in the stack.
- **String Representation**: Get a string representation of the stack.

## Classes

### `EmptyError`

A custom exception class that extends `Exception` to handle stack-specific errors.

### `Stack`

A generic stack class that uses a linked list to manage its elements.

#### Methods

- `__init__`: Initialize an empty stack.
- `__len__`: Return the number of elements in the stack.
- `push`: Add an element to the top of the stack.
- `pop`: Remove and return the top element of the stack. Raise `EmptyError` if the stack is empty.
- `top`: Return the top element of the stack without removing it. Raise `EmptyError` if the stack is empty.
- `is_empty`: Check if the stack is empty.
- `__str__`: Return a string representation of the stack.

## Usage

### Prerequisites

Ensure you have a `LinkedList` class with the following methods:

- `add_right(item: T)`: Add an item to the right end of the list.
- `remove_right() -> T`: Remove and return the item from the right end of the list.
- `_tail`: A reference to the last node in the linked list.

### Example

Here's an example of how to use the stack:

```python
from typing import Generic, TypeVar
from LinkedList import *

T = TypeVar("T")

class EmptyError(Exception):
    def __init__(self, message: str):
        self.message = message

class Stack(Generic[T]):
    __slots__ = ("_data")

    def __init__(self):
        self._data: list[T] = LinkedList()

    def __len__(self) -> int:
        return len(self._data)

    def push(self, item: T) -> None:
        self._data.add_right(item)

    def pop(self) -> T:
        if len(self._data) == 0:
            raise EmptyError('Error in Stack.pop(): stack is empty')
        return self._data.remove_right()

    def top(self) -> T:
        if len(self._data) == 0:
            raise EmptyError('Error in Stack.top(): stack is empty')
        return self._data._tail.data

    def is_empty(self) -> bool:
        return len(self._data) == 0

    def __str__(self) -> str:
        string = "---top---\n"
        current = self._data._tail
        while current is not None:
            string += f"{current.data}\n"
            current = current.prev
        string += "---bottom---"
        return string

def main():
    MyStack = Stack()
    print("Pushing elements onto the stack:")
    MyStack.push(11)
    MyStack.push(33)
    MyStack.push(40)
    MyStack.push(23)
    MyStack.push(10)
    print(MyStack)
    
    print("The length of the stack:")
    print(len(MyStack))
    
    print("The top element of the stack:")
    print(MyStack.top())
    
    print("Popping the top element of the stack:")
    print(MyStack.pop())
    print(MyStack)
    
    print("Checking if the stack is empty:")
    print(MyStack.is_empty())
    
    print("Popping all elements to empty the stack:")
    MyStack.pop()
    MyStack.pop()
    MyStack.pop()
    MyStack.pop()
    print(MyStack)
    
    print("Checking if the stack is empty:")
    print(MyStack.is_empty())

if __name__ == "__main__":
    main()
```
Expected Output
Running the main function should produce the following output:
```
Pushing elements onto the stack:
---top---
10
23
40
33
11
---bottom---
The length of the stack:
5
The top element of the stack:
10
Popping the top element of the stack:
10
---top---
23
40
33
11
---bottom---
Checking if the stack is empty:
False
Popping all elements to empty the stack:
---top---
---bottom---
Checking if the stack is empty:
True
```
