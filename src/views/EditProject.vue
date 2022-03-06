<template>
  <form @submit.prevent="handleSubmit">
      <label>Название задачи:</label>
      <input v-model="title"  type="text">
      <label>Описание:</label>
      <textarea v-model="details" name="" id="" cols="30" rows="10"></textarea>
      <button>Редактировать задачу</button>
  </form>
</template>

<script setup>
import {ref} from "@vue/reactivity";
import {onMounted} from "@vue/runtime-core"
import {useRouter} from "vue-router"

const props = defineProps({
    id: {
        type: String
    }
})

const router = useRouter()

const title = ref('')
const details = ref('')

const handleGetProjectData = async() => {
    const response = await fetch('http://localhost:3001/projects/' + props.id )
    const json = await response.json()

    title.value = json.title
    details.value = json.details
}

onMounted(() => {
    handleGetProjectData()
})

</script>