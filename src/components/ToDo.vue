<template>
    <div>
    <input type="text" v-model="newTodo">
    <button @click="addToDo" type="submit">add todos</button>
        <fieldset>
            <div v-for="toDo in toDos" class="todo" v-if="!toDo.done">
                <input @click="toggleDone(toDo)" type="checkbox" id="todo" name="interest" value="todo">
                <label for="todo" v-text="toDo.description"></label>
                <button v-on:click="deleteTodo(toDo)">Delete</button>
            </div>
        </fieldset>

        <fieldset>
            <div v-for="toDo in toDos" class="done" v-if="toDo.done">
                <input @click="toggleDone(toDo)" type="checkbox" id="todo" name="interest" value="todo">
                <label for="todo" v-text="toDo.description"></label>
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
          toDos: [
              {description: "go to shop", done: false},
              {description: "go market", done: true},
              {description: "go to job", done: true},
              {description: "go to barbershop", done: true},
              {description: "go home", done: false}
          ],
          newTodo:''
      }
  },
    methods:{
      addToDo(){
          this.toDos.push({description: this.newTodo,done: false});
          this.newTodo = '';
      },
      deleteTodo(todo){
          let index = this.toDos.indexOf(todo);
          console.log(index);
          this.toDos.splice(index,1);
      },
        toggleDone(toDo){
          if(toDo.done){
              toDo.done = false;
          }
          else {
             toDo.done = true;
          }
          console.log(toDo);
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
