<script>

import axios from 'axios';

export default {
    name: 'PostFormAxios',
    data(){
        return{
            form: {
                name: '',
            }
        }
    },
    methods:{
        submitForm(){
            axios.post('http://localhost:8080/api/dept', this.form)
                 .then((res) => {
                     //Perform Success Action
                 })
                 .catch((error) => {
                     // error.response.status Check status code
                 }).finally(() => {
                     //Perform action in always
                 });
        }
    }
}

</script>


<template>
    <div>
        <h3 class="green">Создать департамент</h3>
            <form v-on:submit.prevent="submitForm">
                <div class="form-group">
                    <label for="name">Name</label>
                    <br/><br/>
                    <input type="text" class="form-control" id="name" placeholder="Dept" v-model="form.name">
                    <br/><br/>
                </div>
                               
                <div class="form-group">
                    <button class="btn btn-primary">Submit</button>
                </div>
            </form>
    </div>
</template>
