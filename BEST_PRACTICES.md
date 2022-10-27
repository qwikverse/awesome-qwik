# Best Practices
1. A best practice to follow in Qwik features passing a store to child components rather than individual primitives. When you use primitives, the parent component needs to rerender just to pass in the new value. When you pass in a store, the parent component doesn't need to rerender.

```js
import { component$, useStore } from '@builder.io/qwik';

interface CountStore {
  count: number;
}

export const App = component$(() => {
  const store = useStore<CountStore>({ count: 0 });

  return (
    <>
      <button onClick$={() => store.count++}>+1</button>
      <Display store={store} />
    </>
  );
});

interface DisplayProps {
  store: CountStore;
}
export const Display = component$((props: DisplayProps) => {
  return <div>The count is: {props.store.count}</div>;
});


```