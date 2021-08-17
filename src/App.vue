<template>
  <div id="app">
    <h1>Inp value : {{ inputValue }}</h1>

    <!--    <input type="text" :value="inputValue" @input="handleInputChange">-->
    <!--    <input type="text" :value="inputValue" @input="inputValue = $event.target.value">-->
    <!--    <input type="text" v-model="inputValue" @keypress="handleInputChange">-->
    <!--    <input type="text" v-model="inputValue" @input="handleInputChange">-->
    <!--           @keypress.esc="closeWindow">-->
    <!--           @keypress.space="closeWindow"-->
    <!--    <input type="text" v-model="inputValue"-->
    <!--           @keypress="handleInputChange"-->
    <!--           @keypress.enter="alertHandler"-->
    <!--    >-->
    <!--    <input type="text" v-model="inputValue">-->
    <!--    <input type="text" v-model.number="inputValue">-->
    <input
        type="text"
        v-model.trim="inputValue"
        @keypress.enter="createNewTodo"
    >
    <button @click="createNewTodo">create todo</button>

    <div v-if="todo">{{ todo.id }} = {{ todo.title }} = {{ todo.completed }}</div>

    <!--    <br>-->
    <!--    <input type="checkbox" v-model="isOn">-->
    <!--    <br>-->
    <!--    <button @click="isOn = !isOn">toggle checkbox</button>-->
    <!--    <br>-->
    <!--    <button @click.once="isOn = !isOn">toggle checkbox</button>-->
    <!--    <br>-->
    <!--    <button @click.once="btnClkOnce" @click.prevent="isOn = !isOn">toggle checkbox</button>-->

    <!--    <div v-for="error of errors" :key="error"> {{ error }}</div>-->
    <ul v-if="todos.length">
      <li
          v-for="todo of todos" :key="todo.id"
          @click="selectedTodoId = todo.id"
      >
        {{ todo.id }} = {{ todo.title }} = {{ todo.completed }}
      </li>
    </ul>

    <h2 v-else-if="loading">Loading...</h2>
    <h2 v-else>NO DATA</h2>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      inputValue: '',
      // isOn: false,
      // errors: [],
      todos: [],
      todo: null,
      selectedTodoId: null,
      loading: false,
    }
  },
  methods: {
    createNewTodo() {
      if (!this.inputValue) return;

      const newTodo = {
        id: Math.random(),
        title: this.inputValue,
        completed: false,
      }

      this.todos.unshift(newTodo);
      this.inputValue = '';
    },

    async fetchTodos() {
      try {
        this.loading = true;
        const res = await fetch('https://jsonplaceholder.typicode.com/todos');
        this.todos = await res.json();
        console.log(this.todos);
      } catch (e) {
        console.log(e);
      } finally {
        this.loading = false;
      }
    },

    async fetchTodo(id) {
      try {
        this.loading = true;
        const res = await fetch(`https://jsonplaceholder.typicode.com/todos/${id}`);
        this.todo = await res.json();
        console.log(this.todo);
      } catch (e) {
        console.log(e);
      } finally {
        this.loading = false;
      }
    },
    // testMethod() {
    //
    // },
    // btnClkOnce() {
    //   console.log('button @click.once')
    // },
    // closeWindow() {
    //   console.log('tut');
    //   // window.close()
    // },
    // alertHandler() {
    //   alert('hello');
    // },
    //
    // // handleInputChange({target: {value}}) {
    // //   this.inputValue = value;
    // // },
    // handleInputChange(e) {
    //   const {target: {value}, key} = e;
    //   console.log(key, value);
    //
    //   // if (key === 'Enter') {
    //   //   alert('hello');
    //   //   return
    //   // }
    //
    //   // const message = 'input should not contain 0';
    //   //
    //   // if (value.includes('0')) {
    //   //   // this.inputValue = value.replaceAll('0', '');
    //   //
    //   //   !this.errors.includes(message) && this.errors.push(message);
    //   //   // e.preventDefault();
    //   // }else {
    //   //   this.errors.includes(message) && (this.errors = this.errors.filter(el => el !== message));
    //   //
    //   // }
    //
    //   if (value.length >= 5) {
    //     e.preventDefault();
    //   }
    //   // this.inputValue = value;
    // }
  },
  watch: {
    // inputValue() {
    //   console.log(typeof this.inputValue, this.inputValue, 'from watcher')
    // },
    selectedTodoId(){
      this.fetchTodo(this.selectedTodoId);
    }
  },

  // lifecycle:
  // beforeCreate() {
  //   console.log(this.inputValue, this.testMethod, 'beforeCreate')
  // },
  created() {
    console.log(this.inputValue, this.testMethod, 'created');
    this.fetchTodos();
  },

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

<!--inputs-->
<!--lifecycle-->
<!--work with api-->