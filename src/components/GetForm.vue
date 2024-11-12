<script setup lang="ts">
    import { ref, onMounted } from 'vue'
    import axios from 'axios'

    interface AnimalFacts {
        text: string
    }
    const catFacts = ref([] as AnimalFacts[])
    const fetchingFacts = ref(false)
    async function loadMoreFacts() {
        fetchingFacts.value = true
        const catFactsResponse = await axios.get<AnimalFacts[]>('http://localhost:8080/api/dept?list')
        catFacts.value.push(...(catFactsResponse.data || []))
        fetchingFacts.value = false
    }
    async function fetchInitialCatFacts() {
        const catFactsResponse = await axios.get<AnimalFacts[]>('http://localhost:8080/api/dept?list')
        catFacts.value = catFactsResponse.data
    }
    onMounted(async () => {
        await fetchInitialCatFacts()
    })


    // ========== POST ==============//
    
  


</script>



<template>
    <div class="row">
        <div class="col-md-12">
            <h3 class="green">Все департаменты</h3>
        </div>
        <div class="col-md-6">
        <div>
            
      
        </div>    
        </div>
        <div class="col-md-6">
            <ul class="list-group">
                <li v-for="(item, index) in catFacts" :key="index" class="list-group-item">{{index + 1}}. {{item.name}}</li>
            </ul>
        </div>
        <div class="col-md-12 text-center">
                <button @click="loadMoreFacts" class="btn btn-md btn-primary">{{ fetchingFacts ? '...' : 'Load more' }}</button>
        </div>
    </div>
</template>


