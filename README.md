# pystack
Synchronized stack data structure for Python 3


**Usage**

```
from stack import Stack

stack = Stack()

# push item
stack.push('item')

# pop item
item = stack.pop()
```


**Define size**

```
stack = Stack(10)
```

**Producer Consumer example**

```
from stack import Stack

import random
from threading import Thread
from time import sleep

_stack = Stack(10)

item_number = 0


class Producer(Thread):
    __id = 1

    def __init__(self, stack: Stack):
        super().__init__(name='P-%d' % Producer.__id)
        self.__stack = stack
        Producer.__id = Producer.__id + 1
        pass

    def run(self):
        global item_number
        while (True):
            item = 'item_%d' % item_number
            self.__stack.push(item)
            print(self.name, ' produced ', item)
            item_number = item_number + 1
            sleep(random.randint(0, 1) * 0.3)


class Consumer(Thread):
    __id = 1

    def __init__(self, stack):
        super().__init__(name='C-%d' % Consumer.__id)
        self.__stack = stack
        Consumer.__id = Consumer.__id + 1
        pass

    def run(self):
        global item_number
        while (True):
            item = self.__stack.pop()
            print(self.name, ' consumed ', item)
            item_number = item_number - 1
            sleep(random.randint(0, 1) * 0.3)


p1 = Producer(_stack)
p2 = Producer(_stack)
p3 = Producer(_stack)
c1 = Consumer(_stack)
c2 = Consumer(_stack)
c3 = Consumer(_stack)

p1.start()
p2.start()
p3.start()
c1.start()
c2.start()
c3.start()
```

**Any help or suggestion would be appreciated cheers**
