<template>
  <div>
    <form @submit.prevent="handleSubmit">
      <input v-model="title" type="text" required>
      <textarea v-model="details"></textarea>

      <input type="submit" value="Save Project">
    </form>
  </div>
</template>

<script>
export default {
  props: [
    'id'
  ],
  data() {
    return {
      title: '',
      details: '',
      uri: 'http://localhost:3000/projects/' + this.id,
    }
  },
  components: {
    
  },
  methods: {
    handleSubmit() {
      let project = {
        "title": this.title,
        "details": this.details
      };

      fetch(this.uri, {
       method: 'PATCH', 
       headers: { 'Content-Type': 'application/json' },
       body: JSON.stringify(project)
      }).then( () => {
          this.$router.push('/');
        }).catch(err => console.log(err.message));
    }
  },
  mounted() {
    fetch(this.uri)
      .then(res => res.json())
      .then(data => {
        this.title = data.title;
        this.details = data.details;
      })
      .catch(err => console.log(err.message));
  },
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