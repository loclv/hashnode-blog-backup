## TypeScript in Angular - Use generic class with Service 🧋

### Story 🏕️

When we want to use `Service`'s property/method with a special types *each* component.
Basiclly, we want to reuse a logic inside `Service` with type-checking at outside of that `Service`.

For example, in `ExampleService`:

```ts
import { Type } from '@angular/core';

@Injectable({ providedIn: 'root' })
export default class ExampleService {
  /**
   * Gets last component.
   */
  get lastComponent(): Type<any> | undefined {
    // TODO: do something
    return this.loverlyComponents[this.loverlyComponents.length - 1];
  }
}

// ...
export class TheNextComponent {
  constructor(private exampleService: ExampleService) {}

  doSomethings() {
    if (!this.exampleService.lastComponent) return;

    // when you hover on `this.exampleService.lastComponent` by mouse,
    // `Type<any>` is showed up.
    console.log(this.exampleService.lastComponent);
  }
}
```

We don't know exactly what type of last component, what we surely know beacause we used that component recently.
So, we *can not* use last component safely, beacause it's type is `any`.

### Solution ✨

Use [generic class](https://www.typescriptlang.org/docs/handbook/2/generics.html#generic-classes) with service:

```ts
@Injectable({ providedIn: 'root' })
export default class ExampleService<TLastComponent> {
  /**
   * Gets last component.
   */
  get lastComponent(): TLastComponent | undefined {
    // TODO: do something
    return this.loverlyComponents[this.loverlyComponents.length - 1];
  }
}
```

And when inject it into component, we surely know what component is `lastComponent`:

```ts
export class TheNextComponent {
  constructor(
    private exampleService: ExampleService<TheBlueComponent>
  ) {}

  doSomethings() {
    if (!this.exampleService.lastComponent) return;

    // when you hover on `this.exampleService.lastComponent` by mouse,
    // `TheBlueComponent` is showed up.
    console.log(this.exampleService.lastComponent);

    // we can use `lastComponent`'s method safely now ✨
    this.exampleService.lastComponent.goGreen();
  }
}
```
