<template>
  <div>a div in Greeting Component using SCSS</div>
  <p>greeting! {{ userName }}</p>

  <p v-if="myage > 50">You are older than 50</p>
  <p v-else>You are not old enough</p>
</template>

<script>
export default {
  name: "MyGreeting", // shows up in dev tool
  props: ["myage"],
  data() {
    return {
      userName: "John",
    };
  },
};
</script>

<style scoped lang="scss">
@import "./_variables.scss";
/* had to go to settings to disable CSS validation */
/* https://code.visualstudio.com/docs/languages/css#_syntax-verification-linting */
div {
  background-color: $primary;
  padding: $space;
}
p {
  color: darken(#cc4444, 20%);
}
</style>
