<template>
  <div class="parent">
    <a href v-on:click="toggleModal" >Open</a>
    <child v-if="showModal" v-on:toggle-modal="toggleModal"/>
  </div>
</template>

<script>
import Child from "@/components/Child";

export default {
  components: {
    Child
  },
  data() {
    return {
      showModal: false
    };
  },
  methods: {
    toggleModal() {
      console.log("Toggle Modal in Parent");
      event.preventDefault();
      this.showModal = !this.showModal;
    }
  }
};
</script>

<style lang="scss" scoped>
</style>