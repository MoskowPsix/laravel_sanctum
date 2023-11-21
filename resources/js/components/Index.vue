<template lang="">
    <div class="mt-5">
        <h2>Sanctum App</h2>
        <div><router-link v-if="localStorage.getItem('x_xsrf_token')" :to="{name: 'index'}">Index</router-link></div>
        <div><router-link v-if="token" :to="{name: 'get'}">Get</router-link></div>
        <div><router-link v-if="!token" :to="{name: 'user.login'}">Login</router-link></div>
        <div><router-link v-if="!token" :to="{name: 'user.registration'}">Registration</router-link></div>
        <div><router-link v-if="token" :to="{name: 'user.personal'}">Personal</router-link></div>
    <div v-if="token"><a @click.prevent="logout()" href="#">Logout</a></div>
    </div>
        <router-view/>
</template>
<script>

export default {
    name:'Index',
    data() {
        return {
            token: null
        }
    },
    mounted() {
            this.getToken()
    },
    // beforeUpdate() { // Не срабатывает хз почему
    //         this.getToken()
    // },
    updated() { // Не срабатывает хз почему
        this.$nextTick(function () {
            // this.getToken()
            console.log('yes')
        })
    },
    methods: {
        logout() {
            axios.post('/logout').then(response => {
                localStorage.removeItem('x_xsrf_token')
                this.$router.push({name: 'user.login'})
            })
            .catch(err => {
                console.log(err.response)
            })
        },
        getToken() {
            // console.log('yes', this.token)
            this.token = localStorage.getItem('x_xsrf_token')
        }
    },
}
</script>
<style lang="">
    
</style>