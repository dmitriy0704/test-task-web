<script setup lang="ts">
import WelcomeItem from '../WelcomeItem.vue'
import GetForm from './GetDepartment.vue'
import CreateDept from "./CreateDepartment.vue";
</script>

<template>
  <WelcomeItem>
    <template #heading>
      <div class="head">
        <h2>Отделы</h2>
      </div>
    </template>
    <template #default>

      <div class="form-wrap">
        <div class="item">
          <CreateDept/>
        </div>
        <div class="item">
          <GetForm/>
        </div>
      </div>
    </template>
  </WelcomeItem>

</template>

<style>
.head{
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 30px;
}
.form-wrap{
  display: flex;
  justify-content: space-around;
  align-items: center;
}
</style>

