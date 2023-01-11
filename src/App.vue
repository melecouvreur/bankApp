<script>
import Box from './components/Box.vue';

export default {
  name: "App",

  components: {
    Box,
  },

data() {
  return {
    amount: 0,
    name: "",
    id: 3,
    items: [
      {id: 1, name: "Food", amount: -30 },
      {id: 2, name: "Transport", amount: -10 },
      {id: 3, name: "Salary", amount: 150 },
    ],
    searchTerm: "",
  };
},
   methods: {
    addItem() {
      this.id++;
      const newItem = {
        id: this.id,
        name: this.name,
        amount: this.amount,
      };
      console.log(newItem);
      this.items.push(newItem)
      console.log(this.items);
      this.name= "";
      this.amount = 0;
    },
  },
    computed: {
      income() {
        return this.items
        .filter((i) => i.amount > 0)
        .reduce((acc, e) => acc + e.amount, 0)
      },
      expenses() {
        return this.items
        .filter((i) => i.amount < 0)
        .reduce((acc, e) => acc + e.amount, 0)
      },
      balance() {
        return this.income + this.expenses; //can create computed property from computed properties
      },
      filteredItems() {
        console.log(this.filteredItems)
        return this.items.filter((item) => item.name.toLowerCase().includes(this.searchTerm.toLowerCase())) //filter based on dynamic value
      },
    },
  }
</script>


<template>

<div class="container">
  <h1>Bank App</h1>
  <div class="row mb-4">
    <Box :amount="income" title="Income"/>
    <Box :amount="expenses" title="Expenses"/>
    <Box :amount="balance" title="Balance"/>
  </div>

<div class="d-flex mt-4">
      <label> Category </label>
      <input type="text" placeholder="add a new item" v-model="name" />
      <label> Amount  </label>
      <input type="number" placeholder="amount" v-model.number="amount" />
      <button @click="addItem">Add</button>
</div>

<div class="d-flex mt-4">
  <label> Search </label>
  <input type="text" placeholder="Type here" v-model="searchTerm"/>
</div>

<div>
  <ul class="mt-4 list-group">
    <li v-for="item in filteredItems" 
    :key="item.id"
    class="d-flex list-group-item justify-content-between align-items-center"> <!--can run loop on computed property-->
      <span> {{ item.name }}: </span>
      <span> $ {{ item.amount }} </span>
    </li>
  </ul>
</div>

</div>

</template>

<style scoped>
.hide {
  display: none;
}
</style>
