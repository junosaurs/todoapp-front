<template>
    <form class="column_right" @submit.prevent="onSubmit">
        <label for="name">*&nbsp;Название</label>
        <input type="text" class="task" name="name" id="name" v-model='title'>
        <label class="note" for="com">*&nbsp;Описание</label>
        <textarea class="comment" name="comment" id="com" v-model='comm'></textarea>
        <button class="add" type="submit" ><span>Добавить дело</span></button>
    </form>
</template>

<script>
export default {
    data() {
        return {
            title: '',
            comm: '',
        }
    },
    methods: {
        onSubmit(){
            console.log('add', this.title, this.comm)
            if(this.title.trim()){
                const newTodo = {
                    id: todo.id,
                    title: this.title,
                    description: this.comm,
                    completed: false,
                    active:false
                }
                this.$emit('add-todo', newTodo)
                this.title = '', this.comm = ''
            }
        }
    },
}
</script>