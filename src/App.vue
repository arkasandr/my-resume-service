<template>

  <div class="container column">

  </div>

  <div class="container">
    <p>
      <button class="btn primary" v-if="comments.length === 0" @click="loadComments">Загрузить комментарии</button>
    </p>

    <app-loader v-if="commentsLoading"> </app-loader>
    <app-comments :comments="comments"></app-comments>

  </div>

</template>

<script>

import AppComments from './components/AppComments'
import axios from 'axios'
import AppLoader from './components/AppLoader'

export default {

  data () {
    return {
      comments: [],
      resumeLoading: false,
      commentsLoading: false,
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
      this.commentsLoading = true
      const response = await axios.get('https://jsonplaceholder.typicode.com/comments?_limit=42')
      this.comments = response.data
      this.commentsLoading = false
    }
  },

  components: {
    'app-comments': AppComments,
    'app-loader': AppLoader
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
