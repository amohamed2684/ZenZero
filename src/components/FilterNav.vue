<template>
  <div>
    <nav class="filter-nav">
      <button 
        @click="updateFilter('all')"
        :class="{ active: currentFilter === 'all' }"
      >All</button>
      <button 
        @click="updateFilter('ongoing')"
        :class="{ active: currentFilter === 'ongoing' }"
      >Ongoing</button>
      <button 
        @click="updateFilter('completed')"
        :class="{ active: currentFilter === 'completed' }"
      >Completed</button>
    </nav>
  </div>
</template>

<script>
export default {
  props: ['currentFilter'],
  methods: {
    updateFilter(by) {
      this.$emit('filter', by);
    }
  }
}
</script>

<style>
  .filter-nav button{
    background: none;
    border: none;
    color: #bbb;
    outline: none;
    margin-right: 1em;
    letter-spacing: 1px;
    font-weight: bold;
    cursor: pointer;
  }
  .filter-nav button.active {
    color: #555;
  }
</style>