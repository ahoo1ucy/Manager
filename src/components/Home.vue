<template>
  <div id="home">
      <h1>主页</h1>
  </div>
</template>

<script>
    export default{
        name: 'home',
        data(){
            return{

            }
        },
        mounted(){
            //传入cookie到服务器方便跳转或重定向
            var token = $.cookie('user_loginToken');
            if(token == null || token == ''){
                this.$router.push('/Login');
            }else{
                $.post("")
            }
        }
    }
</script>