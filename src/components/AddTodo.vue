<template>
  <div>
      <form @submit="addTodo">
          <input type="text" name="title"  v-model="title" placeholder="Add Todo ...">
          <input type="submit" value="Submit" class="btn">
      </form>
  </div>
</template>

<script>
export default {
    name: "AddTodo",
    data() {
        return {
            title : ''
        }
    },
    methods: {
        addTodo(e) {
            e.preventDefault();

            if(this.title) {
                const newTodo = {
                    title: this.title,
                    completed: false
                }

                this.$emit('add-todo', newTodo);

                this.title = '';
            } 
        }
    }
}
</script>

<style scoped>
    form {
        display: flex;
    }

    input[type="text"] {
        flex: 7;
        padding: 5px;
    }

    input[type="submit"] {
        flex: 3;
    }

    .btn {
        background-color: #008CBA; /* Green */
        border: none;
        color: white;
        padding: 15px 32px;
        text-align: center;
        text-decoration: none;
        display: inline-block;
        font-size: 16px;
        cursor: pointer;
    }

    .btn:hover {
        background-color: #134d61;
    }

    .btn:active {
        background-color: #134d61;
    }
</style>