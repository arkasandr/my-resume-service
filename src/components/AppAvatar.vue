<template>
  <div class="avatar">
    <img :src=resume>
  </div>
</template>

<script>
export default {
  name: 'AppAvatar',
  props: [
    'resume'
  ]
}
</script>

<style scoped>

</style>
