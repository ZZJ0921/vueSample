<template>
  <LoginPage/>
</template>

<script lang="ts" setup>
import LoginPage from './components/LoginPage.vue';
import apiClient from './http';

apiClient.post('/api/create_user?username=jack&password=redballoon');

</script>
