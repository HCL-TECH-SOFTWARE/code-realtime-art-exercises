You can print messages to `stdout` using a [Log Stream](https://secure-dev-ops.github.io/code-realtime/target-rts/logging/#log-stream).
For this exercise you can choose to print the message in the initial transition, which is the first transition that will execute in the state machine after the top capsule instance has been created when the application starts to run:

``` art
initial -> State
`
    // Use Log::out here
`;
```

Or you can choose to add an [entry action](https://secure-dev-ops.github.io/code-realtime/art-lang/#entry-and-exit-action) for the state `State` which will run when it is entered (which happens just after the initial transition has executed).

``` art
state State {
    entry
    `
        // Use Log::out here
    `;
};
```

Note that the application will not terminate by itself. Rather it will keep running, and stay in state `State` forever. To make it terminate you can call `abort()` on the [Controller](https://secure-dev-ops.github.io/code-realtime/targetrts-api/class_r_t_controller.html) that runs the capsule. You can get a pointer to that Controller by calling the `context()` function from any code snippet within the capsule. That function is one of many functions which the TargetRTS provides through the [`RTActor`](https://secure-dev-ops.github.io/code-realtime/targetrts-api/class_r_t_actor.html) class which all C++ classes that are generated from capsules inherit from.