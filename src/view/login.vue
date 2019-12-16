<template>
  <div class="login" v-if="f==false">
    <div class="ig">
      <img src="../assets/后台.png" alt="图片加载失败" />
      <div></div>
    </div>
    <h1 class="h2">渠道商管理平台</h1>
    <form class="form">
      <select class="select">
        <option value>管理员</option>
        <option value>企业</option>
        <option value>平台</option>
      </select>
      <input type="text" placeholder="账号" v-model="name" />
      <input type="text" placeholder="密码" v-model="password" />
      <input type="button" value="登录" @click="logointo()" />
    </form>
  </div>
   <div v-else class="ok">
    <i class="el-icon-success size animated shake"></i>
    <p class="msg animated fadeInLeft">登录成功</p>
  </div>
</template>
<script>
export default {
  data() {
    return {
      f: false,
      name: "",
      password: ""
    };
  },
  methods: {
    //登录
    logointo() {
      //收集表单数据
      let { name, password } = this;
      // 调用 ajax 接口 查询数据库用户密码是否正确
       this.axios
        .post("/login", {
          name: name,
          password: password
        })
        .then(res => {
          console.log(res.data);
          if(res.data.err_code==200){
            localStorage.setItem("houtaitoken",JSON.stringify({id:res.data.id,token:res.data.token}))
            //跳转到base页面
            this.f=true;//显示div
            setTimeout(()=>{
              
              this.$router.push({ name: "base" });
            },3000)
          }else{
            this.name="",
            this.password=""
          }
        });
    }
  }
};
</script>
<style >
* {
  margin: 0;
  padding: 0;
}

.select {
  border: 1px solid #ccc;
  line-height: 40px;
  color: #666;
  font-size: 20px;
  margin-bottom: 10px;
  /* padding: 15px; */
}

input {
  height: 25px;
  margin-bottom: 5px;
}
.ok {
  height: 100vh;
  width: 100px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  /* align-content: center; */
}
.msg {
  text-align: center;
}
.size {
  font-size: 100px;
}
.ig {
  width: 100px;
  height: 100px;
  margin: 0 auto;
  background: red;
}
.ig > img {
  width: 100%;
  height: 100%;
}
.h2 {
  text-align: center;
}
.login {
  width: 70%;
  height: 100vh;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  border: 1px solid black;
}
.form {
  width: 50%;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
}
</style>