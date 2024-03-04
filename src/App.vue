<template>
  <h1>Hello world</h1>
  <button @click="age++">increment</button>
  <button @click="age--">decrement</button>
  <greeting :myage="age"></greeting>
  <!-- Pass Props to Children -->
  <user :myage="age" @age-change="updateAge" :ageChangeFn="updateAgeCB"></user>

  <!-- Named Slot using v-slot:name -->
  <my-form>
    <template v-slot:help>
      <p>{{ helpText }}</p>
    </template>
    <template v-slot:fields>
      <input type="text" placeholder="email" />
      <input type="text" placeholder="username" />
    </template>

    <template v-slot:buttons>
      <button type="submit">Submit</button>
    </template>

    <p>Woolalala</p>
  </my-form>

  <!-- Dynamic Components -->
  <select v-model="componentName">
    <option value="home">Home</option>
    <option value="about">About</option>
  </select>
  <!-- Using Keep Alive we won't see the home page unmounted console log message -->
  <keep-alive>
    <component :is="componentName"></component>
  </keep-alive>
</template>

<script>
import Greeting from "@/components/Greeting.vue";
import User from "@/components/User.vue";
import MyForm from "@/components/Form.vue";
import Home from "@/components/Home.vue";
import About from "@/components/About.vue";

export default {
  name: "MyApp", // this name will show up in Vue dev tool
  components: {
    Greeting,
    User,
    MyForm,
    Home,
    About,
  },
  data() {
    return {
      age: 40,
      helpText: "This is a form",
      componentName: "home",
    };
  },
  methods: {
    updateAge(num) {
      this.age += num;
    },
    // callback functions
    updateAgeCB(num) {
      this.age += num;
    },
  },
};
</script>
