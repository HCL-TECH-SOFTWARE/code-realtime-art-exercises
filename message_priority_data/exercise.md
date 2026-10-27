### Use message priorities to control the order in which messages are received

When an event is sent it's possible to assign a [priority](https://secure-dev-ops.github.io/code-realtime/target-rts/message-communication/#message-priority) to the [RTMessage](https://secure-dev-ops.github.io/code-realtime/targetrts-api/class_r_t_message.html) object that is placed in the receiver's message queue. Messages are ordered in that queue based on their priorities. In this exercise you will use message priorities to control the order in which sent messages are received.

_Note:_ In a real application it's advisable to stick to the default message priority (`General`) unless there is a good reason not to. Excessive use of message priorities may indicate a design problem in the application.

1. Open the <a class="open-file-link" href="Top.art">Top</a> capsule to find the initial transition where 5 characters are sent to the `WordCollector` capsule using the `character` event. Note that no priority is specified, which means that the default `General` priority will be used. Build and run the application to confirm that the messages arrive in the same order as they are sent.

2. Navigate to the `send()` function in the TargetRTS by `ctrl+click` on one of the send-calls (click on the "send" name). 

```cpp
RTS_INLINE int RTOutSignal::send( int priority )
{
    return _port->send( _signal, _data, _type, priority, _rValueRef );
}
```

As you can see, the `send()` function allows a priority to be passed.

3. Use the priorities defined in [RTPriority.h](https://secure-dev-ops.github.io/code-realtime/targetrts-api/_r_t_priority_8h_source.html) to change the order in which the messages are received. Note that the two highest priority levels `Synchronous` and `System` are reserved for internal use within the TargetRTS (for example, `Synchronous` is used for implementing synchronous communication). Set the priorities so the `WordCollector` builds the word "CODER".

4. Build and run the application. Make sure no run-time errors are printed.
