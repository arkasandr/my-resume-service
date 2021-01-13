<template>
  <div class="card">
    <h2>Комментарии</h2>
    <ul class="list">
      <li class="list-item" v-for="item in comments" :key="item.id">
        <div>
          <p><strong>{{ item.email }}</strong></p>
          <small>{{item.body}}</small>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'AppComments',

  props: [
    'comments'
  ]
}
</script>

<style scoped>

</style>
