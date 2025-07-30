<template>
  <div>
    <nav class="main-nav">
      <router-link :to="{name: 'Home'}">Projects</router-link>
      <router-link :to="{name: 'AddProject'}">Add a new project</router-link>
    </nav>
  </div>
</template>

<script>
export default {

}
</script>

<style>
  .main-nav {
    text-align: center;
    margin: 3em auto;
  }
  .main-nav a {
    display: inline-block;
    text-decoration: none;
    margin: 0 1em;
    color: #000;
    font-size: 1.2rem;
  }
  a.router-link-active {
    border-bottom: 2px solid #00ce89;
    padding-bottom: 0.25em;
  }
</style>