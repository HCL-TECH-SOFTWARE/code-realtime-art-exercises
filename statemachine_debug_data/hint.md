The data of an event is accessible in a transition code snippet through the `rtdata` parameter. If you navigate to the generated code for the effect code of `e2` you'll see that it has the type `const int*`. This means that you need to dereference this pointer to print the `int` value.

Usually the data of an event should not be modified by the receiver which is why it is defined as `const`. In some special cases, for example when you need to call a move assignment operator, you need the `rtdata` parameter to be non-const. You can achieve this by setting the `const_rtdata` property on the transition to `false`:

```art
e2: [[rt::properties(const_rtdata=false)]]
    InitialState -> StateB on comPort.e2 
    `
        Log::out << "Transition e2 with data " << *rtdata << std::endl;
    `;
```
