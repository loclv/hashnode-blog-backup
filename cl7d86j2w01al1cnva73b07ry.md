## phaser 3 - How to start game until player press a key 🏁

> Phaser is a fun, free and fast 2D game framework for making HTML5 games for desktop and mobile web browsers, supporting Canvas and WebGL rendering.

## Example code

```ts
import { ScreenName } from '@model';

// first, you must extends Phaser.Scene class to use `input` property.
export class MainMenuScene extends Phaser.Scene {
  private startKey!: Phaser.Input.Keyboard.Key;

  constructor() {
    super({
      key: ScreenName.MainMenuScene,
    });
  }

  init(): void {
    // Create a key object for checking it's status.
    this.startKey = this.input.keyboard.addKey(
      Phaser.Input.Keyboard.KeyCodes.SPACE
    );

    // when initialization, set it's down status is `false`.
    this.startKey.isDown = false;
  }

  // This method is called once per game step,
  // while the scene is running.
  // It looks like this method is called per frame rate. 😹
  update(): void {
    // If player press a key (for example, a space key),
    // `isDown` property is `true`.
    if (this.startKey.isDown) {
      // Start a new scene.
      this.scene.start(ScreenName.GameScene);
    }
  }
}
```

## Reference

- [Phaser](https://phaser.io/)
- [digitsensitive/phaser3-typescript - template](https://github.com/digitsensitive/phaser3-typescript#readme)
