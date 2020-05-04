<template>
  <div class="modal">
    <div class="content">
      <a href @click.prevent="$emit('toggleModal')">&#10006;</a>
      <form>
        <label>{{currentId}}</label>
        <label for="title">Title</label>
        <input type="text" name="title" id="title" v-model="title" />
        <label for="title">Text</label>
        <textarea type="text" name="text" id="text" v-model="content" />
        <label>Select Tags</label>
        <div class="tags">
          <input type="checkbox" id="work" value="Work" v-model="tags" />
          <label for="work">Work</label>
          <input type="checkbox" id="travel" value="Travel" v-model="tags" />
          <label for="travel">Travel</label>
          <input type="checkbox" id="sport" value="Sport" v-model="tags" />
          <label for="sport">Sport</label>
        </div>
      </form>
      <button @click="save">Save</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    modalTitle: String,
    modalContent: String,
    modalTags: Array,
    modalId: Number
  },
  data() {
    return {
      new: false,
      currentItem: {},
      currentId: null,
      title: "",
      content: "",
      tags: []
    };
  },
  methods: {
    save() {
      console.log(this.modalTags.length);
      console.log(this.tags.length);
      if (
        this.modalTitle === "" &&
        this.modalContent === "" &&
        this.modalCardId === undefined &&
        this.modalTags.length === 0
      ) {
        this.$emit("addCard", this.title, this.content, this.tags);
      } else if (
        this.modalTitle !== this.title ||
        this.modalContent !== this.content ||
        this.modalTags !== this.tags
      ) {
        this.$emit(
          "updateCard",
          this.modalId,
          this.title,
          this.content,
          this.tags
        );
      }
      this.$emit("toggleModal");
    },

    isEmpty(obj) {
      for (var key in obj) {
        if (Object.prototype.hasOwnProperty.call(obj, key)) return false;
      }
      return true;
    }
  },
  created() {
    this.title = this.modalTitle;
    this.content = this.modalContent;
    this.tags = this.modalTags;
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
  max-width: 100%;
  top: 0;
  left: 0;
  margin-left: auto;
  margin-right: auto;
  min-height: 100%;
  z-index: 10;
  background: rgba(0, 0, 0, 0.2);
  backdrop-filter: blur(8px);
  .content {
    background-color: #d8d8d8;
    padding: 50px;
    max-width: 800px;
    width: 100%;
    margin-top: 60px;
    margin-left: auto;
    margin-right: auto;
    box-shadow: 0px 0px 16px 0px rgba(0, 0, 0, 0.1);
    a {
      text-decoration: none;
      color: rgb(26, 26, 26);
      width: fit-content;
      align-self: flex-end;
    }
    display: flex;
    flex-direction: column;
  }
  form {
    width: auto;
    margin: 50px;
    margin-top: 8px;
    display: flex;
    flex-direction: column;
    text-align: left;
    input,
    label,
    textarea {
      margin-bottom: 8px;
    }
    textarea,
    input {
      font-family: "Arial";
      padding: 8px;
      resize: none;
      outline: none;
      border: none;
      border-radius: 8px;
      box-shadow: 0px 0px 4px 0px rgba(0, 0, 0, 0.1);
    }
    label {
      margin-right: 8px;
    }
  }
  button {
    border: none;
    outline: none;
    background: none;
    width: fit-content;
    padding: 8px 16px;
    margin-left: auto;
    margin-right: auto;
    border: 2px solid #5c5c5c;
    border-radius: 10px;
    font-weight: bold;
    color: #353535;
    cursor: pointer;
  }
}

@media screen and (max-width: 1200px) {
  .modal {
    width: 100%;
    max-width: 100%;
    top: 0;
    .content {
      width: 100%;
      max-width: fit-content;
      form {
        width: auto;
        textarea {
          min-height: 100px;
        }
      }
    }
  }
}
</style>