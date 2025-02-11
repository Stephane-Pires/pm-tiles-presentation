<script setup lang="ts">
const props = defineProps<{ class?: string; url: string }>()
</script>


<template>
        <iframe id="frame" class="w-full h-full" :src="url" />
  </template>

