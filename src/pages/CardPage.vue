<template>
  <div class="card-grid">
    <card
      v-for="(item, index) in cardList"
      :key="index"
      :item="item"
      :id="index"
      @click.native="openEditCardDialog(index)"
      @deleteCard="deleteCard(index)"
    />
    <button @click="openAddNewCardDialog">Add Card</button>
    <modal
      v-if="showModal"
      :modalTitle="modalTitle"
      :modalContent="modalContent"
      :modalTags="modalTags"
      :modalId="modalId"
      @addCard="addCard"
      @updateCard="updateCard"
      @toggleModal="toggleModal"
    />
  </div>
</template>
<script>
import Card from "@/components/Card";
import Modal from "@/components/Modal";

export default {
  components: {
    Card,
    Modal
  },
  data() {
    return {
      cardList: [],
      showModal: false,
      modalTitle: "",
      modalContent: "",
      modalTags: [],
      modalId: null
    };
  },
  created() {
    if (localStorage.getItem("cardList")) {
      try {
        this.cardList = JSON.parse(localStorage.getItem("cardList"));
      } catch (e) {
        console.log(e);
        localStorage.removeItem("cardList");
      }
    }
  },
  methods: {
    toggleModal() {
      this.showModal = !this.showModal;
    },

    openAddNewCardDialog() {
      this.showModal = true;
      this.modalTitle = "";
      this.modalContent = "";
      this.modalTags = [];
    },

    openEditCardDialog(cardId) {
      this.showModal = true;
      this.modalTitle = this.cardList[cardId].title;
      this.modalContent = this.cardList[cardId].content;
      this.modalTags = this.cardList[cardId].tags;
      this.modalId = cardId;
    },

    addCard(title, content, tags) {
      if (title || content || tags.length) {
        this.cardList.unshift({ date: new Date(), title, content, tags });
      }

      this.saveLocalStoreCardList();
    },

    deleteCard(cardId) {
      this.showModal = false;
      this.cardList.splice(cardId, 1);
      this.saveLocalStoreCardList();
    },

    updateCard(cardId, title, content, tags) {
      let card = {
        date: new Date(),
        title: title,
        content: content,
        tags: tags
      };

      this.cardList.splice(cardId, 1);
      this.cardList.unshift(card);
      this.saveLocalStoreCardList();
    },

    saveLocalStoreCardList() {
      let parsed = JSON.stringify(this.cardList);
      localStorage.setItem("cardList", parsed);
    }
  }
};
</script>
 
<style lang="scss" scoped>
.card-grid {
  margin-left: auto;
  margin-right: auto;
  max-width: 1200px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  column-gap: 40px;
  row-gap: 40px;
  button {
    cursor: pointer;
    align-self: center;
    margin-top: 100px;
    margin-bottom: 100px;
    border: none;
    max-height: 35px;
    outline: none;
    background: none;
    width: fit-content;
    padding: 8px 16px;
    margin-left: auto;
    margin-right: auto;
    border: 2px solid #5c5c5c;
    border-radius: 10px;
  }
}

@media screen and (max-width: 1200px) {
  .card-grid {
    grid-template-columns: repeat(2, 1fr);
    margin-left: 50px;
    margin-right: 50px;
  }
}
@media screen and (max-width: 600px) {
  .card-grid {
    grid-template-columns: repeat(1, 1fr);
    margin-left: 31px;
    margin-right: 31px;
  }
}
</style>