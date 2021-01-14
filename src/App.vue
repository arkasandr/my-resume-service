<template>

  <div class="container column">
    <app-control
      @updateResume="updateResume"
    >
    </app-control>

    <app-resume
      :resume="resume"
    >
    </app-resume>
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
import AppControl from './components/AppControl'
import AppResume from './components/AppResume'

export default {

  data () {
    return {
      comments: [],
      resume: [],
      resumeLoading: false,
      commentsLoading: false,
      title: '',
      subtitle: '',
      avatar: '',
      text: ''
    }
  },

  computed: {

  },

  methods: {
    async loadComments () {
      this.commentsLoading = true
      const response = await axios.get('https://jsonplaceholder.typicode.com/comments?_limit=42')
      this.comments = response.data
      this.commentsLoading = false
    },

    async updateResume ({ type, text }) {
      const response = await fetch('https://my-resume-service-default-rtdb.firebaseio.com/resume.json', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({
          type: type,
          content: text
        })
      })
      const firebaseData = await response.json()
      console.log('updateResume in firebase', firebaseData)
      await this.loadResume()
    },

    async loadResume () {
      try {
        const response = await axios.get('https://my-resume-service-default-rtdb.firebaseio.com/resume.json')
        if (!response.data) {
          throw new Error('Резюме отсутствует')
        }
        this.resume = Object.keys(response.data).map(key => {
          return {
            id: key,
            ...response.data[key]
          }
        })
      } catch (e) {
        // this.alert = {
        //   type: 'danger',
        //   title: 'Ошибка!',
        //   text: e.message
        // }
        // this.loading = false
        console.log(e.message)
      }
    }

  },

  components: {
    'app-comments': AppComments,
    'app-loader': AppLoader,
    'app-control': AppControl,
    'app-resume': AppResume
  },

  mounted () {
    this.loadResume()
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
