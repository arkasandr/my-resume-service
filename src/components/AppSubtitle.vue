<template>
<!--  <div v-for="item in resume" :key = item.id>-->
<!--    <h1 v-if="item.type === 'subtitle'">{{ item.content}}</h1>-->
<!--  </div>-->
  <div >
    <h1>{{resume}}</h1>
  </div>
</template>

<script>
export default {
  name: 'AppSubtitle',
  props: [
    'resume'
  ]
}
</script>

<style scoped>

</style>
