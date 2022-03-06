<template>
  <form @submit.prevent="handleSubmit">
      <label>Название задачи:</label>
      <input v-model="title"  type="text">
      <label>Описание:</label>
      <textarea v-model="details" name="" id="" cols="30" rows="10"></textarea>
      <button>Создать задачу</button>
  </form>
</template>

<script setup>
import {ref} from "@vue/reactivity";
import {useRouter} from "vue-router"

const router = useRouter()

const title = ref('')
const details = ref('')

const handleSubmit = async () => {
    const newProject = {
        title: title.value,
        details: details.value,
        complete: false
    }

    await fetch('http://localhost:3001/projects', {
        method: 'POST',
        body: JSON.stringify(newProject),
        headers: {"Content-Type": "application/json"},

    })

    router.push('/')
}

</script>

<style>
form{
    background: white;
    padding: 20px;
    border-radius: 20px;
}
label {
    display: block;
    color: #bbb;
    text-transform: uppercase;
    font-size: 14px;
    font-weight: 700;
    letter-spacing: 1px;
    margin: 20px 0 10px 0;
}
input{
    padding: 10px;
    border: 0;
    border-bottom: 1px solid #ddd;
    width: 100%;
    box-sizing: border-box;
}
textarea{
    border: 1px solid #ddd;
    padding: 10px;
    width: 100%;
    box-sizing: border-box;
    height: 100px;
}
form button {
    display: block;
    margin: 20px auto 0;
    background: #00ce89;
    color: #fff;
    padding: 10px;
    border: none;
    border-radius: 16px;
    cursor: pointer;
}
</style>