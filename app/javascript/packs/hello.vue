<template>
  <div>
    <ul>
      <li v-for="memo in memos" :key="memo.id">
        {{ memo.title }}: {{ memo.description }}
      </li>
    </ul>
    <div>
      <input v-model="title" placeholder="title" />
      <input v-model="description" placeholder="description" />
      <button @click="addMemo">メモを追加</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      memos: "memos",
    };
  },

  mounted() {
    this.setMemo();
  },

  methods: {
    setMemo: function () {
      axios.get("/api/memos").then((response) => (this.memos = response.data));
    },
    addMemo: function () {
      axios
        .post("/api/memos", {
          title: this.title,
          description: this.description,
        })
        .then((response) => this.setMemo());
    },
  },
};
</script>

<style scoped>
</style>
