<template>
  <!-- prettier-ignore -->
  <iframe
    :src="'https://player.vimeo.com/video/' + videoid + '?autoplay=' + autoplay + '&muted=true'"
    width="640"
    height="360"
    frameborder="0"
    allow="autoplay"
    transparent="true"
    autopause="true"
    loop="true"
    muted="true"
    playsinline="true"
    title="false"
    webkitallowfullscreen
    mozallowfullscreen
    allowfullscreen
  />
</template>

<script>
export default {
  // ID ex 454674801
  // Autoplay true || false
  props: {
    videoid: String,
    autoplay: String
  }
}
</script>
