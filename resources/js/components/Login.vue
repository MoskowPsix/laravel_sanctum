<template lang="">
    <div class="w-25">
        <input v-model="email" type="email" name="email" placeholder="email" class="form-control mt-3 mb-3">
        <input v-model="password" type="password" name="password" placeholder="********" class="form-control mt-3 mb-3">
        <input @click.prevent="login()" type="submit" value="Login" class="btn btn-primary mt-3 mb-3">
    </div>
</template>
<script>
import { Axios } from 'axios';

export default {
    name: "Login",
    data() {
        return {
            email: null,
            password: null,
        }
    } ,

    methods: {
        login() {
            axios.get('/sanctum/csrf-cookie').then(response => {
                axios.post('/login', {email: this.email, password: this.password})
                .then(respons => {
                    // console.log(respons.config.headers['X-XSRF-TOKEN'])
                    localStorage.setItem('x_xsrf_token', respons.config.headers['X-XSRF-TOKEN'])
                    this.$router.push({name: 'user.personal'})

                })
            })
        }
    },
}
</script>
<style lang="">
    
</style>