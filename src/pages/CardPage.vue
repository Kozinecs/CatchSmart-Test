<template>
  <div class="card-grid">
    <card
      v-for="(item, index) in cardList"
      :key="index"
      :item="item"
      :id="index"
      v-on:click.native.self="openModal(item, index)"
      v-on:removeItem="removeItem(index)"
    />
    <button @click="addCard">Add Card</button>
    <modal v-if="showModal" v-on:toggle-modal="toggleModal" :item="clickedCard" :id="clickedId" v-on:saveNewCard="saveNewCard"/>
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
      cardList: [
        {
          date: "24/04/2020",
          title: "Some text here",
          content: "Some content goes here",
          tags: ["work", "home"]
        },
        {
          date: "25/04/2020",
          title: "Some bla bla",
          content: "Some content goes here asd asd asd asd ",
          tags: ["work", "home"]
        }
      ],
      clickedCard: {},
      clickedId: Number,
      showModal: false,
      newCard: null
    };
  },
  mounted() {
    if (localStorage.getItem("cardList")) {
      try {
        this.cardList = JSON.parse(localStorage.getItem("cardList"));
      } catch (e) {
        localStorage.removeItem("cardList");
      }
    }
  },
  methods: {
    openModal(item, index) {
      console.log(item, index);
      this.clickedCard = item;
      this.clickedId = index;
      this.showModal = !this.showModal;
    },
    removeItem(index) {
      this.cardList.splice(index, 1);
      this.saveCard();
    },
    toggleModal() {
      console.log("toggle modal");
      this.showModal = !this.showModal;
    },

    addCard() {
      event.preventDefault();
      this.openModal({}, this.cardList.length + 1);
    },
    saveNewCard(card) {
      this.newCard = card;
      this.cardList.push(this.newCard);
      this.saveCard();
    },
    saveCard() {
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
}
</style>