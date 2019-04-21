# react-soft-slider

![npm (tag)](https://img.shields.io/npm/v/react-soft-slider/beta.svg) ![npm bundle size](https://img.shields.io/bundlephobia/minzip/react-soft-slider.svg) ![NPM](https://img.shields.io/npm/l/react-soft-slider.svg) [![BuildStatus](https://travis-ci.org/dbismut/react-soft-slider.svg?branch=5.x)](https://travis-ci.org/dbismut/react-use-gesture)

React-soft-slider is a minimally-featured carousel. It focuses on providing the best user experience for manipulating slides. It doesn't try to implement additional features such as pagination-dots, next and previous buttons, autoplay. If you're looking for a slider that has all this, there's [plenty](https://github.com/akiran/react-slick) of [alternatives](https://github.com/FormidableLabs/nuka-carousel) [out](https://github.com/express-labs/pure-react-carousel) [there](https://github.com/voronianski/react-swipe).

This allows react-soft-slider to be highly impartial when it comes to styling, you shouldn't be fighting too hard when it comes to making the slider slider look the way you want.

- **Touch-gesture compatible:** handles swipe and drag on mobile and desktop devices
- **Spring animations:** driven by high-performance springs
- **Impartial styling:** you are responsible for the styling of your slides
- **Fully responsive:** as long as your slides styling is responsive as well!
- **Dynamic number of slides:** you can add or remove slides on the fly

React-soft-slider is powered by [react-spring](https://github.com/react-spring/react-spring) for springs animation and [react-use-gesture](https://github.com/react-spring/react-use-gesture) for handling the drag gesture.

## Installation

```
npm install react-soft-slider
```

## Usage

`<Slider />` as a very limited logic, and essentially does two things: it positions the slider to the slide `index` you should provide as a prop, and when the user drags a slide, it will tell you what index he's trying to set through the `onIndexChange` prop. You will usually respond by updating the index as below:

```jsx
import Slider from 'react-soft-slider'

const slides = ['red', 'blue', 'yellow', 'orange']
const style = { width: 300, height: '100%', margin: '0 10px' }

function App() {
  const [index, setIndex] = React.useState(0)

  return (
    <Slider index={index} onIndexChange={setIndex} style={{ width: 400, height: 200 }}>
      {slides.map((color, i) => (
        <div key="i" style={{ ...style, background: color }} />
      ))}
    </Slider>
  )
}
```

As you can see from the example, any child of the `<Slider /> component is considered as a slide. You are fully responsible for the appearance of the slides, and each slide can be styled independently.

> **Note:** although the above example uses hooks, react-soft-slider is compatible with Class-based components. However, since it internally uses hooks, it requires React `16.8+`.

### Props

The `<Slider />` component accepts the following props:

| Name              | Type                                | Description                                                                                       | Default                                     |
| ----------------- | ----------------------------------- | ------------------------------------------------------------------------------------------------- | ------------------------------------------- |
| `children`        | `node`                              | elements you should pass to the slider and that will be considered as slides                      | Required                                    |
| `index`           | `number`                            | the index of the slide that should be shown by the slider                                         | Required                                    |
| `onIndexChange()` | `(newIndex: number) => void`        | function called by the slider when the slide index should change                                  | Required                                    |
| `enabled`         | `boolean`                           | enables or disables the slider gestures                                                           | `true`                                      |
| `trail`           | `boolean`                           | enables or disables trailing of slides (staggered animations)                                     | `true`                                      |
| `draggedScale`    | `Number`                            | scale factor of the slides when dragged                                                           | `1.0`                                       |
| `draggedSpring`   | `object`                            | spring between the pointer and the dragged slide                                                  | `{ tension: 1200, friction: 40 }`           |
| `trailingSpring`  | `object`                            | spring of the other slides                                                                        | `{ mass: 10, tension: 800, friction: 200 }` |
| `onDragStart()`   | `(pressedIndex: number) => void`    | function called when the drag starts, passing the index of the slide being dragged as an argument |                                             |
| `onDragEnd()`     | `(pressedIndex: number) => void`    | function called when the drag ends, passing the index of the slide being dragged as an argument   |                                             |
| `className`       | `string`                            | CSS class passed to the slider wrapper                                                            |                                             |
| `style`           | `object`                            | style passed to the slider wrapper                                                                |                                             |
| `slideStyle`      | `object` or `(i: number) => object` | style passed to the slides                                                                        |                                             |

### Springs configruation

React-soft-slider uses two springs, that you can configure to your liking. It accepts any options supported by react-spring, [see here for more info](https://www.react-spring.io/docs/hooks/api).

## Gotchas

**Sizing your slides relatively to the slider**

If you want to size your slides relatively to the slider width (let's say `width: 80%`), you'll need to rely on `slideStyle` set to `{{ minWidth: '80%' }} and styling your slide with`width`set to`100%`.

**Don't use transform styling in slideStyle**

React-soft-slider uses the `transform` attribute to make slides move so transform attributes in `slideStyle` will get overriden.

**React-soft-slider is open to suggestions!**

React-soft-slider will probably never include slider peripheral features, but is open to suggestions to make handling your slides easier.

## Todo

- [ ] Tests
- [ ] Actually learn and test Typescript definitions
- [ ] Support vertical sliding
- [ ] Prevent scroll on mobile when moving the slider ?