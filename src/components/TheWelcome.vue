<script setup lang="ts">
import WelcomeItem from './WelcomeItem.vue'
import GetForm from './GetForm.vue'
import GetFormV2 from './GetFormV2.vue'
import PostForm from './PostForm.vue'
</script>

<template>
  <WelcomeItem>
    <template #heading>
      <h2>Department</h2>
    </template>
    <template #default>
<!--      <PostForm/>-->
      <GetForm/>
<!--      <GetFormV2/>-->
    </template>
  </WelcomeItem>

</template>
