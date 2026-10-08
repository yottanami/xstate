---
'xstate': patch
---

`stateIn(...)` can now be used as a guard in machines created with `setup(...)` that don't configure any guards. It previously failed to type-check with `Type 'any' is not assignable to type 'never'`, also when wrapped in `not(...)`, `and([...])` or `or([...])`.

An unknown guard name next to `stateIn(...)` inside `and`, `or` or `not` (e.g. `and(['chekc', stateIn('idle')])`) is now reported as a type error. It was previously accepted by the types and failed at runtime.

```ts
setup({
  types: {
    events: {} as { type: 'TOGGLE' }
  }
}).createMachine({
  initial: 'idle',
  states: {
    idle: {
      on: {
        TOGGLE: { guard: stateIn('idle') }
      }
    }
  }
});
```
