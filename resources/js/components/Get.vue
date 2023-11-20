<template lang="">
    <div>
        Get
    </div>
</template>
<script>
import { Axios } from 'axios';

export default {
    name: 'Get',

    mounted() {
        this.getData()
    },

    methods: {
        getData() {
            axios.get('/api/get').then(response => {
                console.log(response)
            })
            .catch(err => {
                console.log(err.response)
            })
        }
    }
}
</script>
<style lang="">
    
</style>