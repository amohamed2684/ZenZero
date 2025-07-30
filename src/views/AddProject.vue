<template>
  <div>
    <form @submit.prevent="handleSubmit">
      <input v-model="title" type="text" placeholder="Title" required>
      <textarea v-model="details" placeholder="Details"></textarea>

      <input type="submit" value="Add Project">
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: '',
      details: ''
    }
  },
  methods: {
    handleSubmit() {
      let project = {
        "title": this.title,
        "details": this.details,
        "complete": false
      }

      fetch("http://localhost:3000/projects", {
       method: "POST", 
       headers: { 'Content-Type': 'application/json' },
       body: JSON.stringify(project)
      }).then( () => {
          this.$router.push('/');
        }).catch(err => console.log(err.message));
    }
  }
}
</script>

<style>
  form {
    background-color: whitesmoke;
    padding: 1.5em;
    border-radius: 1em;
  }

  input, textarea {
    padding: 1em;
    border: 0;
    border-bottom: 1px solid #ddd;
    width: 100%;
    box-sizing: border-box;
  }
  textarea {
    height: 100%;
  }
  input[type="submit"] {
    display: block;
    margin: 1.5em auto 0;
    background-color: #00ce89;
    color: white;
    padding: 1em;
    border: 0;
    border-radius: 6px;
  }
</style>