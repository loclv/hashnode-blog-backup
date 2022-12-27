# Introduce vue-advanced-cropper 🖼️ with Vue 3 - ts - Composition API

I just rewrite the minimum example in [vue-advanced-cropper homepage](https://norserium.github.io/vue-advanced-cropper/) with Vue 3, TypeScript and [Composition API](https://vuejs.org/guide/extras/composition-api-faq.html).

## Preparing

A new project of Vue 3 with TypeScript, `pnpm` - package manager or npm, yarn...

Install [vue-advanced-cropper - vue-next branch for Vue 3](https://github.com/Norserium/vue-advanced-cropper/tree/vue-next):

```sh
pnpm add vue-advanced-cropper@next
pnpm dev
```

Source-code detail in [my repository - loclv/vue3-img-cropper](https://github.com/loclv/vue3-img-cropper).

## Create simple app

```vue
<template>
  <div id="app">
    <Cropper
      class="cropper"
      :src="img"
      :stencil-props="{
        aspectRatio: 10 / 12,
      }"
      @change="change"
    />
  </div>
</template>

<script lang="ts" setup>
import { Cropper, type Coordinates } from "vue-advanced-cropper"
import "vue-advanced-cropper/dist/style.css"

/**
 * Photo by [Vasilis Karkalas](https://www.pexels.com/@vasilis-karkalas-155349971/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from Pexels
 */
const img = "https://images.pexels.com/photos/11301535/pexels-photo-11301535.jpeg"

const change = ({ coordinates, canvas }: { coordinates: Coordinates; canvas: HTMLCanvasElement}) => {
  console.log("🌳 ~ coordinates", coordinates)
  console.log("🚀 ~ canvas", canvas)
}
</script>

<style scoped>
.cropper {
  height: 600px;
}
</style>
```

## Output

![Screen Shot 2022-05-22 at 12.46.47.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1653198481635/-lEF9WmZv.png align="left")