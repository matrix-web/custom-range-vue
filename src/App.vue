<template>
  <div id="app">
    <range-slider v-model="range"/>
  </div>
</template>

<script>
import RangeSlider from '@/components/range-slider'

export default {
  name: 'App',
  data() {
    return {
      range: 0
    }
  },
  components: {
    RangeSlider
  }
}
</script>

<style>
*,
*::after,
*::before {
  box-sizing: border-box;
}

body {
  margin: 0;
  padding: 0;
}
</style>
