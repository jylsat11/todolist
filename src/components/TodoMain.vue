<template>
  <div class="page">
    <header><h1>Vue Fire todo1</h1></header>
    <main>
      <div class="todos">
        <div class="write" v-if="writeState==='add'"> <!--등록-->
          <input ref="writeArea" type="text" v-model="addItemText" @keyup.enter="addItem"/>
          <button class="btn add" v-on:click="addItem">Add</button>
        </div>
        <div class="write" v-else> <!--수정-->
          <input ref="writeArea" type="text" v-model="editItemText" @keyup.enter="editSave"/>
          <button class="btn add" v-on:click="editSave">Save</button>
        </div>
        <ul class="list">
          <li v-for="(item, i) in todos" :key="i">
            <!-- <i class="far fa-check-square"></i> -->
            <i :class="[item.state==='yet' ? 'far' :'fas', 'fa-check-square']" @click="checkItem(i)"></i>
            <span>
              {{ item.text }}
              <b>
                <a href="" v-on:click.prevent="editshow(i)">Edit</a>
                <a href="" v-on:click.prevent='delItem(i)'>Del</a>
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
            crrEditItem:'',
            writeState:'add',
            editItemText:'',
            todos:[
            {text: '공부하기', state: 'yet'},
            {text: '운동하기', state: 'done'},
            {text: '글쓰기', state: 'done'},
        ],
        }
    },
    methods: {
        editshow(index) {
            this.crrEditItem = index;
            this.writeState = 'edit';
            this.editItemText = this.todos[index].text;
        },
        editSave() {
            this.todos[this.crrEditItem].text = this.editItemText;
            this.writeState='add';
        },
        addItem() {
            if (this.addItemText==='') return; 
            this.todos.push({
                text: this.addItemText, state: 'yet'
            });
            this.addItemText='';
        },
        delItem(index){
            this.todos.splice(index,1)
        },
        checkItem(index) {
            let status = this.todos[index].state;
            console.log(status);
            if (status==='yet') {
                this.todos[index].state = 'done';
            }
            else {
                this.todos[index].state = 'yet';
            }
            
        }
    },
    mounted() {
        this.$refs.writeArea.focus()
    }
}
</script>

<style>

</style>