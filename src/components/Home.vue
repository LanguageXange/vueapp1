<template>
  <div>This is home component</div>
</template>

<script>
export default {
  unmounted() {
    console.log("home unmounted");
  },
  activated() {
    console.log("home activated");
  },
  deactived() {
    console.log("home deactivated");
  },
};
</script>
