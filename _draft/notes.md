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