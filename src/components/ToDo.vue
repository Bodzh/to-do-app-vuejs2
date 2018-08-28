<template>
    <div class="container-fluid">
        <h3>ToDo app with Vue.js2</h3>
        <form class="add-form " v-on:submit.prevent="addToDo">
            <input type="text" v-model="newTodo" placeholder="add todo...">
            <button class="btn btn-success" type="submit"><strong class="glyphicon glyphicon-plus"></strong></button>
        </form>
        <div class="row">
                <div>
                <h3>What you need to do...</h3>
                <fieldset>
                    <div v-for="toDo in toDos" class="todo" v-if="!toDo.done">
                        <input @click="toggleDone(toDo)" type="checkbox" id="todo" value="todo">
                        <label for="todo" v-text="toDo.description"></label>
                        <button class="btn btn-warning" v-on:click="deleteTodo(toDo)">Delete</button>
                    </div>
                </fieldset>
            </div>
                <div>
                <h3>What you've already done!)</h3>
                <fieldset>
                    <div v-for="toDo in toDos" class="todo done" v-if="toDo.done">
                        <input @click="toggleDone(toDo)" type="checkbox" id="todo" value="todo" checked>
                        <label class="done-text" for="todo" v-text="toDo.description"></label>
                        <button class="btn btn-warning" v-on:click="deleteTodo(toDo)">Delete</button>
                    </div>
                </fieldset>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'ToDo',
        data() {
            return {
                toDos: [],
                newTodo: ''
            }
        },
        mounted() {
            if (localStorage.getItem('toDos')) {
                try {
                    this.toDos = JSON.parse(localStorage.getItem('toDos'));
                } catch (e) {
                    localStorage.removeItem('toDos');
                }
            }
        },
        methods: {
            addToDo() {
                this.toDos.push({description: this.newTodo, done: false});
                localStorage.description = this.newTodo;
                localStorage.done = false;
                this.newTodo = '';
                this.saveTodos();
            },
            deleteTodo(todo) {
                let index = this.toDos.indexOf(todo);
                console.log(index);
                this.toDos.splice(index, 1);
                this.saveTodos();
            },
            toggleDone(toDo) {
                if (toDo.done) {
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
    .row {
        display: flex;
        flex-direction: row;
        justify-content: space-around;
        color: dimgray;
    }

    .todo {
        border-bottom: 1px solid forestgreen;
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
        padding: 5px;
    }

    .todo:last-child {
        border: 0px;
    }

    .todo > * {
        margin: 5px;
    }

    .done-text {
        text-decoration: line-through;
    }

    .add-form {
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: stretch;
    }

    form > input {
        border: 1px solid darkgrey;
        border-radius: 5px 0px 0px 5px;
        padding: 5px;
    }

    .btn-success {
        border-radius: 0px 5px 5px 0px;

    }

</style>
