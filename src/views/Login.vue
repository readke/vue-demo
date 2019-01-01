<template>
  <div>
    <form action v-if="!isReg">
      <div>用户名：</div>
      <input type="text" v-model="username">
      <div>密码：</div>
      <input type="password" v-model="password">
      <div>
        <button type="button" @click="login()">登录</button>
        <button type="button" @click="reg()">注册</button>
      </div>
    </form>
    <form action v-else>
      <div>用户名：</div>
      <input type="text" v-model="username">
      <div>密码：</div>
      <input type="password" v-model="password">
      <div>重复密码：</div>
      <input type="password" v-model="repeat">
      <div>
        <button type="button" @click="addUser()">确定</button>
        <button type="button" @click="cancel()">取消</button>
      </div>
    </form>
  </div>
</template>
<script>
export default {
  name: 'Login',
  data () {
    return {
      isReg: false,
      username: '',
      password: '',
      repeat: ''
    }
  },
  methods: {
    login () {
      if (this.username === localStorage.getItem('username') && this.password === localStorage.getItem('password')) {
        this.name = ''
        this.password = ''
        this.$router.push('/home/list')
      } else {
        alert('用户名或密码错误')
      }
    },
    reg () {
      console.log('register')
      this.isReg = true
    },
    addUser () {
      if (this.password !== this.repeat) {
        alert('两次密码输入不一致')
        return
      }
      localStorage.setItem('username', this.username)
      localStorage.setItem('password', this.password)
      this.name = ''
      this.password = ''
      this.repeat = ''
      this.isReg = false
    },
    cancel () {
      this.isReg = false
    }
  }
}
</script>
<style scoped>
</style>
