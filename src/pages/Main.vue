<template>
         <div class="container">
            <h1> {{ username }} </h1>

            <p>email: {{ email }}</p>
            <p>senha: {{ password }}</p>
            <p>Endereço: {{ address }}</p>
            <button v-on:click="deleteUser()" class="btn">Deletar Usuário</button>
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
    width: 30%;
}
</style>

<script>


const axios = require('axios')
const URL = 'http://localhost:4000';
//const router = require('../router/index')

export default {
    data: function() {
        return{
            username:'',
            email: '',
            password: '',
            address: '',
        }
    },
    methods: {
        deleteUser: function(){
            console.log(this.username)
            axios({
                method: 'delete',
                url: `${URL}/user`,
                data: {
                    username: this.username
                }
            }).then((response) => {
                console.log('oi')
                this.$router.push('/')
                return response
            }).then((error) => {
                alert(error.response.data)
                return
            })
        
        }
    },
    beforeMount: function(){

            axios.get(`${URL}/user`).then((response) => {
                
                const user = response.data
                this.username = user.username
                this.email = user.email
                this.address = user.address
                this.password = user.password

                return
            }).catch((error) => {
                console.log(error.response)
                return
            })


    }
}
</script>