A guard condition for a transition is specified using the `when` keyword after the transition trigger. The guard condition can access the value of the received event through the `rtdata` parameter. For example, a transition that only should go from `S1` to `S2` when the received event has a value that is 5 will look like this:

```art
S1 -> S2 on somePort.someEvent when `*rtdata == 5`
```

You need to ensure that guard conditions are mutually exclusive, i.e. are written in a way so that only one of them will return `true` for the triggered transitions of a certain state. A good way to achieve that is to use the keyword `else` in a guard. That guard will become `true` if none of the other guards for the transitions of the state returns `true`. So even if the two guards below have mutually exclusive guard conditions:

* when \`x < 3\`
* when \`x >= 3\`

it's better to write them like this instead

* when \`x < 3\`
* when \`else\`

because if you later need to change the first guard, there is no need to also change the second guard to keep them mutually exclusive.

Use the function `getCurrentStateString()`, defined in [`RTActor`](https://secure-dev-ops.github.io/code-realtime/targetrts-api/class_r_t_actor.html), to get the name of the state that is currently active in the state machine.

_Note:_ The `rtdata` parameter is only available in guard conditions and transition effect code snippets. If you need to access the data of the received event elsewhere in a capsule code snippet, you can call `getMsg()` to get the [`RTMessage`](https://secure-dev-ops.github.io/code-realtime/targetrts-api/class_r_t_actor.html) that represents the received event. Then you can call `getData()` on that object to get the data of the received event. However, this function returns the data as an untyped pointer (`void*`) which you have to cast to the expected type. Because of this it's recommended to use `rtdata` whenever possible. In this particular example, it would have been better to pass the event data with a `float` parameter to the `logTooLow()` function.