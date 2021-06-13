<template>
  <div class="container">
    <GlobalHeader :user="userData"></GlobalHeader>
    <column-list :list="list"></column-list>
    <form>
      <div class="mb-3">
        <label for="exampleInputEmail1" class="form-label">邮箱地址</label>
        <ValidateInput :rules="emailRules"></ValidateInput>
      </div>
      <div class="mb-3">
        <label for="exampleInputEmail1" class="form-label">邮箱地址</label>
        <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" v-model="emailRef.val" @blur="validateEmail">
        <div class="form-text" v-if="emailRef.error">{{emailRef.message}}</div>
      </div>
      <div class="mb-3">
        <label for="exampleInputPassword1" class="form-label">Password</label>
        <input type="password" class="form-control" id="exampleInputPassword1">
      </div>
      <div class="mb-3 form-check">
        <input type="checkbox" class="form-check-input" id="exampleCheck1">
        <label class="form-check-label" for="exampleCheck1">Check me out</label>
      </div>
      <button type="submit" class="btn btn-primary">Submit</button>
    </form>
  </div>
</template>

<script lang="ts">
import {defineComponent, reactive} from 'vue'
import 'bootstrap/dist/css/bootstrap.min.css'
import ColumnList, {ColumnProps} from "@/components/ColumnList.vue"
import GlobalHeader, { UserProps } from "@/components/GlobalHeader.vue";
import ValidateInput, { RulesProp } from "@/components/ValidateInput.vue";

const currentUser: UserProps = {
  id: 1,
  isLogin: true,
  name: '张三'
}

const testData: ColumnProps[] = [{
  id: 1,
  title: 'test1的专栏',
  description: '这是描述。简介',
  avatar: '../assets/logo.png'
},{
  id: 2,
  title: 'test2的专栏',
  description: '这是描述。简介',
  avatar: '../assets/logo.png'
},{
  id: 3,
  title: 'test3的专栏',
  description: '这是描述。简介',
  avatar: '../assets/logo.png'
},{
  id: 4,
  title: 'test3的专栏',
  description: '这是描述。简介',
  avatar: '../assets/logo.png'
}]

const emailReg = /^\w{3,}(\.\w+)*@[A-z0-9]+(\.[A-z]{2,5}){1,2}$/


export default defineComponent({
  name: 'App',
  components: {
    ColumnList,
    GlobalHeader,
    ValidateInput
  },
  setup() {
    const emailRules: RulesProp = [
      {type: 'required', message: '电子邮箱地址不能为空'},
      {type: 'email', message: '请输入正确的电子邮箱格式'}
    ]
    const emailRef = reactive({
      val: '',
      error: false,
      message: ''
    })
    const validateEmail = () => {
      console.log(emailReg.test(emailRef.val))
      if (emailRef.val.trim() === '') {
        emailRef.error = true
        emailRef.message = '请输入邮箱'
      } else if (!emailReg.test(emailRef.val)) {
        emailRef.error = true
        emailRef.message = '请输入合法的邮箱'
      } else {
        emailRef.error = false
        emailRef.message = ''
      }
    }

    return {
      list: testData,
      userData: currentUser,
      emailRules,
      emailRef,
      validateEmail
    }
  }
})
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

/*表单*/
form {
  text-align: left;
}
</style>
