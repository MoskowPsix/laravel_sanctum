<template lang="">
    <div class="w-25">
        <input v-model="email" type="name" name="name" placeholder="name" class="form-control mt-3 mb-3">
        <input v-model="email" type="email" name="email" placeholder="email" class="form-control mt-3 mb-3">
        <input v-model="password" type="password" name="password" placeholder="********" class="form-control mt-3 mb-3">
        <input v-model="password" type="password" name="password_confirmation" placeholder="********" class="form-control mt-3 mb-3">
        <input @click.prevent="registration()" type="submit" value="register" class="btn btn-primary mt-3 mb-3">
    </div>
</template>
<script>
export default {
    name: "Registration",
    data() {
        return {
            name: null,
            email: null,
            password: null,
            password_confirmation: null
        }
    },
    methods: {
        registration() {
            axios.get('/sanctum/csrf-cookie').then(response => {
                axios.get('/register', {name: this.name, email: this.email, password: this.password, password_confirmation: this.password_confirmation}).then(response => {
                    localStorage.setItem('x_xsrf_token', response.config.headers['X-XSRF-TOKEN'])
                    this.$router.push({name: 'user.personal'})
                }).catch(error => console.log(error))
            })
            .catch(error => {
                console.log(error.response)
            })
        }
    }
}
</script>
<style lang="">
    
</style>