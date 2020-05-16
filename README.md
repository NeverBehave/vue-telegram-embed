# vue-telegram-embed

Component for Telegram Embed content

## Install and basic usage

```bash
$ npm install --save vue-telegram-embed
```

Register the component

```js
import Vue from 'vue'
import VueTelegramEmbed from "vue-telegram-embed";

// import default styles
import 'vue-telegram-embed/dist/VueTelegramEmbed.css'

Vue.component('vue-telegram-embed', VueTelegramEmbed)
```

You may now use the component in your markup

You may now use the component in your markup

```vue
<template>
    <div id="app">
        <VueTelegramEmbed link="telegram/83" />
    </div>
</template>

<script>
import VueTelegramEmbed from "vue-telegram-embed";

export default {
    components: {
        VueTelegramEmbed
    }
}
</script>
```

### Props

#### link
Type: `String`  
Required: `true`

Post link to the telegram post, usually the last part of the url. 
e.g. `t.me/telegram/83` -> `telegram/83`

#### width
Type: `String`  
Default: `100%`

Any valid html `width` attribute value

#### userpic
Type: `String`  
Default: `auto`  
Options: `['true', 'false', 'auto']`

Force post author's avatar visibiliy.

#### single
Type: `Boolean`  
Default: `false`

When post contains multiple pics, show only the first one by adding `single` query.