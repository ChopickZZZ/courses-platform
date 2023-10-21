<script setup>
const props = defineProps({
  videoId: {
    type: Number,
    required: true,
  },
});
</script>

<template>
  <iframe
    width="460"
    height="315"
    title="Video Player"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowFullscreen
    :src="`https://player.vimeo.com/video/${props.videoId}`"
  >
  </iframe>
</template>
