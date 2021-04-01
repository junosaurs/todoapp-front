<template>
    <div class="container">
        <TodoList />
        <select v-model="filter">
            <option value="all">all</option>
            <option value="completed">Completed</option>
            <option value="not-completed">Not Completed</option>
        </select>
        <Loader v-if='loading'/>
        <TodoItems
            v-else-if='filtered.length'
            v-on:remove-todo="removeTodo" 
            v-bind:todos = "filtered"
            @add-todo="addTodo"
        />
        <p v-else>No todos!</p>
        <!--@remove-todo="removeTodo"-->
        <router-link to="/">Home</router-link>
    </div>
</template>

<script>
import TodoList from "@/components/TodoList"
import TodoItems from "@/components/TodoItems"
import Loader from "@/components/Loader"
export default {
    name: 'app',
    data() {
        return {
            todos: [],
            loading: true,
            filter: 'all'
        }
    },
    mounted() {
        fetch('http://fa-todo.herokuapp.com/task/')
            .then(responce => responce.json())
            .then(json => {
                setTimeout(() => {
                    this.todos = json
                    this.loading = false
                }, 1000)      
            })
    },
    components: {
        TodoList,
        TodoItems,
        Loader,
    },

    computed: {
        filtered() {
            var filtTodos
            if(this.filter === 'all') {
                filtTodos = this.todos
            }
            if(this.filter === 'completed') {
                filtTodos = this.todos.filter(el => el.completed)
                
            }
            if(this.filter === 'not-completed') {
                filtTodos = this.todos.filter(el => !el.completed)
            }
            return filtTodos;
        }
    },

    methods: {
        removeTodo(id) {
        this.todos = this.todos.filter(el => el.id !== id)
        },
        addTodo(todo){
        this.todos.push(todo)
        }
    }
};
</script>