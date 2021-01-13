<template>

  <div class="container column">

  </div>

  <div class="container">
    <p>
      <button class="btn primary" v-if="comments.length === 0" @click="loadComments">Загрузить комментарии</button>
    </p>
<app-comments :comments="comments"></app-comments>
    <!--    <div class="loader"></div>-->
  </div>

</template>

<script>

import AppComments from './components/AppComments'
import axios from 'axios'

export default {

  data () {
    return {
      comments: [],
      resume: ['app-title', 'app-title'],
      addButton: '',
      selectedType: ''
    }
  },

  // computed: {
  //   addButtonDisable() {
  //     return this.addButton.length < 4
  //   }
  // },

  methods: {
    async loadComments () {
      const response = await axios.get('https://jsonplaceholder.typicode.com/comments?_limit=42')
      this.comments = response.data
    }
  },

  components: {
    'app-comments': AppComments
  }

}
</script>

<style>
  .avatar {
    display: flex;
    justify-content: center;
  }

  .avatar img {
    width: 150px;
    height: auto;
    border-radius: 50%;
  }
</style>
