<template>
  <div class="container">
    <h1>A TODO APP</h1>
    <p>
      Hey <input type="text" v-model="todoName" placeholder="name here" /> input
      your todos below;
    </p>
    <section class="todo__container">
      <form @submit.prevent="createTodo">
        <input
          class="todo__input"
          ref="myInput"
          type="text"
          placeholder="input your todo here"
          v-model="todo.todoItem"
        />
        <button type="submit" class="addtodo_btn">ADD TODO</button>
      </form>
      <main class="todo__section">
        <h1 v-if="todos.length > 0">{{ todoName }}'s TODO LIST</h1>
        <p v-if="todos.length == 0">
          HEY {{ todoName }}, YOU CURRENTLY HAVE NOTHING TO DO!!
        </p>
        <!-- <BeakerIcon /> -->

        <div v-for="(eachTodo, index) in todos" class="todo__item" :key="index">
          <input class="checkbox" type="checkbox" :value="eachTodo.done" />
          <textarea
            ref="input"
            class="textbox"
            type="text"
            :value="eachTodo.todoItem">
        </textarea>
          <div class="todo__btns">
            <button @click="editTodo">Edit Todo</button>
            <button @click="deleteTodo(eachTodo)">Delete Todo</button>
          </div>
        </div>
      </main>
    </section>
  </div>
</template>

<!-- work om UI -->
<!-- add animation to  elements -->
<!-- add icons -->
<!-- done function -->
<!-- data ui -->

<script>
// import { BeakerIcon } from "@heroicons/react/24/solid";
export default {
  // components: {
  //     BeakerIcon
  // },
  data() {
    return {
      todoName: localStorage.getItem("todoName") || "",
      todo: {
        todoItem: "",
        done: false,
      },
      todos: JSON.parse(localStorage.getItem("todos")) || [],
      editThisTodo: false,
      editTodoItem: "",
    };
  },
  methods: {
    createTodo() {
      if (!this.todo.todoItem || !this.todoName) return;
      let todo = {
        todoItem: this.todo.todoItem,
        done: false,
      };

      this.todos.push(todo);
      localStorage.setItem("todos", JSON.stringify(this.todos));
      this.updateUserName();
      this.todo.todoItem = "";
    },

    updateUserName() {
      localStorage.setItem("todoName", this.todoName);
    },

    editTodo() {
      this.editTodoItem = this.todo.todoItem;
      this.editThisTodo = !this.editThisTodo;
    },

    deleteTodo(todo) {
      this.todos = this.todos.filter((item) => item !== todo);
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },

    // setComplete() {
    //   todo.done = input.checked;
    // },
  },
  mounted() {
    this.$refs.myInput.focus();
  },
};
</script>

<style scoped>
h1 {
  color: #f9d5b2;
  text-align: center;
  margin-bottom: 2rem;
  text-shadow: 1px 4px 1px rgba(0, 100, 0, 0.671);
}

p {
  font-weight: bold;
  font-size: 1.2rem;
  text-align: center;
}

p input {
  width: 6rem;
  height: 2rem;
  background-color: rgba(225, 225, 225, 0.5);
  text-align: center;
  color: #fff;
  font-weight: bold;
  font-size: 1rem;
  outline: none;
  border: none;
}

.container p {
  color: #f9d5b2;
  margin-bottom: 2rem;
}

.todo__section p {
  color: green;
}

main h1 {
  color: #f9d5b2;
  text-align: center;
  background-color: rgba(255, 255, 255, 0.5);
  margin: 3rem auto;
  padding: 1rem;
  text-shadow: 1px 4px 1px rgba(0, 100, 0, 0.671);
  white-space: nowrap;
  max-width: 30rem;
  border-radius: 4px;
}

main p {
  color: green;
}

.container {
  width: 40rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: 5rem auto;
}
.todo__container form {
  display: flex;
  flex-direction: row;
  gap: 1.5rem;
  margin-bottom: 5rem;
  padding: 1.5rem;
  background-color: rgba(255, 255, 255, 0.5);
  opacity: 0.9;
  border-radius: 4px;
}

.textbox {
  width: 50%;
  padding-left: 1rem;
  height: 4rem;
  background-color: rgba(255, 255, 255, 0.5);
  background-color: rgba(355, 355, 355, 0.5);
  font-size: 1rem;
  outline: none;
 
}

.checkbox {
  height: 2rem;
  width: 2rem;
  border-radius: 50%;

}

.todo__input {
  height: 5rem;
  width: 80%;
  border: none;
  background: #eee;
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 1rem;
  font-size: 1.3rem;
  outline: none;
  color: #000;
}

.todo__input[placeholder] {
  color: #444;
  padding-left: 1rem;
}
.addtodo_btn {
  background-color: #000;
  border: 5px solid #f9d5b2;
  width: 13rem;
  border-radius: 1rem;
  color: #fff;
  font-weight: bold;
  box-shadow: 1px, 4px, 1px rgba(0, 0, 0, 0.671);
  &:hover {
    border: none;
    color: #f9d5b2;
    border-radius: 10rem;
    font-size: 1rem;
  }
}

.todo__section .todo__item {
  display: flex;
  margin-bottom: 2rem;
  border: 2px solid green;
  padding: 1.2rem;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
  font-size: 1.6rem;
  border-top-left-radius: 3rem;
  border-bottom-right-radius: 3rem;
 
}

.todo__btns {
  display: flex;
}

.todo__section .todo__item button {
  height: 4rem;
  width: 8rem;
  white-space: nowrap;
  border: none;
  border-radius: 1rem;
  color: #fff;
  font-weight: bold;

  &:hover {
    letter-spacing: 1px;
  }
}

.todo__section .todo__item button:first-child {
  margin-right: 1rem;
  background-color: rgba(0, 255, 0, 0.3);
  &:hover {
    background-color: green;
  }
}
.todo__section .todo__item button:last-child {
  background-color: rgba(360, 0, 0, 0.3);
  &:hover {
    background-color: red;
  }
}

@media (max-width: 550px) {
  .container {
    width: 28rem;
  }

  h1 {
    font-size: 2.9rem;
  }

  .todo__section .todo__item button {
    width: 6rem;
  }

  .textbox {
    width: 70%;
  }

  .checkbox {
    width: 3rem;
    height: 3rem;
  }
}

@media (max-width: 450px) {
  .textbox {
    width: 7rem;
  }
  .checkbox {
    width: 3rem;
    height: 3rem;
  }

  .todo__section .todo__item button {
    width: 4rem;
  }
}
</style>
