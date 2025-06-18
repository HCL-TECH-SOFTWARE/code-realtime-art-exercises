The implementation of the capsule constructor can look like this:

```cpp
Operator::Operator(RTController* rtg_rts, RTActorRef* rtg_ref, const std::string& operatorName) 
        : RTActor(rtg_rts, rtg_ref), name(operatorName) {}
```

A frame port is a behavior port that is typed with the predefined `Frame` protocol.