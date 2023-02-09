<template>
  <div class="page">
    <header><h1>Vue Fire todo1</h1></header>
    <main>
      <div class="todos">
        <div class="write">
          <input id="text1" type="text" @keyup.enter="addItem"/>
          <button class="btn add" v-on:click="addItem">Add</button>
        </div>
        <ul class="list">
          <li v-for="item in todos" :key="item.text">
            <!-- <i class="far fa-check-square"></i> -->
            <i :class="[item.state==='yet' ? 'far' :'fas', 'fa-check-square']"></i>
            <span>
              {{ item.text }}
              <b>
                <a href="" >Edit</a>
                <a href="">Del</a>
              </b>
            </span>
          </li>
        </ul>
      </div>
    </main>
  </div>
 
</template>

<script>
export default {
    data() {
        return {
            addItemText:'',
            todos:[
            {text: '공부하기', state: 'yet'},
            {text: '운동하기', state: 'done'},
            {text: '글쓰기', state: 'done'},
        ],
        }
    },
    methods: {

        addItem() {
            let input= document.querySelector('input');
            this.addItemText=input.value;
            this.todos.push({
                text: this.addItemText, state: 'yet'
            })
        }
    }
}
</script>

<style>

</style>