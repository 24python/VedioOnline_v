<template>
  <div>
    <h3>{{msg.title}}</h3>
    <p><button @click="zan(msg.pk)">{{msg.agree_num}}</button></p>

    <p>{{msg.content}}</p>
  </div>
</template>

<script>
export default {
  name: 'article',
  data () {
    return {msg: 'test'}
  },
  created () {
    this.initCours()
  },
  methods: {

    initCours () {
      let that = this
      this.$axios.request({
        url: 'http://127.0.0.1:8000/api/v1/article/' + this.$route.params.pk,
        method: 'GET'
      }).then(function (ret) {
        that.msg = ret.data.data
        console.log(that.msg)
      }).catch(function (ret) {
        alert('数据失败')
      })
    },

    zan (pk) {
      let that = this
      this.$axios.post('http://127.0.0.1:8000/api/v1/zan/', {
        pk: pk,
        k: '123'
      })
        .then(function (response) {
          that.msg.agree_num = response.data
        })
        .catch(function (error) {
          console.log(error)
        })
    }
  }
}
</script>

<style >
  .art_li{
    border: solid 1px green;
  }
</style>
