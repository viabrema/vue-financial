<template>
  <div>
    <h1>{{ data.month }}/{{data.year}}</h1>
    <h2>Entradas</h2>
    <ul>
      <li v-for="(entry, index) in data.entries" :key="index">
        <span><input type="text" v-model="entry.name"></span>
        <span><input type="text" v-model="entry.value"></span>
      </li>
      <li><span>Total</span><span>{{entryTotal}}</span></li>
    </ul>

    <h2>Saídas</h2>
    <ul>
      <li v-for="(expense, index) in data.expenses" :key="index">
        <span><input type="text" v-model="expense.name"></span>
        <span><input type="text" v-model="expense.value"></span>
      </li>
      <li><span>Total</span><span>{{expenseTotal}}</span></li>
    </ul>

    <h2>Saldo Total: {{entryTotal - expenseTotal}}</h2>

    <entry @cadastre="cadastre"></entry>
  </div>
</template>

<script>
import { reactive, computed } from "vue";
import Entry from './components/Entry.vue';


export default {
  name: "App",

  setup(props) {
    const data = reactive({
      month: 5,
      year: 2021,
      entries: [{ name: "Inicial", value: 0.0 }],
      expenses: [{ name: "Inicial", value: 0.0 }],
    });


    const entryTotal = computed(() => {
      let total = 0;
      data.entries.forEach(e => {
        total = Number(total) + Number(e.value);
      });
      return total;
    })

    const expenseTotal = computed(() => {
      let total = 0;
      data.expenses.forEach(e => {
        total = Number(total) + Number(e.value);
      });
      return total;
    })

    function cadastre(res){
      if(res.type == 1){
        data.entries.push(res.data);
      }else{
        data.expenses.push(res.data);
      }
    }

    return {
      data,
      cadastre,
      entryTotal,
      expenseTotal
    };
  },
  components: {
    Entry

  },
};
</script>

<style lang="stylus"></style>
