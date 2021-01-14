<template>
<!--  <div class="avatar" v-for="item in resume" :key=item.id>-->
<!--    <img v-if="item.type === 'avatar'" :src=item.content>-->
<!--  </div>-->
  <div  class="avatar">
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
