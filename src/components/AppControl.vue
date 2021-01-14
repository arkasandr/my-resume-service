<template>
  <form class="card card-w30" @submit.prevent="updateResume">
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

    <button class="btn primary" :disabled="addButtonDisable">Добавить</button>
  </form>
</template>

<script>
export default {
  name: 'AppControl',
  emits: {
    updateResume: (data) => {
      if (typeof data === 'object') {
        return true
      } else {
        console.warn('Invalid submit event payload!')
        return false
      }
    }
  },
  data () {
    return {
      type: 'title',
      content: ''
    }
  },

  computed: {
    addButtonDisable () {
      return this.content.length < 4
    }
  },

  methods: {
    updateResume () {
      // if (this.type !== 'combo') {
      //   data = {type: this.type, value: this.value}
      // } else {
      const data = {
        type: this.type,
        text: this.content
      }
      // }
      this.$emit('updateResume', data)
      this.type = 'title'
      this.content = ''
    }
  }
}
</script>

<style scoped>

</style>
