<template>
  <div>
    <form @submit.prevent="addTodo">
      <input type="text" v-model="title" name="title" placeholder="Add Todo ...." >
      <input type="submit" value="Add" class="btn" >
    </form>
  </div>
</template>

<script>
// import uuid from 'uuid';

export default {
  name: "AddTodo",
  data() {
    return {
      title: '',
    }
  },
  methods: {
    addTodo() {
      // e.preventDefault();
      const newTodo = {
        // id: uuid.v4(),
        title: this.title,
        completed: false
      }
      // Send up to parent to use
      this.$emit('add-todo', newTodo);
      this.title = '';
    }
  }
}
</script>

<style scoped>
  form {
    display: flex;
  }
  input[type="text"] {
    flex: 10;
    padding: 5px;
  }
  inpout[type="submit"] {
    flex: 2;
  }
</style>