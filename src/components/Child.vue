<template>
  <div class="modal">
    <a href v-on:click="test">Close</a>
  </div>
</template>

<script>
export default {
  methods: {
    test() {
      console.log("call test");
      event.preventDefault();
      this.$emit("toggle-modal");
    }
  }
};
</script>

<style lang="scss" scoped>
.modal {
  max-width: 1200px;
  margin: 56px;
  height: 80vh;
  background: #d8d8d8;
}
</style>