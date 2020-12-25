# Vuetify Fullscreen Timer
## Installation
Install the package through `npm`
```
npm install vuetify-fullscreen-timer
```

## Usage
To use the componet simply, import into the *.vue file you wan to have it in like below:
```
<template>
    <vuetify-fullscreen-timer :start-point="YOUR_START_POINT_AS_DATE"></vuetify-fullscreen-timer>
</template>
import VuetifyFullscreenTimer from 'vuetify-fullscreen-timer';

export default {
    components: {
        VuetifyFullscreenTimer
    }
}
```
**Hint:** Since its a normal component adding you can just give it any name you like. Look at the following example.
```
<template>
    <my-timer></my-timer>
</template>
export default {
    components: {
        'my-timer': VuetifyFullscreenTimer
    }
}
```
### Properties
* **outputMode:** By default is set to `minutes`. This property will define the output type when the user clicks `stop`. This property is based on the `moment js` library datetime units.
* **startPoint:**  This property is **mandatory**. `startPoint` tells the component to start counting the time difference since when. The type that this property accepts is `Date`.
* **title:** You can give the timer a title so it shows up in big fonts to see why the timer is started. **This is optional**.

