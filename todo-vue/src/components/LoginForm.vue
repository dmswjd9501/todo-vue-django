<template>
<!-- form에 이벤트 리스너 달아서, 
    1) 사용자 입력값 출력
    2) /api-token-auth/로 요청 보내서 토큰값 출력
 -->
<form class="login-form" @submit.prevent="login">
    <label for="username">ID : </label>
    <input v-model="credentials.username" type="text" id=username> <br>
    <label for="password">Password : </label>
    <input v-model="credentials.password" type="password" id=password>
    <button type="submit">로그인</button>
</form>
</template>

<script>
export default {
    name: 'LoginForm',
    data() {
        return {
            credentials: {}
        }
    },
    methods: {
        login() {
            this.$emit('login-event', this.credentials)
            this.credentials = {}
        }
    }

}
</script>

<style>

</style>