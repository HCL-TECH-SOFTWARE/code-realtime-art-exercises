The Art syntax for inheriting a capsule is the same as in C++ (but without a visibility keyword; inheritance in Art is always public). For example:

```art
capsule Derived : Base {
    // ...
};
```

An easy way to redefine the `Done` state is to copy it from the `Greeting` capsule and just add the `redefine` keyword before the state name.

To access the type descriptor `RTType_SpanishGreeting` the `Greeting` capsule needs to include `SpanishGreeting.h`. Use an `[[rt::impl_preface]]` code snippet for adding the include directive.
