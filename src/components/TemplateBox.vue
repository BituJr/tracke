<template>
  <div class="box has-text-weight-bold">
    <slot></slot>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: 'TemplateBox'
});
</script>

<style scoped>
    .box {
        background: #ADD8E6;
    }
</style>