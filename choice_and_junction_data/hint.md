You can access the data of an event from the guard code snippet by dereferencing the `rtdata` parameter.

An `else` guard is a guard condition which consists of the keyword `else`. The transition with the `else` guard will execute if no other outgoing transition from the choice will execute, because their guard conditions return `false`.

Do not use an `else` guard for the transition from the junction to `PositiveThenNegative` since it would become `true` also if the second number is zero. If the second number is zero the state machine should remain in the `Positive` state.
