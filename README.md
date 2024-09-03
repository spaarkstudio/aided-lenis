[![LENIS](https://assets.darkroom.engineering/lenis/header.png)](https://github.com/darkroomengineering/lenis)

Go to [darkroomengineering/lenis](https://github.com/darkroomengineering/lenis) for docs. This repository only documents patches made for better control over lenis.

## Patches
- Introduce `changed` boolean variable to `onComplete`.
    - If the scrollTo `target` is equals to the current scroll offset, `changed` would be `false`, otherwise `changed` would be `true`.
    - Reason: `changed` allows developers to handle asynchronous tasks differently when `scrollTo` does not do anything and executes `onComplete`.
```js
lenis.scrollTo(target, {
    duration: 2,
    onComplete(lenis, changed) {
        if (changed) {
            console.log("It did scroll, so I'm executed after 2 seconds.");
        } else {
            console.log("The target is the same as scroll offset, so I'm executed immediately.");
        }
    }
});
```