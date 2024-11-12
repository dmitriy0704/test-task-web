<script setup lang="ts">
import {ref, onMounted} from 'vue'
import axios from 'axios'

// === GET === //

interface Departments {
  text: string
}

const dept_list = ref([] as Departments[])

async function fetchInitialDeptList() {
  const deptListResponse = await axios
      .get<Departments[]>('http://localhost:8080/api/dept?list')
  dept_list.value = deptListResponse.data
}

onMounted(async () => {
  await fetchInitialDeptList()
  await createDept()
})

// === POST === //

async function createDept() {

  const data = {'deptname': ''}
  const response = await axios
      .post('http://localhost:8080/api/dept', data);
}


</script>

<template>
  <div class="row">
    <div class="col-md-12">
      <h3 class="green">Все департаменты</h3>
    </div>
    <div class="col-md-6">
      <ul class="list-group">
        <li v-for="(item, index) in dept_list"
            :key="index"
            class="list-group-item">
          {{ index + 1 }}. {{ item.name }}
        </li>
      </ul>
    </div>
  </div>

  <div>
    <h3 class="green">Создать департамент</h3>
    <form v-on:submit.prevent="submitForm">
      <div class="form-group">
        <label for="name">Name</label>
        <br/><br/>
        <input type="text"
               class="form-control"
               id="name" placeholder="Dept"
               v-model="deptname">
        <br/><br/>
      </div>

      <div class="form-group">
        <button class="btn btn-primary">Submit</button>
      </div>
    </form>
  </div>
</template>

