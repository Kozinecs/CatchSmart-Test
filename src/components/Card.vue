<template>
  <div class="card">
    <div class="date">
      <span>{{moment(item.date).fromNow()}}</span>
      <button v-on:click="$emit('removeItem')">remove</button>
    </div>
    <h2>{{item.title}}</h2>
    <p>{{item.content}}</p>
    <div class="badge">
      <span v-for="(tag, index) in item.tags" :key="index">{{tag}}</span>
    </div>
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
      moment: moment
    }
  }
};
</script>

<style lang="scss" scoped>
.card {
  cursor: pointer;
  text-align: left;
  padding: 26px;
  background-color: #d8d8d8;
  border-radius: 8px;
  transition: 0.3s ease-out;
  border: 1px solid #ebebeb;
  display: flex;
  flex-direction: column;
  position: relative;
  z-index: 1;
  user-select: none;
  &:hover {
    box-shadow: 2px 0px 25px 0px rgba(0, 0, 0, 0.2);
    transition: 0.3s ease-out;
    .date {
      button {
        display: flex;
      }
    }
  }
  .date {
    display: flex;
    position: relative;
    z-index: 2;
    justify-content: space-between;
    button {
      display: none;
    }
  }
}
</style>