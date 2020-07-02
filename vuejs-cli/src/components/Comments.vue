<template>
    <div class="container">
        <h1>Comentários</h1>
        <hr />
        <FormTodo v-on:add-todo="addComment"></FormTodo>
        <div class="list-group">
            <p v-if="comments.length <= 0">Sem Comentários</p>
            <div class="list-group-item" v-for="(comment, index) in allComents" v-bind:key="index">
                <span class="comment__author">Autor: <strong>{{ comment.name }}</strong></span>
                <p>{{ comment.message }}</p>
                <div>
                    <a href="#" title="Excluir" v-on:click.prevent="removeComment(index)">Excluir</a>
                </div>
            </div>
        </div>
        <hr />
    </div>
</template>

<script>
import FormTodo from './FormTodo';
export default{
    components: {
        FormTodo
    },
    data() {
        return {
            comments: [],
        }
    },
    methods: {
        addComment(comment){
            this.comments.push(comment);
        },
        removeComment(index){
            this.comments.splice(index, 1);
        }
    },
    computed: {
        allComents() {
            return this.comments.map(comment => ({
                ...comment,
                name: comment.name.trim() === '' ? 'Anônimo' : comment.name
            }))
        }
    },
    watch: {
        comments(val) {
            console.log('val', val)
        }
    }
}
</script>

