<template>
  <div class="content">
    <div class="bg"
      :style = "{ 'background-image': `url(${markdownContent.attributes.backgroundImage})` }"
    >
    </div>
    
    <div v-html="markdownContent.content" class="text"></div>
  </div>
</template>
<script lang="ts">
export default {
  props: ['markdownContent'],
};
</script>
