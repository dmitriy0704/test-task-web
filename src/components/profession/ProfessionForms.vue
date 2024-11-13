<script setup lang="ts">
import WelcomeItem from '../WelcomeItem.vue'
import GetForm from './GetProfessions.vue'
import CreateForm from "./CreateProfession.vue";
</script>

<template >
  <WelcomeItem>
    <template #heading>
      <div class="head">
        <h2>Профессии</h2>
      </div>
    </template>

    <template #default>
      <div class="form-wrap">
        <div class="item">
          <CreateForm/>
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
  justify-content: flex-start;
  align-items: flex-start;
}

.form-wrap div{
  margin-right: 30px;
}
</style>

