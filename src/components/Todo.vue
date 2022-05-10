<script lang="ts">
interface todo {
  task: string;
  done: boolean;
}

const newTodo = "";

const addTodo = (todos: todo[], newTodo: string) => {
  if (!newTodo) return;
  todos.push({ task: newTodo, done: false });
};

const todos: todo[] = [{ task: "1st todo", done: false }];

export default {
  data() {
    return {
      todos,
      newTodo,
    };
  },
  methods: {
    addTodo() {
      addTodo(this.todos, this.newTodo);
      this.newTodo = "";
    },
    removeTodo(index: number) {
      this.todos = this.todos.filter((el, i) => i !== index);
    },
  },
};
</script>

<template>
  <h2>Todo app</h2>

  <!-- handling default events - @event is the syntax -->
  <form @submit.prevent="addTodo" class="form">
    <input type="text" v-model="newTodo" class="form-input" />
    <button type="submit" class="submit">Submit</button>
  </form>

  <main class="todo-wrapper">
    <!-- render all todos -->
    <div class="todo" v-for="(todo, index) in todos" :key="index">
      <!-- dynamically adding classes -->
      <h2 :class="{ 'line-through': todo.done }" class="task">
        {{ todo.task }}
      </h2>
      <!-- 2way binding nested property -->
      <input type="checkbox" v-model="todo.done" class="done" />
      <button class="delete" @click="removeTodo(index)">Delete</button>
    </div>
  </main>
</template>

<style>
.line-through {
  text-decoration: line-through;
}
.submit {
  background-color: hsl(145, 29%, 53%);
  color: white;
  padding: 0.2rem 1rem;
  border-radius: 0.4rem;
}
.todo {
  display: flex;
  margin-top: 1rem;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}
.task {
  margin: 0;
}

.done {
  height: 20px;
  width: 20px;
}
.delete {
  color: white;
  padding: 0.2rem 1rem;
  border-radius: 0.4rem;
  background-color: hsl(0, 69%, 60%);
}
</style>
