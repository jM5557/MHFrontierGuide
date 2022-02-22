<template>
    <a class = "clickable-image" :href = "src" target = "_blank">
        <img :alt = "alt" :src = "src" />
    </a>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
    name: "clickable-image",
    props: ["alt", "src"]
})
</script>