<template>
  <button 
    type = "button"
    v-bind:class = "`checkbox-item ${ (clicked) ? 'clicked' : '' }`"
    v-on:click="() => this.clicked = !this.clicked"
  >
    <span>
      {{ text }}
    </span>
  </button>
</template>
<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  props: ['text'],
  data: () => {
    return {
      clicked: false
    }
  }
})
</script>
