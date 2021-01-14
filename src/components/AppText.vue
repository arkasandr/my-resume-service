<template>
<!--  <div class="text" v-for="item in resume" :key=item.id >-->
<!--  <p v-if="item.type === 'text'">-->
<!--    {{ item.content}}-->
<!--  </p>-->
<!--  </div>-->
  <div class="text">
  <p>
    {{ resume }}
  </p>
  </div>
</template>

<script>
export default {
  name: 'AppText',
  props: [
    'resume'
  ]
}
</script>

<style scoped>

</style>
