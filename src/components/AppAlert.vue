<template>
  <div class="alert" v-if="alert" :class="alert.type">
    <h3>{{ alert.title }}</h3>
    <div class="inline">
      <p>{{ alert.text }}</p>
      <button class="btn" :class="alert.type" @click="$emit('close')">Закрыть</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AppAlert',
  emits: ['close'],
  props: ['alert']
}
</script>

<style scoped>
  .inline {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
</style>
