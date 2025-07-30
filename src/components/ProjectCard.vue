<template>
  <div class="project">
    <div class="actions">
      <h3 @click="showDetails = !showDetails">{{ project.title }}</h3>
      <div class="icons">
        <span @click="editProject" class="material-symbols-outlined">edit</span>
        <span @click="deleteProject" class="material-symbols-outlined">delete</span>
        <span @click="toggleComplete" class="material-symbols-outlined">check</span>
      </div>
    </div>
    <div v-if="showDetails" class="details">
      {{ project.details }}
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showDetails: false,
      uri: "http://localhost:3000/projects/" + this.project.id
    }
  },
  props: [
    'project'
  ],
  methods: {
    deleteProject() {
      fetch(this.uri, {method: 'DELETE'})
        .then(() => {
          this.$emit('delete', this.project.id)
        }).catch(err => console.log(err));
    },
    toggleComplete() {
      fetch(this.uri, {
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
          complete: !this.project.complete
        })
      }).then(() => {
        this.$emit('complete', this.project.id)
      }).catch(err => console.log(err));
    },
    editProject() {
      this.$router.push({name: 'EditProject', params: {'id': this.project.id}})
    }
  }
}
</script>

<style>
.project {
  margin: 1em auto;
  background-color: aliceblue;
  padding: 1em 2em;
  border-radius: 0.25em;
  box-shadow: 1px 2px 2px rgba(0, 0, 0, 0.5);
  border-left: 4px solid #00aaee;
}
h3 {
  cursor: pointer;
}
.actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.material-symbols-outlined {
  font-size: 24px;
  margin-left: 1em;
  color: #bbb;
  cursor: pointer;
}

.material-symbols-outlined:hover {
  color: #777;
}
</style>