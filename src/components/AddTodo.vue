<template>
    <div>
        <form @submit="addTodo">
            <input type="text" v-model="title" name="title" placeholder="Add ToDo">
            <input type="submit" class="btn" value="submit">
        </form>
    </div>
</template>

<script>
export default {
    name: "AddTodo",
    data(){
        return{
            title: ''
        }
    },
    methods: {
        addTodo(e){
            e.preventDefault();
            const newTodo = {
                title: this.title,
                completed: false
            }

            this.$emit('add-todo', newTodo);

            this.title = '';
        }
    }
}
</script>

<style scoped>
    input[type="text"]{
        flex: 10;
        padding: 5px;
        border: 2px;
    }


    form{
        display: flex;
    }
    input[type="submit"]{
        flex: 2;
    }
</style>