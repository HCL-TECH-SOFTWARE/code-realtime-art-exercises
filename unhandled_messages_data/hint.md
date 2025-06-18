Use [internal transitions](https://secure-dev-ops.github.io/code-realtime/art-lang/#internal-transition) to handle an event in a state without leaving the state. Note that

- a transition doesn't need to have an effect code snippet
- a transition can have multiple triggers (separated by commas)

An asterisk (`*`) can be used in a trigger instead of explicitly mentioning a specific event. This will make the trigger apply for all events that are received on a port. Use of such "asterisk triggers" are useful to make a state machine more resilient to changes in the protocols that type its service ports.