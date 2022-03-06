<template>
  <div class = "project" :class="{completed: project.complete}">
      <div class="actions">
          <h3 @click="handleShowDetails">{{project.title}}</h3>
          <div class="icons">
              <router-link :to="`/edit-project/${project.id}`">
                  <span class="material-icons">edit</span>
              </router-link>
              <span @click="handleDeleteProject" class="material-icons">delete</span>
              <span @click="handleUpdateProject" class="material-icons tick">done</span>
          </div>
      </div>
      <div v-if="showDetails" class="details"> 
          <p>{{project.details}}</p>
      </div>
  </div>
</template>

<script>
export default {
    props: ['project'],
    data() {
        return {
            showDetails: false,
            uri: 'http://localhost:3001/projects/' + this.project.id
        }
    },
    methods: {
        handleShowDetails() {
            this.showDetails = !this.showDetails
        },
        async handleDeleteProject() {
            await fetch(this.uri, {
                method: 'DELETE'
            })
            this.$emit('handleDelete', this.project.id)
        },
        async handleUpdateProject() {
            await fetch(this.uri, {
                method: 'PATCH',
                headers: {"Content-Type": "application/json"},
                body: JSON.stringify({complete: !this.project.complete})
            })
            this.$emit('handleUpdate', this.project.id)
        }
    }
}
</script>

<style>
.project {
    margin: 20px auto;
    background: #fff;
    padding: 10px 20px;
    border-radius: 4px;
    box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.05);
    border-left: 4px solid #e90074;
}
.project h3{
    cursor: pointer;
}
.actions{
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.icons .material-icons{
    font-size: 24px;
    margin-left: 24px;
    color: #bbb;
    cursor: pointer;
}
.material-icons:hover {
    color: #777;
}
.project.completed {
    border-left: 4px solid #00ce89;
}
.project.completed .tick{
    color: #00ce89;
}
</style>