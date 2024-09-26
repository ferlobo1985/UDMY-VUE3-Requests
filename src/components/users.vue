<template>
    <div class="row">

        <div class="col-auto mb-4"
            v-for="(user) in data.users"
            :key="user.id"
        >
            <div class="card" style="width: 14rem;">
                <img 
                    class="card-img-top" 
                    :src="'https://placebeard.it/300/300?'+ user.id"
                    alt="Card image cap"
                >
                <div class="card-body">
                    <div class="card-text">
                        <strong>Name:</strong> {{ user.name }}
                    </div>
                    <div class="card-text">
                        <strong>Lastname:</strong>  {{ user.lastname }}
                    </div>
                </div>
            </div>
         </div>

    </div>
</template>

<script setup>
    import axios from 'axios';
    import { onMounted, reactive } from 'vue';

    const data = reactive({
        users:[]
    })

    const loadUsers = () => {
        axios.get(`http://localhost:3004/users`)
        .then(response=>{
            data.users = response.data;
        })
        .catch(error =>{
            console.log(error)
        })
    }

    onMounted(()=>{
        loadUsers();
    })

</script>