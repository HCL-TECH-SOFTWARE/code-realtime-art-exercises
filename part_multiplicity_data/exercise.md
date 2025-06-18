### Make the application print 6 unique greetings by only using one fixed and one optional capsule part

A capsule [part](https://secure-dev-ops.github.io/code-realtime/art-lang/#part) can at run-time contain more than one capsule instance. How many capsule instances that a part can contain is decided by its **multiplicity**. In the exercise about optional parts you learnt that a multiplicity consists of two numbers on the syntax `[lower..upper]`. The lower limit specifies how many capsule instances that should be automatically created in a fixed part when the container capsule instance is created. For an optional part the lower limit is therefore always 0 (since no capsule instances are automatically created in optional parts). In this exercise we'll look at the upper limit of the part multiplicity, which specifies the maximum number of capsule instances that can fit in the part at runtime.

1. Create two parts in the <a class="open-file-link" href="Top.art">Top</a> capsule, both typed by the `Greeting` capsule. Call the first part `fPart` and make it fixed with multiplicity `[3]`. Call the second part `oPart` and make it optional with multiplicity `[0..3]`. 
2. Extend the printout message in the `Greeting` capsule so it also prints the index at which it is located within the part. Use the function `getIndex()` that is provided by the TargetRTS class [`RTActor`](https://secure-dev-ops.github.io/code-realtime/targetrts-api/class_r_t_actor.html).
3. Build and run the application. You should see 3 printouts like this (if necessary, adjust your code so the printout follows this format):

```shell
Hello from part fPart at index 0
Hello from part fPart at index 1
Hello from part fPart at index 2
```

4. Create a frame port in the <a class="open-file-link" href="Top.art">Top</a> capsule and use the `incarnate()` function provided by that frame port to create 3 instances of `Greeting` when the <a class="open-file-link" href="Top.art">Top</a> capsule starts up.
5. The `getIndex()` function returns the zero-based index of the running capsule instance within its container part. There is also a function `index()` which returns the one-based index (i.e. the first index is 1 rather than 0). Complete the exercise by changing the code so it prints the one-based index instead.

_Note:_ From the order of the printouts we can learn that when a capsule instance is created, it will incarnate its fixed parts *before* its initial transition runs. This is important because it ensures that when the initial transition runs, all capsule instances in fixed parts are already available and can be used by the capsule. In later exercises you will learn how a capsule instance can communicate with the capsule instances in its parts by means of events.