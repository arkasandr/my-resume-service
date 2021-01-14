<template>
  <div class="card card-w70">
    <!--    <h1>Резюме Nickname</h1>-->
    <!--    <div class="avatar">-->
    <!--      <img src="https://cdn.dribbble.com/users/5592443/screenshots/14279501/drbl_pop_r_m_rick_4x.png">-->
    <!--    </div>-->
    <!--    <h2>Опыт работы</h2>-->
    <!--    <p>-->
    <!--      главный герой американского мультсериала «Рик и Морти», гениальный учёный, изобретатель, атеист (хотя в некоторых сериях он даже молится Богу, однако, каждый раз после чудесного спасения ссылается на удачу и вновь отвергает его существование), алкоголик, социопат, дедушка Морти. На момент начала третьего сезона ему 70 лет[1]. Рик боится пиратов, а его главной слабостью является некий - "Санчезиум". Исходя из того, что существует неограниченное количество вселенных, существует неограниченное количество Риков, герой сериала предположительно принадлежит к измерению С-137. В серии комикcов Рик относится к измерению C-132, а в игре «Pocket Mortys» — к измерению C-123[2]. Прототипом Рика Санчеза является Эмметт Браун, герой кинотрилогии «Назад в будущее»[3].-->
    <!--    </p>-->
    <h3 v-if="resume.size === 0">Добавьте первый блок, чтобы увидеть результат</h3>
    <!--    <app-title :resume="resume"></app-title>-->
    <!--    <app-subtitle :resume="resume"></app-subtitle>-->
    <!--    <app-avatar :resume="resume"></app-avatar>-->
    <!--    <app-text :resume="resume"></app-text>-->
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
    componentName () {
      const res = []
      this.resume.forEach(item => {
        // // )
        // // for (item in this.resume) {
        // if (item.type === 'title') {
        const type = 'app-' + item.type
        const content = item.content
        res.push({ type: type, content: content })
        // } else if (item.type === 'subtitle') {
        //   res.push('app-subtitle')
        // } else if (item.type === 'text') {
        //   res.push('app-text')
        // } else if (item.type === 'avatar') {
        //   res.push('app-avatar')
        // }
        console.log('type array', res)
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
