<script>
  export default {
    data() {
    return {
      newtodo: '',
      todos: [],
    };
  },
    methods: {
      async ListTodos() {
        const response = await fetch("http://127.0.0.1:8080/todos", { method: "GET" });
        const data = await response.json();
        this.todos = data.data
      },
      
      async AddTodo() {
        const requestOptions = {
          method: "PUT",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({ title: this.newtodo })
        };
        const response = await fetch("http://127.0.0.1:8080/todos", requestOptions);
        const data = await response.json();
        this.ListTodos();
        this.newtodo = '';
        
      },
      
      async CompleteTodo(id) {
        const requestOptions = {
          method: "POST",
          headers: { "Content-Type": "application/json" }
        };
        const response = await fetch(`http://127.0.0.1:8080/todos/${id}/completed`, requestOptions);
        const data = await response.json();
        this.ListTodos();
        this.newtodo = '';
        
      },

      async RemoveTodo(id) {      

        await fetch(`http://127.0.0.1:8080/todos/${id}`, { method: "DELETE" });
        this.ListTodos();
        
      }

    },
    created() {
      this.ListTodos();
    },
  }
</script>

<template>
  <div >
    <input type="text" class="todo-input" v-model="newtodo" placeholder="What needs to be done" @keyup.enter="AddTodo"/>
  </div>
  <div v-for="todo in todos" :key="todo.id" class="todo-item" @change="CompleteTodo(todo.id)">
    <div class="item-left">
      <div class="checkbox"><input type="checkbox" v-model="todo.completed"/></div>
      <div :class="{completed : todo.completed}">{{ todo.title }}</div>    
    </div>
    <div class="remove-item" @click="RemoveTodo(todo.id)">
      &times;
    </div>
    
  </div>  
</template>

<style scoped>
.todo-input {
  width: 100%;
  padding: 10px 18px;
  font-size: 18px;
  margin-top: 2rem;
  margin-bottom: 2rem;
}

.todo-item {
  margin-bottom: 1rem;
  display: flex;
  align-items: center;
  justify-content: space-between;

}

.remove-item {
  cursor: pointer;
  margin-left: 2rem;

}
.remove-item:hover {
  color: red;
}

.item-left {
  display: flex;
  align-items: center;
}

.completed {
  text-decoration: line-through;
  color: greenyellow;
  
}

.checkbox {
  margin-right: 2rem;
}

</style>