<template>
  <div>
    这是helloWorld页面
  </div>
</template>

<script>

export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      active:0,
      stepsData:
      [
        {title:'步骤1'},
        {title:'步骤2'},
        {title:'步骤3'}
      ]
    }
  },
  created(){

  },
  mounted(){
 // this.UserSin()
  },
  methods:{
    UserSin(){
      sessionStorage.header = 'application/json;charset=UTF-8';
      let params={
          "AccountCode": "esf_dev",
          "Login": "zt",
          "Pwd": "123456"
      };
      this.$post('http://quickcq.com/api/auth/signin',params).then(res=>{
      console.log(res);
      });
    },

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.aa{
  width: 900px;
  height: 300px;
  background-color: #42b983;
}
</style>
