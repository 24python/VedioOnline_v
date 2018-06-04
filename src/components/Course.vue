<template>
  <div>
    <h1>课程列表</h1>

    <div v-for="row in courseList" :key="row.name">
      <div style="width: 350px;float: left">
        <p>{{row.course_img}}</p>
        <h3><router-link :to="{name:'detail',params:{id:row.id}}">{{row.name}}</router-link></h3>
        <p>{{row.brief}}</p>
        <p>{{row.period}}</p>
        <p>{{row.level}}</p>

      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'index',
  data () {
    return {
      courseList: [

      ]
    }
  },
  mounted: function () {
    // vue页面刚加载时自动执行
    this.initCourse()
  },
  methods: {
    initCourse: function () {
      /*
        this.courseList = [
          {id:1,title:'Python全栈'},
          {id:2,title:'Linux运维'},
          {id:3,title:'金融分析'},
        ]
        */

      // 通过ajax向接口发送请求，并获取课程列表
      // axios 发送ajax请求
      // npm install axios --save
      // 第一步：在main.js中配置
      // 第二步：使用axios发送请求
      var that = this

      this.$axios.request({
        url: 'http://127.0.0.1:8000/api/v1/course/',
        method: 'GET'
      }).then(function (ret) {
        // ajax请求发送成功后，获取的响应内容
        console.log(ret.data)
        if (ret.data.code === 1000) {
          that.courseList = ret.data.data
        }
      }).catch(function (ret) {
        // ajax请求失败之后，获取响应的内容
      })
    }
  }
}
</script>

<style scoped>

</style>
