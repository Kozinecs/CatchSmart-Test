<template>
  <div class="modal">
    <a href v-on:click.prevent="$emit('toggle-modal')">Close</a>
    <form>
      <label>{{id}}</label>
      <label for="title">Title</label>
      <input type="text" name="title" id="title" v-model="item.title" />
      <label for="title">Text</label>
      <textarea type="text" name="text" id="text" v-model="item.text" />
    </form>
    <button v-on:click="save">Save</button>
  </div>
</template>

<script>
import moment from 'moment'

export default {
  props: {
    item: Object,
    id: Number
  },
  data() {
    return {
      cardContent: {
        title: "Some title",
        text: "Some text",
        moment: moment
      }
    };
  },
  methods: {
    save() {
      let date = new Date();
      let card = {
        date: date,
        title: this.item.title,
        content: this.item.text,
        tags: ["work", "home"]
      };
      this.$emit("saveNewCard", card);
      this.$emit("toggle-modal", true);
    }
  }
};
</script>

<style lang="scss" scoped>
.modal {
  display: flex;
  flex-direction: column;
  background-color: #d8d8d8;
  width: 100%;
  position: fixed;
  max-width: 1200px;
  top: 50px;
  margin-left: auto;
  margin-right: auto;
  min-height: 80vh;
  z-index: 10;
  form {
    margin: 50px;
    display: flex;
    flex-direction: column;
    text-align: left;
    input,
    label {
      margin-bottom: 8px;
    }
  }
}
</style>