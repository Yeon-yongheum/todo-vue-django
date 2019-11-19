<template>
<div>
  <!-- form에 이벤트 리스너 달아서,
      1) 사용자 입력값 출력
      2) /api-token-auth/ 로 요청 보내서 토큰값 출력
 -->
    <form @submit.prevent="login">
        <label for="username">username: </label>
        <input v-model="credentials.username" type="text" id="username"> 
        <br>  
        <label for="password">password: </label>
        <input v-model="credentials.password" type="password" id="password">
        <br>
        <button type="submit">로그인</button>
    </form>
</div>
</template>

<script>
import axios from 'axios'
// 특정 폴더명으로 경로가 끝나게 되면, 폴더 내부의 index.js를 뜻함
import router from '../router'
export default {
    name: 'LoginForm',
    data() {
        return {
            credentials: {}
        }
    },
    methods: {
        login(){
            // this.$emit('login-event',this.credentials)
            // this.credentials = {}
        axios.post('http://127.0.0.1:8000/api-token-auth/', this.credentials)
            .then(response => {
                console.log(response)
                const token = response.data.token
                this.$session.start()
                this.$session.set('jwt',token)
                router.push('/')
            })
            .catch(error => {
                console.log(error)
            })
        },
    }
    
}
</script>

<style>

</style>