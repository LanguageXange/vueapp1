<template>
  <div>{{ userName }} is {{ myage }} years old</div>
  <div>double age is {{ doubleAge }}</div>

  <button @click="onClickAge">update age + 5 from user component</button>
  <button @click="ageChangeFn(10)">update age + 10 with callback function</button>
</template>

<script>
export default {
  name: "MyUser",
  data() {
    return {
      userName: "Amy",
    };
  },
  //props:["myage"],
  // type checking
  props: {
    myage: {
      type: Number,
      required: true,
      default: 20,
      validator(v) { // validator runs before the instance created so we don't have access to this
     // console.log(this,'what is this in validator')
        return v < 200;
      },
    },
    ageChangeFn: Function
  },
  emits: ["age-change"], // help document what the component does,
  computed: {
    doubleAge() {
      return this.myage * 2;
    },
  },
  methods: {
    onClickAge() {
      // emit event
      this.$emit("age-change", 5);
    },
  },
};
</script>

<style lang="scss" scoped></style>
