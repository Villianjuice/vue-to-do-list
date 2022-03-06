<template>
  <h1>Это мои задачи</h1>
  <div v-if="projects.length > 0">
    <div v-for="project in projects" :key="project.id">
      <Project @handleDelete="handleDeleteProject" @handleUpdate="handleUpdateProject" :project="project"/>
    </div>
  </div>
</template>

<script>
import Project from '@/components/Project.vue'
export default {
    components: {Project},
    data() {
      return {
        projects: [] //Здесь будем хранить все задачи
      }
    },
    methods: {
      async getProjects() {
        // Эта функция будет получать ланные с бека
        const response = await fetch ('http://localhost:3001/projects');
        const json = await response.json();

        this.projects = await json // сохранили данные полученные с бека в переменную projects
      },
      handleDeleteProject(id) {
        this.projects = this.projects.filter(project => project.id !== id)
      },
      handleUpdateProject(id) {
        const project = this.projects.find(project => project.id === id)
        project.complete = !project.complete
      }
    },

    
    mounted() {
      this.getProjects()
    }
}
</script>

<style>

</style>