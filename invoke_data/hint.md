When an event is invoked, a pointer to an [RTMessage](https://secure-dev-ops.github.io/code-realtime/targetrts-api/class_r_t_message.html) object has to be passed by the client. Store it on the stack so it is automatically deleted.

```cpp
RTMessage reply1;
serverP.getDouble(14).invoke(&reply1);
```

A port becomes [notifying](https://secure-dev-ops.github.io/code-realtime/art-lang/#notifying-port) by declaring it with the `notify` keyword.
