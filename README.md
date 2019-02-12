# rsup-duration
Convenient duration time utility

## Install
```sh
npm install rsup-progress
```
```js
import duration from 'rsup-duration'
```

## Example
```js
const d = duration()

console.log(d.isPast) // => false
console.log(d.isDuring) // => false

d.start(1000)
console.log(d.isPast) // => false
console.log(d.isDuring) // => true

await d.waitOnStop() // Resolved after 1 second.

console.log(d.isPast) // => true
console.log(d.isDuring) // => false

d.start(1000)
console.log(d.isPast) // => false
console.log(d.isDuring) // => true

delay(200).then(()=> d.stop())
await d.waitOnStop() // Resolved after 200ms.
```

## API
### duration(defaultMs = 0)
Create a duration instance.

### d.isPast
Returns whether the duration has passed.

### d.isDuring
Returns whether the duration is in progress.

### d.start([ms = defaultMs [, force = false]])
Start time. If already in progress, this call is ignored.

- `ms` - duration time. If not, the `defaultMs` is specified.
- `force`  - If `force` is true, stop and new start when time is in progress.

```js
const d = duration(1000)
d.start() // ms = 1000, force = false
d.start(500) // ms = 500, force = false
d.start(500, true) // ms = 500, force = true
d.start(true) // // ms = 1000, force = true
```

Returns the promise that waits until stop.
```js
console.log(d.isPast) // => false
await d.start(1000) // Resolved after 1 second.
console.log(d.isPast) // => true
```

### d.stop()
Stop time.

```js
d.start(1000)
delay(200).then(()=> d.stop())
await d.waitOnStop() // Resolved after 200ms.
```

### d.waitOnStop()
Returns the promise that waits until stop.

## License
MIT
