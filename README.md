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
class Queue:
    def __init__(self, size=10):
        self.size = size
        self.arr = [None] * size
        self.front = 0
        self.rear = -1

    def enqueue(self, x):
        if self.rear == self.size - 1:
            print("Queue Overflow")
            return
        self.rear += 1
        self.arr[self.rear] = x

    def dequeue(self):
        if self.front > self.rear:
            print("Queue Underflow")
            return
        self.front += 1

    # ✅ متد حل مشکل صف ساده
    def fix_queue(self):
        j = 0
        for i in range(self.front, self.rear + 1):
            self.arr[j] = self.arr[i]
            j += 1

        self.rear = self.rear - self.front
        self.front = 0

    def display(self):
        if self.front > self.rear:
            print("Queue is empty")
            return
        for i in range(self.front, self.rear + 1):
            print(self.arr[i], end=" ")
        print()







q = Queue(5)

q.enqueue(10)
q.enqueue(20)
q.enqueue(30)
q.dequeue()
q.dequeue()

q.enqueue(40)
q.enqueue(50)   # اینجا ممکنه مشکل ایجاد بشه

q.fix_queue()   # ✅ حل مشکل

q.enqueue(60)
q.display()







class Stack:
    def __init__(self):
        self.items = []

    def push(self, x):
        self.items.append(x)

    def pop(self):
        if self.is_empty():
            print("Stack Underflow")
            return None
        return self.items.pop()

    def is_empty(self):
        return len(self.items) == 0

    def display(self):
        print(self.items)

    # ✅ متد اولویت‌بندی زوج و فرد
    def prioritize_even_odd(self):
        even = []
        odd = []

        # تخلیه پشته
        while not self.is_empty():
            x = self.pop()
            if x % 2 == 0:
                even.append(x)
            else:
                odd.append(x)

        # بازگرداندن: اول زوج‌ها، بعد فردها
        for x in reversed(odd):
            self.push(x)

        for x in reversed(even):
            self.push(x)






s = Stack()
s.push(1)
s.push(2)
s.push(3)
s.push(4)
s.push(5)

s.prioritize_even_odd()
s.display()



















class Stack:
    def __init__(self, size=5):
        self.size = size
        self.is_static = True   # شروع به صورت استاتیک
        self.stack = [None] * size
        self.top = -1

    def push(self, x):
        if self.is_static:
            if self.top == self.size - 1:
                print("Stack Overflow (Static)")
                return
            self.top += 1
            self.stack[self.top] = x
        else:
            self.stack.append(x)

    def pop(self):
        if self.is_empty():
            print("Stack Underflow")
            return None

        if self.is_static:
            x = self.stack[self.top]
            self.top -= 1
            return x
        else:
            return self.stack.pop()

    def is_empty(self):
        if self.is_static:
            return self.top == -1
        return len(self.stack) == 0

    # ✅ متد تغییر نوع پشته
    def toggle_stack_type(self):
        if self.is_static:
            # استاتیک → داینامیک
            new_stack = []
            for i in range(self.top + 1):
                new_stack.append(self.stack[i])

            self.stack = new_stack
            self.is_static = False
            print("Stack changed to Dynamic")

        else:
            # داینامیک → استاتیک
            new_stack = [None] * self.size
            n = min(len(self.stack), self.size)

            for i in range(n):
                new_stack[i] = self.stack[i]

            self.stack = new_stack
            self.top = n - 1
            self.is_static = True
            print("Stack changed to Static")

    def display(self):
        if self.is_static:
            print(self.stack[:self.top + 1])
        else:
            print(self.stack)







s = Stack(5)

s.push(10)
s.push(20)
s.push(30)

s.toggle_stack_type()  # استاتیک → داینامیک
s.push(40)
s.push(50)
s.push(60)

s.toggle_stack_type()  # داینامیک → استاتیک
s.display()

















class CircularQueue:
    def __init__(self, size=10):
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
            print("Queue is Full")
            return

        if self.is_empty():
            self.front = 0
            self.rear = 0
        else:
            self.rear = (self.rear + 1) % self.size

        self.queue[self.rear] = x

    def dequeue(self):
        if self.is_empty():
            print("Queue is Empty")
            return None

        x = self.queue[self.front]

        if self.front == self.rear:
            self.front = -1
            self.rear = -1
        else:
            self.front = (self.front + 1) % self.size

        return x

    # ✅ متد گزارش ۵ لاگ آخر
    def last_five_logs(self):
        if self.is_empty():
            print("No logs available")
            return

        count = self.count_elements()
        logs_to_show = min(5, count)

        result = []
        index = self.rear

        for _ in range(logs_to_show):
            result.append(self.queue[index])
            index = (index - 1 + self.size) % self.size

        result.reverse()  # ترتیب صحیح
        print("Last logs:", result)

    def count_elements(self):
        if self.rear >= self.front:
            return self.rear - self.front + 1
        return self.size - self.front + self.rear + 1





cq = CircularQueue(7)

cq.enqueue("Log1")
cq.enqueue("Log2")
cq.enqueue("Log3")
cq.enqueue("Log4")
cq.enqueue("Log5")
cq.enqueue("Log6")
cq.enqueue("Log7")

cq.last_five_logs()

















from datetime import datetime

class CircularQueue:
    def __init__(self, size=5):
        self.size = size
        self.queue = [None] * size
        self.front = -1
        self.rear = -1

        # ذخیره ۵ زمان آخر پر شدن صف
        self.full_times = []

    def is_full(self):
        return (self.rear + 1) % self.size == self.front

    def is_empty(self):
        return self.front == -1

    def enqueue(self, x):
        if self.is_full():
            self._save_full_time()
            return

        if self.is_empty():
            self.front = self.rear = 0
        else:
            self.rear = (self.rear + 1) % self.size

        self.queue[self.rear] = x

    # ✅ ثبت زمان پر شدن صف
    def _save_full_time(self):
        time_now = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
        self.full_times.append(time_now)

        if len(self.full_times) > 5:
            self.full_times.pop(0)

    # ✅ متد گزارش ۵ زمان آخر پر شدن صف
    def report_full_times(self):
        if not self.full_times:
            print("Queue has never been full")
            return

        for t in self.full_times:
            print(t)


























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

    def get_valid_elements(self):
        if self.is_empty():
            return []

        result = []
        i = self.front
        while True:
            result.append(self.queue[i])
            if i == self.rear:
                break
            i = (i + 1) % self.size
        return result







def create_and_transfer():
    queues = []
    stacks = []

    # ایجاد ۱۰۰۰ صف حلقوی
    for i in range(1000):
        q = CircularQueue()
        for j in range(3):       # داده نمونه
            q.enqueue(i * 10 + j)
        queues.append(q)

    # ایجاد ۱۰۰۰ پشته
    for _ in range(1000):
        stacks.append(Stack())

    # انتقال داده‌های معتبر صف‌ها به‌صورت معکوس به پشته‌ها
    for i in range(1000):
        data = queues[i].get_valid_elements()
        for x in reversed(data):
            stacks[i].push(x)

    return queues, stacks















# ---------- Circular Queue ----------
class CircularQueue:
    def __init__(self, size=10):
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
            return False
        if self.is_empty():
            self.front = self.rear = 0
        else:
            self.rear = (self.rear + 1) % self.size
        self.queue[self.rear] = x
        return True

    def dequeue(self):
        if self.is_empty():
            return None
        value = self.queue[self.front]
        if self.front == self.rear:
            self.front = self.rear = -1
        else:
            self.front = (self.front + 1) % self.size
        return value


# ---------- Stack ----------
class Stack:
    def __init__(self):
        self.stack = []

    def push(self, x):
        self.stack.append(x)

    def pop(self):
        if not self.stack:
            return None
        return self.stack.pop()

    def stack_empty(self):
        return len(self.stack) == 0


# ---------- Priority Circular Queue ----------
class PriorityCircularQueue(CircularQueue, Stack):

    def __init__(self, size=10):
        CircularQueue.__init__(self, size)
        Stack.__init__(self)

    # 1
    def enqueue_with_priority(self, x):
        if self.is_full():
            return False
        data = self.get_elements()
        data.append(x)
        data.sort(reverse=True)
        self.clear()
        for item in data:
            self.enqueue(item)
        return True

    # 2
    def dequeue_priority(self):
        return self.dequeue()

    # 3
    def peek(self):
        if self.is_empty():
            return None
        return self.queue[self.front]

    # 4
    def get_elements(self):
        if self.is_empty():
            return []
        result = []
        i = self.front
        while True:
            result.append(self.queue[i])
            if i == self.rear:
                break
            i = (i + 1) % self.size
        return result

    # 5
    def clear(self):
        self.front = self.rear = -1
        self.queue = [None] * self.size

    # 6
    def count(self):
        return len(self.get_elements())

    # 7
    def contains(self, x):
        return x in self.get_elements()

    # 8
    def reverse(self):
        for x in self.get_elements():
            self.push(x)
        self.clear()
        while not self.stack_empty():
            self.enqueue(self.pop())

    # 9
    def move_to_stack(self):
        for x in self.get_elements():
            self.push(x)

    # 10
    def display(self):
        print(self.get_elements())
















class CircularQueue:
    def __init__(self, size=10):
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

    # ✅ متد تبدیل صف حلقوی به صف ساده
    def to_simple_queue(self):
        if self.is_empty():
            return

        new_queue = [None] * self.size
        i = self.front
        idx = 0

        while True:
            new_queue[idx] = self.queue[i]
            if i == self.rear:
                break
            i = (i + 1) % self.size
            idx += 1

        self.queue = new_queue
        self.front = 0
        self.rear = idx












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

    # ✅ متد اولویت‌دار کردن پشته
    def prioritize(self):
        temp = []
        while not self.is_empty():
            temp.append(self.pop())

        temp.sort(reverse=True)   # اولویت بالاتر = عدد بزرگ‌تر

        for x in temp:
            self.push(x)






s = Stack()
s.push(3)
s.push(1)
s.push(5)
s.push(2)

s.prioritize()
print(s.stack)   # [1, 2, 3, 5]  ← 5 بالای پشته















class AdvancedStack:
    # 1
    def __init__(self):
        self.stack = []

    # 2
    def is_empty(self):
        return len(self.stack) == 0

    # 3
    def size(self):
        return len(self.stack)

    # 4
    def push(self, x):
        self.stack.append(x)

    # 5
    def pop(self):
        if self.is_empty():
            return None
        return self.stack.pop()

    # 6
    def peek(self):
        if self.is_empty():
            return None
        return self.stack[-1]

    # 7
    def clear(self):
        self.stack.clear()

    # 8
    def contains(self, x):
        return x in self.stack

    # 9
    def reverse(self):
        self.stack.reverse()

    # 10
    def copy(self):
        return self.stack.copy()

    # 11
    def get_min(self):
        return min(self.stack) if not self.is_empty() else None

    # 12
    def get_max(self):
        return max(self.stack) if not self.is_empty() else None

    # 13
    def sum(self):
        return sum(self.stack)

    # 14
    def average(self):
        if self.is_empty():
            return None
        return sum(self.stack) / self.size()

    # 15
    def count_even(self):
        return sum(1 for x in self.stack if x % 2 == 0)

    # 16
    def count_odd(self):
        return sum(1 for x in self.stack if x % 2 != 0)

    # 17
    def remove_duplicates(self):
        self.stack = list(dict.fromkeys(self.stack))

    # 18
    def sort_ascending(self):
        self.stack.sort()

    # 19
    def sort_descending(self):
        self.stack.sort(reverse=True)

    # 20
    def prioritize(self):
        self.sort_descending()

    # 21
    def push_multiple(self, items):
        for x in items:
            self.push(x)

    # 22
    def pop_multiple(self, k):
        result = []
        for _ in range(min(k, self.size())):
            result.append(self.pop())
        return result

    # 23
    def is_palindrome(self):
        return self.stack == self.stack[::-1]

    # 24
    def get_middle(self):
        if self.is_empty():
            return None
        return self.stack[self.size() // 2]

    # 25
    def replace(self, old, new):
        self.stack = [new if x == old else x for x in self.stack]

    # 26
    def remove_value(self, x):
        self.stack = [v for v in self.stack if v != x]

    # 27
    def frequency(self, x):
        return self.stack.count(x)

    # 28
    def max_frequency(self):
        if self.is_empty():
            return None
        return max(set(self.stack), key=self.stack.count)

    # 29
    def min_frequency(self):
        if self.is_empty():
            return None
        return min(set(self.stack), key=self.stack.count)

    # 30
    def push_if_unique(self, x):
        if x not in self.stack:
            self.push(x)

    # 31
    def swap_top(self):
        if self.size() < 2:
            return
        self.stack[-1], self.stack[-2] = self.stack[-2], self.stack[-1]

    # 32
    def rotate_left(self):
        if self.size() > 1:
            self.stack.append(self.stack.pop(0))

    # 33
    def rotate_right(self):
        if self.size() > 1:
            self.stack.insert(0, self.stack.pop())

    # 34
    def to_string(self):
        return " ".join(map(str, self.stack))

    # 35
    def info(self):
        return {
            "size": self.size(),
            "is_empty": self.is_empty(),
            "top": self.peek()
        }



















class MegaStack:

    # ===== متدهای پایه (1–10) =====
    def __init__(self):                       # 1
        self.stack = []

    def is_empty(self):                       # 2
        return len(self.stack) == 0

    def size(self):                           # 3
        return len(self.stack)

    def push(self, x):                        # 4
        self.stack.append(x)

    def pop(self):                            # 5
        if self.is_empty():
            return None
        return self.stack.pop()

    def peek(self):                           # 6
        return None if self.is_empty() else self.stack[-1]

    def clear(self):                          # 7
        self.stack.clear()

    def copy(self):                           # 8
        return self.stack.copy()

    def to_list(self):                        # 9
        return list(self.stack)

    def contains(self, x):                    # 10
        return x in self.stack

    # ===== آماری (11–20) =====
    def get_min(self):                        # 11
        return min(self.stack) if not self.is_empty() else None

    def get_max(self):                        # 12
        return max(self.stack) if not self.is_empty() else None

    def get_sum(self):                        # 13
        return sum(self.stack)

    def average(self):                        # 14
        return self.get_sum() / self.size() if not self.is_empty() else None

    def count_even(self):                     # 15
        return sum(1 for x in self.stack if x % 2 == 0)

    def count_odd(self):                      # 16
        return sum(1 for x in self.stack if x % 2 != 0)

    def frequency(self, x):                   # 17
        return self.stack.count(x)

    def max_frequency(self):                  # 18
        return max(set(self.stack), key=self.stack.count) if self.stack else None

    def min_frequency(self):                  # 19
        return min(set(self.stack), key=self.stack.count) if self.stack else None

    def unique_count(self):                   # 20
        return len(set(self.stack))

    # ===== مرتب‌سازی و اولویت (21–30) =====
    def sort_ascending(self):                 # 21
        self.stack.sort()

    def sort_descending(self):                # 22
        self.stack.sort(reverse=True)

    def prioritize(self):                     # 23
        self.sort_descending()

    def remove_duplicates(self):              # 24
        self.stack = list(dict.fromkeys(self.stack))

    def push_if_unique(self, x):               # 25
        if x not in self.stack:
            self.push(x)

    def replace(self, old, new):               # 26
        self.stack = [new if x == old else x for x in self.stack]

    def remove_value(self, x):                 # 27
        self.stack = [v for v in self.stack if v != x]

    def get_middle(self):                      # 28
        return self.stack[self.size() // 2] if not self.is_empty() else None

    def is_sorted(self):                       # 29
        return self.stack == sorted(self.stack)

    def reverse(self):                         # 30
        self.stack.reverse()

    # ===== چندعملیاتی (31–40) =====
    def push_multiple(self, items):            # 31
        for x in items:
            self.push(x)

    def pop_multiple(self, k):                 # 32
        result = []
        for _ in range(min(k, self.size())):
            result.append(self.pop())
        return result

    def swap_top(self):                        # 33
        if self.size() >= 2:
            self.stack[-1], self.stack[-2] = self.stack[-2], self.stack[-1]

    def rotate_left(self):                     # 34
        if self.size() > 1:
            self.stack.append(self.stack.pop(0))

    def rotate_right(self):                    # 35
        if self.size() > 1:
            self.stack.insert(0, self.stack.pop())

    def duplicate_top(self):                   # 36
        if not self.is_empty():
            self.push(self.peek())

    def remove_top(self):                      # 37
        if not self.is_empty():
            self.pop()

    def bottom(self):                          # 38
        return self.stack[0] if not self.is_empty() else None

    def remove_bottom(self):                   # 39
        if not self.is_empty():
            self.stack.pop(0)

    def insert_bottom(self, x):                # 40
        self.stack.insert(0, x)

    # ===== منطقی و الگوریتمی (41–55) =====
    def is_palindrome(self):                   # 41
        return self.stack == self.stack[::-1]

    def all_positive(self):                    # 42
        return all(x > 0 for x in self.stack)

    def any_negative(self):                    # 43
        return any(x < 0 for x in self.stack)

    def find_index(self, x):                   # 44
        return self.stack.index(x) if x in self.stack else -1

    def count_greater_than(self, k):           # 45
        return sum(1 for x in self.stack if x > k)

    def count_less_than(self, k):              # 46
        return sum(1 for x in self.stack if x < k)

    def map_square(self):                      # 47
        self.stack = [x * x for x in self.stack]

    def filter_even(self):                     # 48
        self.stack = [x for x in self.stack if x % 2 == 0]

    def filter_odd(self):                      # 49
        self.stack = [x for x in self.stack if x % 2 != 0]

    def sum_top_k(self, k):                    # 50
        return sum(self.stack[-k:])

    def compare_size(self, other):             # 51
        return self.size() - other.size()

    def merge(self, other):                    # 52
        self.push_multiple(other.to_list())

    def equals(self, other):                   # 53
        return self.stack == other.to_list()

    def clear_if_full(self, limit):             # 54
        if self.size() >= limit:
            self.clear()

    def trim(self, k):                         # 55
        self.stack = self.stack[:k]

    # ===== نمایشی و اطلاعاتی (56–65) =====
    def to_string(self):                       # 56
        return " ".join(map(str, self.stack))

    def print_stack(self):                     # 57
        print(self.stack)

    def info(self):                            # 58
        return {
            "size": self.size(),
            "is_empty": self.is_empty(),
            "top": self.peek()
        }

    def memory_usage(self):                    # 59
        return self.size() * 8   # تخمینی

    def reset(self):                           # 60
        self.clear()

    def clone(self):                           # 61
        new = MegaStack()
        new.push_multiple(self.stack)
        return new

    def push_range(self, a, b):                # 62
        for i in range(a, b + 1):
            self.push(i)

    def remove_range(self, a, b):              # 63
        self.stack = [x for x in self.stack if not (a <= x <= b)]

    def count_range(self, a, b):               # 64
        return sum(1 for x in self.stack if a <= x <= b)

    def checksum(self):                        # 65
        return hash(tuple(self.stack))













class MegaStack:

    # ===== متدهای پایه (1–10) =====
    def __init__(self):                       # 1
        self.stack = []

    def is_empty(self):                       # 2
        return len(self.stack) == 0

    def size(self):                           # 3
        return len(self.stack)

    def push(self, x):                        # 4
        self.stack.append(x)

    def pop(self):                            # 5
        if self.is_empty():
            return None
        return self.stack.pop()

    def peek(self):                           # 6
        return None if self.is_empty() else self.stack[-1]

    def clear(self):                          # 7
        self.stack.clear()

    def copy(self):                           # 8
        return self.stack.copy()

    def to_list(self):                        # 9
        return list(self.stack)

    def contains(self, x):                    # 10
        return x in self.stack

    # ===== آماری (11–20) =====
    def get_min(self):                        # 11
        return min(self.stack) if not self.is_empty() else None

    def get_max(self):                        # 12
        return max(self.stack) if not self.is_empty() else None

    def get_sum(self):                        # 13
        return sum(self.stack)

    def average(self):                        # 14
        return self.get_sum() / self.size() if not self.is_empty() else None

    def count_even(self):                     # 15
        return sum(1 for x in self.stack if x % 2 == 0)

    def count_odd(self):                      # 16
        return sum(1 for x in self.stack if x % 2 != 0)

    def frequency(self, x):                   # 17
        return self.stack.count(x)

    def max_frequency(self):                  # 18
        return max(set(self.stack), key=self.stack.count) if self.stack else None

    def min_frequency(self):                  # 19
        return min(set(self.stack), key=self.stack.count) if self.stack else None

    def unique_count(self):                   # 20
        return len(set(self.stack))

    # ===== مرتب‌سازی و اولویت (21–30) =====
    def sort_ascending(self):                 # 21
        self.stack.sort()

    def sort_descending(self):                # 22
        self.stack.sort(reverse=True)

    def prioritize(self):                     # 23
        self.sort_descending()

    def remove_duplicates(self):              # 24
        self.stack = list(dict.fromkeys(self.stack))

    def push_if_unique(self, x):               # 25
        if x not in self.stack:
            self.push(x)

    def replace(self, old, new):               # 26
        self.stack = [new if x == old else x for x in self.stack]

    def remove_value(self, x):                 # 27
        self.stack = [v for v in self.stack if v != x]

    def get_middle(self):                      # 28
        return self.stack[self.size() // 2] if not self.is_empty() else None

    def is_sorted(self):                       # 29
        return self.stack == sorted(self.stack)

    def reverse(self):                         # 30
        self.stack.reverse()

    # ===== چندعملیاتی (31–40) =====
    def push_multiple(self, items):            # 31
        for x in items:
            self.push(x)

    def pop_multiple(self, k):                 # 32
        result = []
        for _ in range(min(k, self.size())):
            result.append(self.pop())
        return result

    def swap_top(self):                        # 33
        if self.size() >= 2:
            self.stack[-1], self.stack[-2] = self.stack[-2], self.stack[-1]

    def rotate_left(self):                     # 34
        if self.size() > 1:
            self.stack.append(self.stack.pop(0))

    def rotate_right(self):                    # 35
        if self.size() > 1:
            self.stack.insert(0, self.stack.pop())

    def duplicate_top(self):                   # 36
        if not self.is_empty():
            self.push(self.peek())

    def remove_top(self):                      # 37
        if not self.is_empty():
            self.pop()

    def bottom(self):                          # 38
        return self.stack[0] if not self.is_empty() else None

    def remove_bottom(self):                   # 39
        if not self.is_empty():
            self.stack.pop(0)

    def insert_bottom(self, x):                # 40
        self.stack.insert(0, x)

    # ===== منطقی و الگوریتمی (41–55) =====
    def is_palindrome(self):                   # 41
        return self.stack == self.stack[::-1]

    def all_positive(self):                    # 42
        return all(x > 0 for x in self.stack)

    def any_negative(self):                    # 43
        return any(x < 0 for x in self.stack)

    def find_index(self, x):                   # 44
        return self.stack.index(x) if x in self.stack else -1

    def count_greater_than(self, k):           # 45
        return sum(1 for x in self.stack if x > k)

    def count_less_than(self, k):              # 46
        return sum(1 for x in self.stack if x < k)

    def map_square(self):                      # 47
        self.stack = [x * x for x in self.stack]

    def filter_even(self):                     # 48
        self.stack = [x for x in self.stack if x % 2 == 0]

    def filter_odd(self):                      # 49
        self.stack = [x for x in self.stack if x % 2 != 0]

    def sum_top_k(self, k):                    # 50
        return sum(self.stack[-k:])

    def compare_size(self, other):             # 51
        return self.size() - other.size()

    def merge(self, other):                    # 52
        self.push_multiple(other.to_list())

    def equals(self, other):                   # 53
        return self.stack == other.to_list()

    def clear_if_full(self, limit):             # 54
        if self.size() >= limit:
            self.clear()

    def trim(self, k):                         # 55
        self.stack = self.stack[:k]

    # ===== نمایشی و اطلاعاتی (56–65) =====
    def to_string(self):                       # 56
        return " ".join(map(str, self.stack))

    def print_stack(self):                     # 57
        print(self.stack)

    def info(self):                            # 58
        return {
            "size": self.size(),
            "is_empty": self.is_empty(),
            "top": self.peek()
        }

    def memory_usage(self):                    # 59
        return self.size() * 8   # تخمینی

    def reset(self):                           # 60
        self.clear()

    def clone(self):                           # 61
        new = MegaStack()
        new.push_multiple(self.stack)
        return new

    def push_range(self, a, b):                # 62
        for i in range(a, b + 1):
            self.push(i)

    def remove_range(self, a, b):              # 63
        self.stack = [x for x in self.stack if not (a <= x <= b)]

    def count_range(self, a, b):               # 64
        return sum(1 for x in self.stack if a <= x <= b)

    def checksum(self):                        # 65
        return hash(tuple(self.stack))








# ===============================
# Circular Queue (صف حلقوی)
# ===============================
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


# ===============================
# Stack (پشته)
# ===============================
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
        return None if self.is_empty() else self.stack[-1]


# ===============================
# Hybrid Structure
# (ارث‌بری از صف حلقوی و پشته)
# ===============================
class HybridStructure(CircularQueue, Stack):
    def __init__(self, size=5):
        super().__init__(size)   # سازنده CircularQueue
        self.stack = []          # سازنده Stack

    # اضافه کردن داده (رفتار صف)
    def add(self, x):
        self.enqueue(x)

    # انتقال عناصر صف به پشته
    def queue_to_stack(self):
        if self.is_empty():
            return

        i = self.front
        while True:
            self.stack.append(self.queue[i])
            if i == self.rear:
                break
            i = (i + 1) % self.size

    # حذف با اولویت پشته
    def remove(self):
        if self.stack:
            return self.stack.pop()
        return self.dequeue()

    # وضعیت ساختار
    def status(self):
        return {
            "queue": self.queue,
            "front": self.front,
            "rear": self.rear,
            "stack": self.stack
        }

    # پاک‌سازی کامل
    def clear_all(self):
        self.front = self.rear = -1
        self.queue = [None] * self.size
        self.stack.clear()














# ===============================
# Stack (پشته)
# ===============================
class Stack:
    def __init__(self):
        self.items = []

    def is_empty(self):
        return len(self.items) == 0

    def push(self, x):
        self.items.append(x)

    def pop(self):
        if self.is_empty():
            return None
        return self.items.pop()

    def peek(self):
        return None if self.is_empty() else self.items[-1]


# ===============================
# Queue using Stack (صف با پشته)
# ===============================
class QueueWithStack:
    def __init__(self):
        self.stack1 = Stack()  # برای enqueue
        self.stack2 = Stack()  # برای dequeue

    # اضافه کردن عنصر (enqueue)
    def enqueue(self, x):
        self.stack1.push(x)

    # حذف عنصر (dequeue)
    def dequeue(self):
        if self.stack2.is_empty():
            while not self.stack1.is_empty():
                self.stack2.push(self.stack1.pop())

        return self.stack2.pop()

    # مشاهده عنصر جلویی صف
    def front(self):
        if self.stack2.is_empty():
            while not self.stack1.is_empty():
                self.stack2.push(self.stack1.pop())

        return self.stack2.peek()

    # بررسی خالی بودن صف
    def is_empty(self):
        return self.stack1.is_empty() and self.stack2.is_empty()












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












# ===============================
# Stack (پشته)
# ===============================
class Stack:
    def __init__(self):
        self.items = []

    def is_empty(self):
        return len(self.items) == 0

    def push(self, x):
        self.items.append(x)

    def pop(self):
        if self.is_empty():
            return None
        return self.items.pop()


# ===============================
# Postfix to Infix
# ===============================
def postfix_to_infix(expression):
    stack = Stack()
    operators = {'+', '-', '*', '/', '^'}

    for ch in expression:
        # اگر عملوند بود
        if ch not in operators:
            stack.push(ch)
        else:
            # اگر عملگر بود
            op2 = stack.pop()
            op1 = stack.pop()
            new_expr = "(" + op1 + ch + op2 + ")"
            stack.push(new_expr)

    return stack.pop()






exp = "ab+c*"
print(postfix_to_infix(exp))















# ======================================
# Node (گره سه‌بعدی)
# ======================================
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None
        self.prev = None
        self.down = None


# ======================================
# Three Dimensional Linked List
# ======================================
class ThreeDimensionalLinkedList:
    def __init__(self):
        self.head = None


    # 1
    def is_empty(self):
        return self.head is None


    # 2
    def add_first(self, data):
        new_node = Node(data)
        if not self.is_empty():
            self.head.prev = new_node
            new_node.next = self.head
        self.head = new_node


    # 3
    def add_last(self, data):
        new_node = Node(data)
        if self.is_empty():
            self.head = new_node
            return
        temp = self.head
        while temp.next:
            temp = temp.next
        temp.next = new_node
        new_node.prev = temp


    # 4
    def remove_first(self):
        if self.is_empty():
            return None
        value = self.head.data
        self.head = self.head.next
        if self.head:
            self.head.prev = None
        return value


    # 5
    def remove_last(self):
        if self.is_empty():
            return None
        temp = self.head
        while temp.next:
            temp = temp.next
        if temp.prev:
            temp.prev.next = None
        else:
            self.head = None
        return temp.data


    # 6
    def search(self, data):
        temp = self.head
        while temp:
            if temp.data == data:
                return True
            temp = temp.next
        return False


    # 7
    def count(self):
        cnt = 0
        temp = self.head
        while temp:
            cnt += 1
            temp = temp.next
        return cnt


    # 8
    def display(self):
        temp = self.head
        while temp:
            print(temp.data, end=" <-> ")
            temp = temp.next
        print("None")


    # 9
    def add_down(self, parent_data, child_data):
        temp = self.head
        while temp:
            if temp.data == parent_data:
                temp.down = Node(child_data)
                return
            temp = temp.next


    # 10
    def display_down(self, data):
        temp = self.head
        while temp:
            if temp.data == data and temp.down:
                print(temp.down.data)
                return
            temp = temp.next


    # 11
    def remove_down(self, data):
        temp = self.head
        while temp:
            if temp.data == data:
                temp.down = None
                return
            temp = temp.next


    # 12
    def has_down(self, data):
        temp = self.head
        while temp:
            if temp.data == data:
                return temp.down is not None
            temp = temp.next
        return False


    # 13
    def get_first(self):
        if self.is_empty():
            return None
        return self.head.data


    # 14
    def get_last(self):
        if self.is_empty():
            return None
        temp = self.head
        while temp.next:
            temp = temp.next
        return temp.data


    # 15
    def clear(self):
        self.head = None















# ======================================
# Node (گره چهار بعدی)
# ======================================
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None
        self.prev = None
        self.down = None
        self.up = None


# ======================================
# Four Dimensional Linked List
# ======================================
class FourDimensionalLinkedList:
    def __init__(self):
        self.head = None


    # 1
    def is_empty(self):
        return self.head is None


    # 2
    def add_first(self, data):
        new_node = Node(data)
        if not self.is_empty():
            self.head.prev = new_node
            new_node.next = self.head
        self.head = new_node


    # 3
    def add_last(self, data):
        new_node = Node(data)
        if self.is_empty():
            self.head = new_node
            return
        temp = self.head
        while temp.next:
            temp = temp.next
        temp.next = new_node
        new_node.prev = temp


    # 4
    def remove_first(self):
        if self.is_empty():
            return None
        value = self.head.data
        self.head = self.head.next
        if self.head:
            self.head.prev = None
        return value


    # 5
    def remove_last(self):
        if self.is_empty():
            return None
        temp = self.head
        while temp.next:
            temp = temp.next
        if temp.prev:
            temp.prev.next = None
        else:
            self.head = None
        return temp.data


    # 6
    def search(self, data):
        temp = self.head
        while temp:
            if temp.data == data:
                return True
            temp = temp.next
        return False


    # 7
    def count(self):
        cnt = 0
        temp = self.head
        while temp:
            cnt += 1
            temp = temp.next
        return cnt


    # 8
    def display(self):
        temp = self.head
        while temp:
            print(temp.data, end=" <-> ")
            temp = temp.next
        print("None")


    # 9
    def add_down(self, parent_data, child_data):
        temp = self.head
        while temp:
            if temp.data == parent_data:
                temp.down = Node(child_data)
                return
            temp = temp.next


    # 10
    def add_up(self, parent_data, child_data):
        temp = self.head
        while temp:
            if temp.data == parent_data:
                temp.up = Node(child_data)
                return
            temp = temp.next


    # 11
    def remove_down(self, data):
        temp = self.head
        while temp:
            if temp.data == data:
                temp.down = None
                return
            temp = temp.next


    # 12
    def remove_up(self, data):
        temp = self.head
        while temp:
            if temp.data == data:
                temp.up = None
                return
            temp = temp.next


    # 13
    def has_down(self, data):
        temp = self.head
        while temp:
            if temp.data == data:
                return temp.down is not None
            temp = temp.next
        return False


    # 14
    def has_up(self, data):
        temp = self.head
        while temp:
            if temp.data == data:
                return temp.up is not None
            temp = temp.next
        return False


    # 15
    def clear(self):
        self.head = None











# =========================
# Node
# =========================
class Node:
    def __init__(self, data):
        self.data = data
        self.prev = None
        self.next = None


# =========================
# Doubly Linked List
# =========================
class doublelinklist:
    def __init__(self, capa):
        self.head = None
        self.tail = None
        self.s = 0
        self.capasity = capa

    def insert_after(self, node_data, new_data):
        cur = self.head
        while cur:
            if cur.data == node_data:
                new_node = Node(new_data)
                new_node.prev = cur
                new_node.next = cur.next
                if cur.next:
                    cur.next.prev = new_node
                else:
                    self.tail = new_node
                cur.next = new_node
                self.s += 1
                return
            cur = cur.next
        print("مقدار مورد نظر پیدا نشد")

    def push_back(self, data):
        new_node = Node(data)
        if self.tail is None:
            self.head = new_node
            self.tail = new_node
        else:
            self.tail.next = new_node
            new_node.prev = self.tail
            self.tail = new_node
        self.s += 1

    def pop_back(self):
        if self.tail is None:
            print("استک خالی")
            return -1
        data = self.tail.data
        self.tail = self.tail.prev
        if self.tail:
            self.tail.next = None
            self.s -= 1
        else:
            self.head = None
            self.s = 0
        return data

    def back(self):
        if self.tail is None:
            print("استک خالی")
            return -1
        return self.tail.data

    def size(self):
        return self.s

    def is_empty(self):
        return self.head is None

    def print_all(self):
        cur = self.head
        while cur:
            print(cur.data, end=" ")
            cur = cur.next
        print()


# =========================
# Stack (با لیست پیوندی)
# =========================
class stack:
    def __init__(self, faza):
        self.faza = faza
        self.a = doublelinklist(faza)

    def push(self, data):
        if self.a.size() >= self.faza:
            print("پر هست استک")
            return -1
        self.a.push_back(data)

    def pop(self):
        return self.a.pop_back()

    def top(self):
        return self.a.back()

    def is_empty(self):
        return self.a.is_empty()

    def force_insert(self, data):
        self.a.push_back(data)

    def print_all(self):
        self.a.print_all()


# =========================
# Count even numbers (Linked List)
# =========================
def count_even(linked_list_object):
    even_count = 0
    current_node = linked_list_object.head

    while current_node:
        if current_node.data % 2 == 0:
            even_count += 1
        current_node = current_node.next

    return even_count


# =========================
# Count & Print even numbers (Stack)
# =========================
def count_even2(stack_object):
    even_count = 0
    print("اعداد زوج در استک:")

    current_node = stack_object.a.head
    while current_node:
        if current_node.data % 2 == 0:
            print(current_node.data, end=" ")
            even_count += 1
        current_node = current_node.next

    print()
    print(f"تعداد کل اعداد زوج: {even_count}")
    return even_count


# =========================
# Test
# =========================
test_stack = stack(10)

for _ in range(10):
    r = random.randint(1, 20)
    test_stack.push(r)

result = count_even2(test_stack)












 

