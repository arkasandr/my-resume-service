<template>
  <div class="card card-w70">
    <h3 v-if="firstElementAdding">Добавьте первый блок, чтобы увидеть результат</h3>
    <div v-for="item in componentName" :key="item">
      <component :is="item.type" :resume="item.content"></component>
    </div>

  </div>
</template>

<script>

import AppTitle from './AppTitle'
import AppSubtitle from './AppSubtitle'
import AppAvatar from './AppAvatar'
import AppText from './AppText'

export default {
  name: 'AppResume',
  props: [
    'resume'
  ],
  data () {
    return {}
  },
  computed: {
    firstElementAdding () {
      return this.resume.size === 0
    },
    componentName () {
      const res = []
      this.resume.forEach(item => {
        const type = 'app-' + item.type
        const content = item.content
        res.push({ type: type, content: content })
      }
      )
      return res
    }
  },

  components: {
    'app-title': AppTitle,
    'app-subtitle': AppSubtitle,
    'app-avatar': AppAvatar,
    'app-text': AppText
  }
}
</script>

<style scoped>

</style>
