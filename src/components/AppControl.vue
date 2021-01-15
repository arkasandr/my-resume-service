<template>
  <form class="card card-w30" @submit.prevent="resetTextarea">
    <div class="form-control">
      <label for="type">Тип блока</label>
      <select id="type" v-model="type">
        <option value="title">Заголовок</option>
        <option value="subtitle">Подзаголовок</option>
        <option value="avatar">Аватар</option>
        <option value="text">Текст</option>
      </select>
    </div>

    <div class="form-control">
      <label for="value">Значение</label>
      <textarea id="value" rows="3" v-model="content"></textarea>
    </div>

    <button class="btn primary" :disabled="addButtonDisable" @click="resetTextarea">Добавить</button>
  </form>
</template>

<script>
export default {
  name: 'AppControl',
  emits: ['updateResume'],
  props: ['reset'],
  data () {
    return {
      type: 'title',
      content: ''
    }
  },
  methods: {
    resetTextarea () {
      this.$emit('updateResume', this.type, this.content)
      this.content = ''
    }
  },

  computed: {
    addButtonDisable () {
      return this.content.length < 4
    }
  }

}
</script>

<style scoped>

</style>
