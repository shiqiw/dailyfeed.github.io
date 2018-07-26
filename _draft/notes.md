### Shared cache service
> Local persistent or make secondary

### [Continuous availability](https://en.wikipedia.org/wiki/Continuous_availability)

### Cluster products

### Concurrency
> Shared state concurrency => use lock, use java.util.concurrent.*
> 
> Message passing concurrency
>
> STM (atomic, does not guarantee synchronize)

### Event driven architecture
> Domain event ==> event hub
>
> Event sourcing
>
> Manual reset
>
> Exclusive, not for broadcast message ==> do not use event hub/ kafka for publisher subscriber model.
>
> Networking braodcasting token ring

### CQRS
> Netflix, LinkedIn, Uber use kafka.
>
> From data => presentation => business => data to report => presentation => event. Storage is separate with event.
>
> Wrtie data store is separate from read data store. Read is way more than write, it is like master-slave => won't be inconsistent.

### Publish subscribe

### Point to point

### Store-forward
> Sender => mediator (storage, e.g when not proper processor, store and forward) => receiver

### Request reply
> Request => queue (does not duplicate) => reply

### Sender and subscriber
> Send with topic, subscribe and duplicate event in same channel
>
> Service bus

### Competing consumer

### Queue based load leveling pattern

### Messaging

### Fire forget
fire receive evetually

### PV操作
当一个进程阻塞了的时候，它已经执行过了P操作，并卡在临界区那个地方。当唤醒它时就立即进入它自己的临界区，并不需要执行P操作了，当执行完了临界区的程序后，就执行V操作。

### About Python Makefile
[Makefiles in python projects](https://krzysztofzuraw.com/blog/2016/makefiles-in-python-projects.html)

### Create a python app in Azure
https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-get-started-python

### LMAX
High-perf inter-thread messaging library

### Java tree map
Guaranteed O(log n) runtime based on red-black tree.

Key ordered in natural order by default.

Used for ceiling and floor (key) range.

### Design Google canlendar

Kafka/ Event hub/ Message queue

Apache Spark

Samza