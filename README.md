# asadicode
class Stack:
    def __init__(self):
        self.stack = []

    def is_empty(self):
        return len(self.stack) == 0

    def push(self, x):
        self.stack.append(x)

    def pop(self):
        if self.is_empty():
            return None
        return self.stack.pop()

    def peek(self):
        if self.is_empty():
            return None
        return self.stack[-1]





class SimpleQueue:
    def __init__(self, size=5):
        self.size = size
        self.queue = [None] * size
        self.front = 0
        self.rear = -1

    def is_empty(self):
        return self.front > self.rear

    def is_full(self):
        return self.rear == self.size - 1

    def enqueue(self, x):
        if self.is_full():
            return
        self.rear += 1
        self.queue[self.rear] = x

    def dequeue(self):
        if self.is_empty():
            return None
        value = self.queue[self.front]
        self.front += 1
        return value





class CircularQueue:
    def __init__(self, size=5):
        self.size = size
        self.queue = [None] * size
        self.front = -1
        self.rear = -1

    def is_empty(self):
        return self.front == -1

    def is_full(self):
        return (self.rear + 1) % self.size == self.front

    def enqueue(self, x):
        if self.is_full():
            return
        if self.is_empty():
            self.front = self.rear = 0
        else:
            self.rear = (self.rear + 1) % self.size
        self.queue[self.rear] = x

    def dequeue(self):
        if self.is_empty():
            return None

        value = self.queue[self.front]
        if self.front == self.rear:
            self.front = self.rear = -1
        else:
            self.front = (self.front + 1) % self.size
        return value
