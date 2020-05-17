<template>
      <div class="container">
            <h2>Cadastro</h2>
            <p> Username: <input v-model="username" placeholder="Username"></p>
            <p>Email: <input v-model="email" placeholder="Email"></p>
            <p>Password: <input v-model="password" type="password" placeholder="Password"></p>
            <p>Endereço: <input v-model="address" type= "text" placeholder="Address"></p> 
            <br /><br />
            <button  v-on:click="signUp()"  class="btn">Cadastrar</button>
            <p> Já tem uma conta? <router-link to='/'> Clique aqui </router-link></p>
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

const axios = require('axios')
const URL = 'http://localhost:4000';

export default {

    data: function(){
        return{
            username: '',
            email: '',
            password: '',
            address: ''
        }
    },
    methods: {
        signUp: function(){

            axios.post(`${URL}/register`, {
            
                name: this.username,
                email: this.email,
                password: this.password,
                address: this.address
                
            }).then((response) => {
                console.log(response)
                this.$router.push('/')
                return
            }).catch((error) => {
                alert(error.response.data)
                return
            })
        }
   
    }
}
</script>