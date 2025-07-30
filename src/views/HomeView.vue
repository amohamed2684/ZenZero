<template>
  <div class="home">
    <div v-if="projects.length">
      <FilterNav @filter="currentFilter = $event" :current-filter="currentFilter" />
      <div v-for="project in filteredProjects" :key="project.id">
        <ProjectCard 
          :project="project" 
          @delete="handleDelete" 
          @complete="handleComplete" 
          @edit="handleEdit"
        />
      </div>
    </div>
    <div v-else>
      <h2>loading projects</h2>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'HomeView',
  components: {
  },
  setup() {

  }
}
</script>
