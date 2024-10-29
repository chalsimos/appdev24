<template>
    <div>
        <h1>Create User</h1>
        <form @submit.prevent="createUser">
            <label>name</label>
            <input type="text" v-model="user.name" placeholder="enter your name" required>
            <br><br><label>age</label>
            <input type="text" v-model="user.age" placeholder="enter your age" required>
            <br><br><label>gender</label>
            <input type="text" v-model="user.gender" placeholder="enter your gender" required>
            <br><br><label>address</label>
            <input type="text" v-model="user.address" placeholder="enter your address" required>
            <br><br><label>phone</label>
            <input type="text" v-model="user.phone" placeholder="enter your phone" required>
            <button type="submit">add user</button>
        </form>

    </div>
</template>
<script>
import axios from 'axios'
export default {
    data(){
        return {
            user: {
                name:'',
                age:'',
                gender:'',
                address:'',
                phone:'',
            }
        };
    },
    methods:{
        async createUser(){
            await axios.post('http://localhost:5000/api/users', this.user);
            this.user = {name:'', age:'', gender:'', address:'', phone:''};
            
        }
    }
}
</script>