<template>
  <div id="app">
    <h1>Inp value : {{ inputValue }}</h1>

    <!--    <input type="text" :value="inputValue" @input="handleInputChange">-->
    <!--    <input type="text" :value="inputValue" @input="inputValue = $event.target.value">-->
    <input type="text" v-model="inputValue" @keypress="handleInputChange">

  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      inputValue: '123'
    }
  },
  methods: {
    // handleInputChange({target: {value}}) {
    //   this.inputValue = value;
    // },
    handleInputChange(e) {
      const {target: {value}, preventDefault} = e;
      console.log(value);
      if (value.includes('0')) {
        preventDefault();
        // return;
      }
      // this.inputValue = value;
      15:30
    }
  }
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