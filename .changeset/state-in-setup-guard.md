---
'xstate': patch
---

`stateIn(...)` can now be used as a guard in machines created with `setup(...)` that don't configure any guards. It previously failed to type-check with `Type 'any' is not assignable to type 'never'`.

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
