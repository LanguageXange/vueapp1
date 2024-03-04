<template>
  <form>
    <div>
      <slot name="help"> </slot>
    </div>
    <div>
      <slot name="fields"></slot>
    </div>

    <div>
      <slot name="buttons"></slot>
    </div>
    <slot></slot>
  </form>
</template>

<script>
// inserting content with slots

export default {
  name: "MyForm",
};
</script>

<style lang="scss" scoped>
form {
  border: 2px solid black;
  margin: 50px 0;
  padding: 20px;
  max-width: 400px;
}
</style>
