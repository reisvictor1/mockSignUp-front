<template>
        <div class="container">
            <h2>Login</h2>
            <p> Username: </p>
            <input v-model="username" placeholder="Username">
            <p>Password:</p>
            <input v-model="password" type="password" placeholder="Password">
            <br /><br />
                <button v-on:click="Login()" class="btn">Login</button>
            <p> Não tem conta? <router-link to='/register'> Clique aqui </router-link></p>
        </div>
</template>


<style scoped>
.container{
    margin: 5% 25%;
    padding: 1% 0%;
    box-shadow: 0 10px 15px -3px rgba(0,0,0,.1),0 4px 6px -2px rgba(0,0,0,.05);
    text-align: center;
}



.btn{
    background-color: #3399ff;
    color: white;
    font-size: larger;
    text-align: center;
    border: 1px rgba(0,0,0,.1) solid;
    border-radius: 10px;
    height: 40px;
    width: 25%;
}

</style>

<script>

//const router = require('../router/index')
const axios = require('axios')
const URL = 'http://localhost:4000';

export default {
    data: function(){
        return {
            username: '',
            password: '',
            email: '',
            address: ''
        }
    },
    methods: {

        Login: async function(){

            axios.post(`${URL}/login`, {
                name: this.username,
                pass: this.password
            }).then((response) => {

                let user = response.data

                this.username = user.username
                this.email = user.email
                this.address = user.address
                this.password = user.password
                
                this.$router.push('/main')
                return

            }).catch((error) => {
                console.log(error.response)
                alert(error.response.data)
                return
            })
        }

    }
    
}
</script>