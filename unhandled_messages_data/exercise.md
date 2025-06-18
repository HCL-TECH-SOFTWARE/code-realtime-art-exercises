### Make the application handle all events it can receive

A capsule state machine should at all times be prepared to handle messages for *all* events that can be received on *all* its service ports. If the TargetRTS dispatches a message to a capsule which its state machine does not handle, a run-time error will be printed. Read more about unexpected messages in [the documentation](https://secure-dev-ops.github.io/code-realtime/target-rts/message-communication/#unhandled-messages).

This exercise application consists of a <a class="open-file-link" href="Top.art">Top</a> capsule with a fixed part `cap` typed by the <a class="open-file-link" href="Cap.art">Cap</a> capsule. `Top` sends the events defined in <a class="open-file-link" href="Events.art">Events.art</a> to `Cap`. However, the `Cap` state machine is incomplete and not ready to handle all of the events in all its states.

1. Start by connecting the ports `p1` and `p2` of the <a class="open-file-link" href="Top.art">Top</a> capsule with the ports `port1` and `port2` of the <a class="open-file-link" href="Cap.art">Cap</a> capsule. Remember that a conjugated port (marked with a `~` after its name) swaps the meaning of in-events and out-events. When you have connected the ports correctly there should no longer be any warnings reported for `Top`.

2. Look at the <a class="open-file-link" href="Top.art">Top</a> capsule state machine to understand how it communicates with `Cap` by sending events to it. Compare that with the state machine of the <a class="open-file-link" href="Cap.art">Cap</a> capsule. You may already now realize that `Cap`'s state machine is not prepared to handle all messages it receives from `Top`.

3. Build and run the application. The state machine of `Cap` transitions to state `S3`, but two run-time errors are printed:

```shell
cap(1)@S1 received unexpected message: port2[1]%in1 data: void
cap(1)@S3 received unexpected message: port1[1]%out1 data: void
```

These messages show that the state machine of `Cap` doesn't handle all possible messages that it can receive in all its states. Read [this chapter in the documentation](https://secure-dev-ops.github.io/code-realtime/target-rts/logging/#targetrts-error-logging) to understand how to interpret these messages.

4. Fix the state machine of the <a class="open-file-link" href="Cap.art">Cap</a> capsule so that all messages are handled and these errors no longer occur.

5. Again build and run the application to confirm that the `Cap` state machine now transitions to state `S3` without any errors caused by unhandled messages.

6. Add two more events to the <a class="open-file-link" href="Events.art">Events</a> protocol:

```art
in newIn(); 
out newOut(); 
```

7. Update the initial transition of the <a class="open-file-link" href="Top.art">Top</a> capsule state machine so it looks like this:

```art
p2.in1().send();
p2.newIn().send(); // new event
p1.out1().send();
p1.newOut().send(); // new event
p2.in1().send();
p2.newIn().send(); // new event
p1.out1().send();
p1.newOut().send(); // new event
```

8. Build and run the application. If you now again get errors that show that the `Cap` state machine doesn't handle the new events, update the state machine so the errors don't occur. Can you find a way to do it without having to explicitly mention the newly added events?