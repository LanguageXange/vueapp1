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

  <!-- Transitions and Animations -->
  <button @click="flag = !flag">Toggle hello</button>
  <!-- mode determines the order of animation by default it's in-out -->
  <!-- <transition name="woola" mode="out-in">
    <h2 v-if="flag" key="main">Hello</h2>
    <h2 v-else key="secondary">Another Hello</h2>
  </transition> -->

  <!-- Animating with CSS Animations -->
  <!-- https://vuejs.org/guide/built-ins/transition#using-transitions-and-animations-together -->
  <!-- adding `appear` so that animation plays on the first load -->
  <!-- <transition name="zoom" type="animation" appear>
  <h2 v-if="flag">Animating with CSS</h2>
</transition> -->

  <!-- Animating with JS - functions defined in methods object -->
  <!-- Web Animations API - https://developer.mozilla.org/en-US/docs/Web/API/Element/animate -->
  <!-- :css-"false" tells Vue that don't check for CSS animation skip to use JS animation -->
  <!-- if using both CSS and JS we can remove 'done' in enter and leave function and Vue will use the CSS duration -->
  <!-- <transition
    @before-enter="beforeEnter"
    @enter="enter"
    @after-enter="afterEnter"
    @before-leave="beforeLeave"
    @leave="leave"
    @after-leave="afterLeave"
    @enter-cancelled="enterCancelled"
    @leave-cancelled="leaveCancelled"
    :css="true"
    name="woola"
  >
    <h2 v-if="flag">Animating with JS & CSS</h2>
  </transition> -->

  <!-- Animating a List with transition-group -->
  <button @click="addItem">Add Item</button>

  <ul>
    <transition-group name="woola">
      <li v-for="(item, index) in items" :key="item" @click="removeItem(index)">
        {{ item }}
      </li>
    </transition-group>
  </ul>
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
      flag: true,
      items: ["apple", "banana", "oranges", "grapes"],
    };
  },
  methods: {
    addItem() {
      const randomNum = Math.floor(Math.random() * 200 + 1);
      const randomIndex = Math.floor(Math.random() * this.items.length);
      this.items.splice(randomIndex, 0, randomNum);
    },
    removeItem(id) {
      this.items.splice(id, 1);
    },
    updateAge(num) {
      this.age += num;
    },
    // callback functions
    updateAgeCB(num) {
      this.age += num;
    },

    // JS Animations
    beforeEnter(el) {
      console.log("before enter event fired");
    },
    enter(el) {
      console.log("enter event fired");
    },
    afterEnter(el) {
      console.log("after enter event fired");
    },
    beforeLeave(el) {
      console.log("before leave event fired");
    },
    leave(el) {
      console.log("leave event fired");
    },
    afterLeave(el) {
      console.log("after leave event fired");
    },
    enterCancelled() {
      console.log("enter cancelled event fired");
    },
    leaveCancelled() {
      console.log("leave cancelled event fired");
    },
  },
};
</script>

<!-- enter-from;enter-to;enter-active && leave-from; leave-to;leave-active -->
<style>
/* First Animation */
.woola-enter-from {
  opacity: 0;
  transform: translateY(-20px);
}
.woola-enter-active {
  transition: all 0.5s linear;
}
.woola-leave-to {
  transition: all 0.25s linear;
  opacity: 0;
  transform: translateY(-20px);
}

/* for smoother list animation   */
/* transform property is automatically applied to element that's moving */
/* when adding new item, that item occupies space so other elments needs moving */
.woola-move {
  transition: all 1s linear;
}
/* when removing the element, the animation takes place first and the it's removed */
/* as it's animating the element still occupies the space meaning that other elements don't need to move */
/* that's why the transform property doesn't have to change */
/* SOLUTION */
/* adding position absolute so that the element will give up the space making other elements to move up*/
.woola-leave-active {
  position: absolute;
}

/* Second Animation */
h2 {
  padding: 20px;
  width: 250px;
  margin: 20px;
}
@keyframes zoom-in {
  from {
    transform: scale(0, 0);
  }
  to {
    transform: scale(1, 1);
  }
}
@keyframes zoom-out {
  from {
    transform: scale(1, 1);
  }
  to {
    transform: scale(0, 0);
  }
}
.zoom-enter-active {
  animation: zoom-in 1s linear forwards;
  transition: all 5s linear;
}
.zoom-leave-active {
  animation: zoom-out 1s linear forwards;
  transition: all 5s linear;
}
.zoom-enter-from,
.zoom-leave-to {
  opacity: 0;
}

li {
  font-size: 25px;
  cursor: pointer;
  width: max-content;

  &:hover {
    background-color: #eee;
  }
}
</style>
