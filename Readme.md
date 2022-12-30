
# CREATING A CHANNEL

To create a channel, we can use the static Channel class which exposes factory methods to create the two main types of channel. 

## CreateUnbounded<T> 
creates a channel with an unlimited capacity. This can be quite dangerous if your producer outpaces you the consumer. In that scenario, without a capacity limit, the channel will keep accepting new items. When the consumer is not keeping up, the number of queued items will keep increasing. Each item being held in the channel requires some memory which can’t be released until the object has been consumed. Therefore, it’s possible to run out of available memory in this scenario.

## CreateBounded<T> 
creates a channel with a finite capacity. In this scenario, it’s possible to develop a producer/consumer pattern which accommodates this limit. For example, you can have your producer await (non-blocking) capacity within the channel before it completes its write operation. This is a form of backpressure, which, when used, can slow your producer down, or even stop it, until the consumer has read some items and created capacity.

We won’t cover these producer/consumer patterns in this post, so I’m going to use a single unbounded channel in my sample. For real-world applications, I recommend sticking to bounded channels. (from https://www.stevejgordon.co.uk/an-introduction-to-system-threading-channels)