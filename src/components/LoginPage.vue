<template>
  <a-card bordered="false" style="width: 500px">
    <h1 style="text-align: center;">LoginPage</h1>
    <div>
      <a-form
          :model="formState"
          name="basic"
          :label-col="{ span: 8 }"
          :wrapper-col="{ span: 16 }"
          autocomplete="off"
      >
        <a-form-item
            label="Username"
            name="username"
            :rules="[{ required: true, message: 'Please input your username!' }]"
        >
          <a-input v-model:value="formState.username" />
        </a-form-item>

        <a-form-item
            label="Password"
            name="password"
            :rules="[{ required: true, message: 'Please input your password!' }]"
        >
          <a-input-password v-model:value="formState.password" />
        </a-form-item>

        <a-form-item :wrapper-col="{ offset: 8, span: 16 }">
          <a-button type="primary" html-type="submit" @click="submit()" :disabled="isSubmitActive">登陆</a-button>
        </a-form-item>
      </a-form>
    </div>
  </a-card>
</template>

<script lang="ts" setup >
import apiClient from '../http';
import {computed, reactive} from 'vue'

interface FormState {
  username: string;
  password: string;
}
const formState = reactive<FormState>({
  username: '',
  password: '',
});

const submit = async () => {
  await apiClient.post(`http://127.0.0.1:7001/api/user/login?username=${formState.username}&password=${formState.password}`).then(response => {
    alert(response.data.message+"\nToken: " + response.data.data.token);
  }).catch(error => {
    alert(error.response.data.message)
  })
}

const isSubmitActive = computed(() => {
  return formState.username === '' || formState.password === '';
})
</script>

