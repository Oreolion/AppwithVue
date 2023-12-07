<template>
  <div class="container">
    <div class="animate__animated animate__fadeInDown">
      <h1>
        A TODO APP
        <svg
          xmlns="http://www.w3.org/2000/svg"
          height="4rem"
          width="4rem"
          viewBox="0 0 576 512"
        >
          <path
            fill="#f8c683"
            d="M0 96C0 60.7 28.7 32 64 32H512c35.3 0 64 28.7 64 64V416c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V96zM128 288a32 32 0 1 0 0-64 32 32 0 1 0 0 64zm32-128a32 32 0 1 0 -64 0 32 32 0 1 0 64 0zM128 384a32 32 0 1 0 0-64 32 32 0 1 0 0 64zm96-248c-13.3 0-24 10.7-24 24s10.7 24 24 24H448c13.3 0 24-10.7 24-24s-10.7-24-24-24H224zm0 96c-13.3 0-24 10.7-24 24s10.7 24 24 24H448c13.3 0 24-10.7 24-24s-10.7-24-24-24H224zm0 96c-13.3 0-24 10.7-24 24s10.7 24 24 24H448c13.3 0 24-10.7 24-24s-10.7-24-24-24H224z"
          />
        </svg>
      </h1>
      <p>
        Hey
        <input type="text" v-model="todoName" placeholder="name here" /> input
        your todos below
        <svg
          xmlns="http://www.w3.org/2000/svg"
          height="16"
          width="12"
          viewBox="0 0 384 512"
        >
          <path
            fill="#008000"
            d="M169.4 502.6c12.5 12.5 32.8 12.5 45.3 0l128-128c12.5-12.5 12.5-32.8 0-45.3s-32.8-12.5-45.3 0L224 402.7 224 32c0-17.7-14.3-32-32-32s-32 14.3-32 32l0 370.7L86.6 329.4c-12.5-12.5-32.8-12.5-45.3 0s-12.5 32.8 0 45.3l128 128z"
          />
        </svg>
      </p>
    </div>
    <section id="todo__container" class="animate__animated animate__fadeInDown">
      <form @submit.prevent="createTodo">
        <input
          class="todo__input"
          ref="myInput"
          type="text"
          placeholder="input your todo here"
          v-model="todo.todoItem"
        />
        <button type="submit" class="addtodo_btn">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            height="1.5rem"
            width="1.5rem"
            viewBox="0 0 448 512"
          >
            <path
              fill="#008000"
              d="M256 80c0-17.7-14.3-32-32-32s-32 14.3-32 32V224H48c-17.7 0-32 14.3-32 32s14.3 32 32 32H192V432c0 17.7 14.3 32 32 32s32-14.3 32-32V288H400c17.7 0 32-14.3 32-32s-14.3-32-32-32H256V80z"
            />
          </svg>
        </button>
      </form>

      <main class="todo__section">
        <h1 v-if="todos.length > 0">
          {{ todoName }}'s TODO LIST
          <svg
            xmlns="http://www.w3.org/2000/svg"
            height="3rem"
            width="3rem"
            viewBox="0 0 512 512"
          >
            <path
              fill="#f8c683"
              d="M24 56c0-13.3 10.7-24 24-24H80c13.3 0 24 10.7 24 24V176h16c13.3 0 24 10.7 24 24s-10.7 24-24 24H40c-13.3 0-24-10.7-24-24s10.7-24 24-24H56V80H48C34.7 80 24 69.3 24 56zM86.7 341.2c-6.5-7.4-18.3-6.9-24 1.2L51.5 357.9c-7.7 10.8-22.7 13.3-33.5 5.6s-13.3-22.7-5.6-33.5l11.1-15.6c23.7-33.2 72.3-35.6 99.2-4.9c21.3 24.4 20.8 60.9-1.1 84.7L86.8 432H120c13.3 0 24 10.7 24 24s-10.7 24-24 24H32c-9.5 0-18.2-5.6-22-14.4s-2.1-18.9 4.3-25.9l72-78c5.3-5.8 5.4-14.6 .3-20.5zM224 64H480c17.7 0 32 14.3 32 32s-14.3 32-32 32H224c-17.7 0-32-14.3-32-32s14.3-32 32-32zm0 160H480c17.7 0 32 14.3 32 32s-14.3 32-32 32H224c-17.7 0-32-14.3-32-32s14.3-32 32-32zm0 160H480c17.7 0 32 14.3 32 32s-14.3 32-32 32H224c-17.7 0-32-14.3-32-32s14.3-32 32-32z"
            />
          </svg>
        </h1>
        <div class="detail__box">
            <p>Number of todos: <span>{{todos.length  }}</span> </p>
            <p>Completed todos: <span>{{ getCompleted() }}</span> </p>
        </div>

        <p v-if="todos.length == 0">
          HEY {{ todoName }}, YOU CURRENTLY HAVE NOTHING TO DO!!
        </p>

        <transition-group name="list">
          <div
            v-for="(eachTodo, index) in todos"
            :class="`todo__item ${eachTodo.done && 'done'}`"
            :key="index"
          >
            <input
              class="checkbox"
              type="checkbox"
              v-model="eachTodo.done"
              @click="setComplete"
            />
            <textarea class="textbox" type="text" :value="eachTodo.todoItem">
            </textarea>
            <div class="todo__btns">
              <button @click="editTodo">
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  height="16"
                  width="16"
                  viewBox="0 0 512 512"
                >
                  <path
                    fill="#ffffff"
                    d="M471.6 21.7c-21.9-21.9-57.3-21.9-79.2 0L362.3 51.7l97.9 97.9 30.1-30.1c21.9-21.9 21.9-57.3 0-79.2L471.6 21.7zm-299.2 220c-6.1 6.1-10.8 13.6-13.5 21.9l-29.6 88.8c-2.9 8.6-.6 18.1 5.8 24.6s15.9 8.7 24.6 5.8l88.8-29.6c8.2-2.7 15.7-7.4 21.9-13.5L437.7 172.3 339.7 74.3 172.4 241.7zM96 64C43 64 0 107 0 160V416c0 53 43 96 96 96H352c53 0 96-43 96-96V320c0-17.7-14.3-32-32-32s-32 14.3-32 32v96c0 17.7-14.3 32-32 32H96c-17.7 0-32-14.3-32-32V160c0-17.7 14.3-32 32-32h96c17.7 0 32-14.3 32-32s-14.3-32-32-32H96z"
                  />
                </svg>
              </button>
              <button @click="deleteTodo(eachTodo)">
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  height="16"
                  width="14"
                  viewBox="0 0 448 512"
                >
                  <path
                    fill="#ffffff"
                    d="M135.2 17.7C140.6 6.8 151.7 0 163.8 0H284.2c12.1 0 23.2 6.8 28.6 17.7L320 32h96c17.7 0 32 14.3 32 32s-14.3 32-32 32H32C14.3 96 0 81.7 0 64S14.3 32 32 32h96l7.2-14.3zM32 128H416V448c0 35.3-28.7 64-64 64H96c-35.3 0-64-28.7-64-64V128zm96 64c-8.8 0-16 7.2-16 16V432c0 8.8 7.2 16 16 16s16-7.2 16-16V208c0-8.8-7.2-16-16-16zm96 0c-8.8 0-16 7.2-16 16V432c0 8.8 7.2 16 16 16s16-7.2 16-16V208c0-8.8-7.2-16-16-16zm96 0c-8.8 0-16 7.2-16 16V432c0 8.8 7.2 16 16 16s16-7.2 16-16V208c0-8.8-7.2-16-16-16z"
                  />
                </svg>
              </button>
            </div>
          </div>
        </transition-group>
      </main>
    </section>
  </div>
</template>

<script>
import "animate.css";
export default {
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
      if (!this.todo.todoItem || !this.todoName) {
        if (!this.todoName) alert("please input name");
        if (!this.todo.todoItem) alert("please input what to do");
        return;
      }
      let todo = {
        todoItem: this.todo.todoItem,
        done: false,
      };

      this.todos.push(todo);
      localStorage.setItem("todos", JSON.stringify(this.todos));
      this.updateUserName();
      this.todo.todoItem = "";
    },
    getCompleted () {
        const result = this.todos.filter((item) => item.done == true).length;

        return result;

    },

    updateUserName() {
      localStorage.setItem("todoName", this.todoName);
    },

    editTodo() {
      this.editTodoItem = this.todo.todoItem;
      this.editThisTodo = !this.editThisTodo;
      return;
    },

    deleteTodo(todo) {
      this.todos = this.todos.filter((item) => item !== todo);
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },

    setComplete() {
      this.todo.done = !this.todo.done;
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
  },
  mounted() {
    this.$refs.myInput.focus();
  },
};
</script>

<style scoped>
.container {
  max-width: 39rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: 5rem auto;
  background-color: rgba(360, 360, 360, 0.5);
  padding: 2rem;
  border-radius: 1rem;
  overflow-x: hidden;
}

p {
  font-weight: bold;
  font-size: 1.2rem;
}

p input {
  width: 30%;
  height: 2.5rem;
  background-color: rgba(225, 225, 225, 0.5);
  text-align: center;
  color: #fff;
  font-weight: bold;
  font-size: 1.1rem;
  outline: none;
  border: none;
}

p input[placeholder] {
  color: #fff;
}

.container h1 {
  color: #f9d5b2;
  text-align: center;
  align-items: center;
  justify-content: center;
  margin: 0 auto;
  margin-bottom: 2rem;
  text-shadow: 1px 4px 1px rgba(0, 100, 0, 0.671);
  display: flex;
  gap: 1rem;
  white-space: nowrap;
  max-width: 32rem;
  font-size: 3rem;
}

.container h1 + p {
  color: #f9d5b2;
  max-width: 32rem;
  text-align: center;
  margin-bottom: 2rem;
 
}

.todo__section p {
  color: green;
  text-align: center;
  max-width: 32rem;


}

.todo__section h1 {
  color: #f9d5b2;
  text-align: center;
  background-color: rgba(255, 255, 255, 0.5);
  margin: 3rem auto;
  font-size: 2rem;
  text-shadow: 1px 4px 1px rgba(0, 100, 0, 0.671);
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 4px;
  max-width: 32rem;
  overflow: hidden;
}


.done .textbox {
  text-decoration: line-through;
  text-decoration-color: red;
}

#todo__container form {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  gap: 1.5rem;
  margin-bottom: 3rem;
  padding: 1rem;
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 4px;
  height: 7rem;
  max-width: 32rem;
}

.textbox {
  width: 50%;
  padding-left: 1rem;
  height: 4rem;
  background-color: rgba(255, 255, 255, 0.5);
  background-color: rgba(355, 355, 355, 0.5);
  font-size: 1.3rem;
  outline: none;
  border: none;
  border-radius: 3px;
}

.checkbox {
  height: 2rem;
  width: 2rem;
}

.todo__input {
  height: 5rem;
  width:75%;
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
  display: flex;
  padding: 0.7rem;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  background-color: #000;
  white-space: nowrap;
  border: 5px solid #f9d5b2;
  cursor: pointer;
  width: 7rem;
  height: 4rem;
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

.todo__section {
  max-width: 32rem;
}

.todo__section .detail__box {

    border-radius: .5rem;
    max-width: 32rem;
    margin-bottom: 1rem;
    background-color: rgba(0, 180, 0, 0.2);   
    display: flex;
    flex-direction: row;
    gap: .5rem;
    align-items: flex-start;
    padding: 1rem;
    font-family: monospace;
    justify-content: space-between;

    


}

.todo__section .detail__box p {
    white-space: nowrap;
}

.todo__section .detail__box p span {
    font-weight: bold;
    background-color: rgba(255, 255, 255, 0.5);
    padding: .2rem;

}
.todo__section .todo__item {
  display: flex;
  margin-bottom: 2rem;
  border: 2px solid green;
  height: 8rem;
  align-items: center;
  padding: 1rem 2rem;
  justify-content: space-between;
  gap: 2rem;
  font-size: 1.6rem;
  border-top-left-radius: 3rem;
  border-bottom-right-radius: 3rem;
  width: 32rem;
}

.todo__btns {
  display: flex;
  gap: .6rem;
}

.todo__section .todo__item button {
  cursor: pointer;
  height: 3rem;
  width: 4rem;
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
.list-move,
.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(-50px);
}

.list-leave-active {
  position: absolute;
}

.animate__animated {
  animation-duration: 3s;
}

@media (max-width: 650px) {
  .container {
    max-width: 29rem;
    padding: 2rem;
  }

  #todo__container form {
    max-width: 27rem;
  }

  .container h1 {
    font-size: 2rem;
  }

  .container h1 + p {
    font-size: 1.1rem;
  }

  .todo__section h1 {
    font-size: 1.6rem;
  }

  .todo__section .todo__item {
    max-width: 27rem;
    gap: 1rem;
  }

  .textbox {
    height: 5rem;
  }

  .checkbox {
    width: 3rem;
    height: 3rem;
  }

  .todo__btns {
    display: flex;
  }
}

@media (max-width: 450px) {
  .container {
    max-width: 26rem;
  }

  #todo__container form {
    max-width: 24rem;
  }
  .textbox {
    width: 9rem;
  }
  .checkbox {
    width: 2.5rem;
    height: 2.5rem;
  }

  .todo__section .todo__item {
    max-width: 24rem;
    gap: 1rem;
  }

  .todo__btns {
    display: flex;
    flex-direction: column;
  }
}
</style>
