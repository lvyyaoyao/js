<template>
    <div>
      <h1>课程列表</h1>
      <ul v-for="item in courseList">
        <li>{{item.title}}</li>
      </ul>
    </div>
</template>

<script>
  export default {
        name: "Course",
        data(){
          return{
            courseList:[
              {id:1,title:'Python基础'},
              {id:2,title:'Java基础'},
              {id:3,title:'Js基础'},
              {id:4,title:'C#基础'},
            ]
          }
        },
        mounted(){
          this.initCourse();
      },
        methods:{
           initCourse:function () {
              var that = this
              // 向后台发送ajax请求
              this.$axios.request({
                url: 'http://127.0.0.1:8000/api/v1/courses/',
                method: 'GET',
                responseType: 'json'
              }).then(function (arg) {
                // 成功之后
                if(arg.data.code === 1000){
                    that.courseList = arg.data.data
                }else{
                  alert(arg.data.error);
                }
              }).catch(function (arg) {
              })
          }
        }

    }
</script>

<style scoped>

</style>
