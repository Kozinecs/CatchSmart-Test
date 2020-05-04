<template>
  <div class="card">
    <div class="date">
      <span>{{moment(item.date).fromNow()}}</span>
      <button @click.stop="$emit('deleteCard')">&#10006;</button>
    </div>
    <h2>{{item.title}}</h2>
    <p>{{item.content}}</p>
    <div class="badge">
      <span v-for="(tag, index) in item.tags" :key="index">{{tag}}</span>
    </div>
  </div>
</template>
 
<script>
import moment from "moment";

export default {
  props: {
    item: Object,
    id: Number
  },
  data() {
    return {
      moment
    };
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
  h2 {
    margin-bottom: 0px;
  }
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
    height: 30px;
    display: flex;
    align-items: center;
    position: relative;
    z-index: 2;
    justify-content: space-between;
    button {
      display: none;
      border: none;
      background: none;
      outline: none;
      color: #c50909;
      cursor: pointer;
      font-size: 20px;
      line-height: 30px;
    }
    span {
      line-height: 30px;
    }
  }
  .badge {
    margin-top: auto;
    span {
      padding: 4px 8px;
      background-color: #845ec2;
      color: rgb(219, 219, 219);
      border-radius: 16px;
      margin-right: 8px;
    }
  }
}

@media screen and (max-width: 1200px) {
  .card {
    .date {
      button {
        display: flex;
      }
    }
  }
}
</style>