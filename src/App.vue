<template>
  <section class="container">
    <header>
      <h1>Shopping list</h1>
    </header>
    <section id="add" class="container">
      <input v-model="input" />
      <button :disabled="checkLenght()" @click="addItem()">Add to list</button>
    </section>

    <section id="active" class="container">
      <h2>Active Items</h2>
      <ul>
        <li v-for="item in validItems" :key="`item-${item.id}`">
          <span @click="deleteItem(item)" style="margin-right: 15px">X</span>
          <span>{{ item.text }}</span>
        </li>
      </ul>
    </section>

    <section class="container">
      <h2>Deleted Items</h2>
      <ul>
        <li v-for="item in deletedItems" :key="`item-${item.id}`">
          <span style="text-decoration: line-through"> {{ item.text }}</span>
        </li>
      </ul>
    </section>
  </section>
</template>

<script>
export default {
  data() {
    return {
      input: "",
      list: [],
    };
  },
  methods: {
    addItem() {
      this.list.push({
        id: this.list.length + 1,
        text: this.input,
        is_deleted: false,
      });
      this.input = "";
    },
    deleteItem(item) {
      item.is_deleted = true;
    },
    checkLenght() {
      let check;
      this.input.length > 0 ? (check = false) : (check = true);
      return check;
    },
  },
  computed: {
    validItems() {
      return this.list.filter((item) => !item.is_deleted);
    },
    deletedItems() {
      return this.list.filter((item) => item.is_deleted);
    },
  },
};
</script>

<style>
header {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 0.5rem;
  background-color: #2d8791;
  color: white;
  text-align: center;
  border-radius: 16px;
}

.container {
  text-align: center;
  padding-bottom: 0.5rem;
  margin: 2rem auto;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  border-radius: 12px;
  font-family: "Jost", sans-serif;
}
section {
  width: 90%;
  max-width: 40rem;
}
input {
  padding: 1rem;
  font-size: large;
}
button {
  font: inherit;
  border: 1px solid #88005b;
  background-color: #88005b;
  color: white;
  padding: 1rem;
  border-radius: 12px;
  margin: 1rem;
  width: 12rem;
  cursor: pointer;
  box-shadow: 1px 1px 4px rgba(0, 0, 0, 0.26);
}
button:active {
  background-color: #af0a78;
  border-color: #af0a78;
  box-shadow: 1px 1px 8px rgba(0, 0, 0, 0.26);
}

ul {
  list-style: none;
}
</style>
