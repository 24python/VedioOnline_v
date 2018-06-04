<template>
  <div>
    <ul class="art_li" v-for="art in msg" :key="art.title">
        <!--<img :src="'http://127.0.0.1:8000/media/'+art.head_img" alt="" width="250px">-->
        <h3> <router-link :to="{name:'articlecontent' ,params:{pk:art.pk}}">{{art.title}}</router-link></h3>
        <p>{{art.brief}}</p>
        <span>阅读人数：{{art.comment_num}}|</span>
        <span>点赞人数：{{art.agree_num}}|</span>
        <span>发布时间：{{art.pub_date}}</span>
    </ul>
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
        url: 'http://127.0.0.1:8000/api/v1/article/',
        method: 'GET'
      }).then(function (ret) {
        that.msg = ret.data.data
        console.log(that.msg)
      }).catch(function (ret) {
        alert('数据失败')
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
