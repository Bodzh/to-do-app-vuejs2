<template>
    <div>
        <form v-on:submit.prevent="addToDo">
    <input type="text" v-model="newTodo" >
    <button type="submit">add todos</button>
        </form>

        <fieldset>
            <div v-for="toDo in toDos" class="todo" v-if="!toDo.done">
                <input @click="toggleDone(toDo)" type="checkbox" id="todo" value="todo" >
                <label for="todo" v-text="toDo.description"></label>
                <button v-on:click="deleteTodo(toDo)">Delete</button>
            </div>
        </fieldset>

        <fieldset>
            <div v-for="toDo in toDos" class="done" v-if="toDo.done">
                <input @click="toggleDone(toDo)" type="checkbox" id="todo" value="todo" checked>
                <label  for="todo" v-text="toDo.description"></label>
                <button v-on:click="deleteTodo(toDo)">Delete</button>
            </div>
        </fieldset>

    </div>
</template>

<script>
export default {
  name: 'ToDo',
  data() {
      return {
          toDos: [ ],
          newTodo:''
      }
  },
    mounted() {
        if (localStorage.getItem('toDos')) {
            try {
                this.toDos = JSON.parse(localStorage.getItem('toDos'));
            } catch(e) {
                localStorage.removeItem('toDos');
            }
        }
    },
    methods:{
      addToDo(){
          this.toDos.push({description: this.newTodo,done: false});
          localStorage.description = this.newTodo;
          localStorage.done = false;
          this.newTodo = '';
          this.saveTodos();
      },
      deleteTodo(todo){
          let index = this.toDos.indexOf(todo);
          console.log(index);
          this.toDos.splice(index,1);
          this.saveTodos();
      },
        toggleDone(toDo){
          if(toDo.done){
              toDo.done = false;
          }
          else {
             toDo.done = true;
          }
          this.saveTodos();
          console.log(toDo);
        },
        saveTodos() {
            const parsed = JSON.stringify(this.toDos);
            localStorage.setItem('toDos', parsed);
        }
    }



}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.done{
    text-decoration: line-through;
}
</style>
