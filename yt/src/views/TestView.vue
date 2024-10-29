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
<table border="1">
    <tr>
        <th>name</th>
        <th>age</th>
        <th>gender</th>
        <th>address</th>
        <th>phone no.</th>
        <th>action</th>
    </tr>
    <tr v-for="user in users" :key="users._id">
        <td>{{ user.name }}</td>
        <td>{{ user.age }}</td>
        <td>{{ user.gender }}</td>
        <td>{{ user.address }}</td>
        <td>{{ user.phone }}</td>
        <td><button @click="deleteUser(user._id)">delete</button>
        <button @click="editUser(user)">edit</button></td>
    </tr>
</table>
    </div>
</template>
<script>
import axios from 'axios'
export default {
    data(){
        return {
            users:[],
            user: {
                name:'',
                age:'',
                gender:'',
                address:'',
                phone:'',
            }
        };
    },
    mounted(){
        this.getUsers();
    },
    methods:{
        async deleteUser(id){
            await axios.delete(`http://localhost:5000/api/users/${id}`);
            this.getUsers();
        },
        async getUsers(){
            const res = await axios.get('http://localhost:5000/api/users');
            this.users = res.data;
        },
        async createUser(){
            await axios.post('http://localhost:5000/api/users', this.user);
            this.user = {name:'', age:'', gender:'', address:'', phone:''};
            this.getUsers();
        },
        editUser(user){
            this.user = { ...user};
        }
    }
}
</script>