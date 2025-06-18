To add a timer port to a capsule, place the cursor after its initial `{` and press `ctrl+space`. Select the command **New Port**. Give the port a name (for example `timer`) and set its type to the predefined `Timing` protocol. The created port will by default be declared with the `service` keyword, which means that other capsules can send events to it. We don't want that for a timer port, so replace that keyword with `behavior` instead which makes it a non-service behavior port. Non-service means that only the capsule itself can use the port, and behavior means that any event that arrives on the port will be handled by the capsule's own state machine.

To set the timer in the initial transition, write a line of code that calls the `informIn` function on the timer port like this:

```cpp
RTTimerId tid = timer.informIn(RTTimespec(1, 0));
```

The returned [RTTimerId](https://secure-dev-ops.github.io/code-realtime/targetrts-api/class_r_t_timer_id.html) object represents the timer request and you should call `isValid()` on this object to make sure the timer was successfully set.

Finally add a transition from `S1` to `S2` with a trigger that makes it run when the `timeout` event is received on the timer port. You can do it by placing the cursor after the initial transition and press `ctrl+space`. Select the command **New Triggered Transition**. Note that this transition doesn't need a code snippet because "Hello World!" will be printed when state `S2` is entered, which happens right after the timeout transition has executed.