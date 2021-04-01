<template>
    <div class="container">
            <div class="column_left">
            <ul class="window">
                <li v-for="(todo, i) of todos"
                    v-bind:key='todo'
                    v-bind:index='i'>
                    <div class="new_task">
                        <div class="head">
                            <span class="span" v-bind:class="{done:todo.completed}">
                                <input type="checkbox" class="check" v-on:change="todo.completed = !todo.completed">
                                <strong class="id_number">{{i+1}}</strong>&nbsp;
                                <strong>{{todo.title}}</strong>
                            </span>
                                <button class="delete" v-on:click="$emit('remove-todo', todo.id)">&times;</button>
                                <button class="arrow" v-on:click="todo.active = !todo.active">&or;</button>
                            <hr>
                            <div id="toggle_com" class="com" v-bind:class="{toggle:todo.active}">{{todo.description}}</div>
                        </div>
                    </div>
                </li>
            </ul>
        </div>
        <AddTodo @add-todo='addTodo'/>
    </div>
    
</template>

<script>
import AddTodo from '@/components/AddTodo'
export default {
    mounted() {
        let a = document.getElementsByClassName('span')
        console.log(a[0].classList)
        for(let i=0; i<a.length; i++){
            if(a[i].classList.contains('done')){
                a[i].childNodes[0].checked=true
            }
            
        }
        console.log(a)
    },
    components: {
        AddTodo
    },
    props:['todos'],
    methods: {
        /* removeTodo(id) {
            this.$emit('remove-todo', id)
        } */
        addTodo(todo) {
            this.$emit('add-todo', todo)
        },
    }
}
</script>

<style lang="scss" scoped>
.delete {
    background-color:red;
    color: #fff;
    border: none;
    border-radius: 50%;
    margin-left: 10px;
    outline: none;
    cursor: pointer;
    &:hover {
        border:1px solid black;
    }
}
.done {
    text-decoration: line-through;
    width: auto;
}
.toggle {
    height: 0; 
    padding: 0;
    opacity: 0;
}

</style>

