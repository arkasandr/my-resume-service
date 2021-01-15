<template>
  <div class="container">
    <app-alert :alert="alert" @close="alert = null"></app-alert>
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

      <app-loader v-if="commentsLoading"></app-loader>
      <app-comments :comments="comments"></app-comments>

    </div>
  </div>
</template>

<script>

import AppComments from './components/AppComments'
import axios from 'axios'
import AppLoader from './components/AppLoader'
import AppControl from './components/AppControl'
import AppResume from './components/AppResume'
import AppAlert from './components/AppAlert'

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
      text: '',
      alert: null
    }
  },

  methods: {
    loadComments () {
      try {
        this.commentsLoading = true
        setTimeout(async () => {
          const response = await axios.get('https://jsonplaceholder.typicode.com/comments?_limit=42')
          if (!response.data) {
            throw new Error('Комментарии отсутствуют')
          }
          this.comments = response.data
          this.commentsLoading = false
        }, 1500)
        this.alert = {
          type: 'primary',
          title: 'Успешно!',
          text: 'Комментарии загружены!'
        }
      } catch (e) {
        this.alert = {
          type: 'danger',
          title: 'Ошибка!',
          text: e.message
        }
      }
    },

    async updateResume (type, content) {
      try {
        const response = await fetch('https://my-resume-service-default-rtdb.firebaseio.com/resume.json', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            type: type,
            content: content
          })
        })
        const firebaseData = await response.json()
        console.log('updateResume in firebase', firebaseData)
        await this.loadResume()
      } catch (e) {
        this.alert = {
          type: 'danger',
          title: 'Ошибка!',
          text: e.message
        }
      }
    },

    async loadResume () {
      try {
        this.commentsLoading = true
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
        this.commentsLoading = false
        this.alert = {
          type: 'primary',
          title: 'Успешно!',
          text: 'Ваше резюме готово!'
        }
        this.commentsLoading = false
      } catch (e) {
        this.alert = {
          type: 'danger',
          title: 'Ошибка!',
          text: e.message
        }
        this.commentsLoading = false
      }
    }

  },

  components: {
    'app-comments': AppComments,
    'app-loader': AppLoader,
    'app-control': AppControl,
    'app-resume': AppResume,
    'app-alert': AppAlert
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
