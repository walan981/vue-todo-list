<template>
    <div class="container">
        <h1>Comments</h1>
        <hr/>
        <div class="form-todo form-group">
            <p>
                <input placeholder="name" type="text" name="author"
                class="form-control" v-model='newName'/>
            </p>
            <p>
                <textarea placeholder="comment" name="message"
                class="form-control" v-model='newMessage'></textarea>
            </p>
            <button v-on:click='addComment' type="submit" class="btn btn-primary">
                Comment
            </button>
        </div>
        <br/>
        <div class="list-group">
            <p v-if="comments.length<=0">No comments yet...</p>
            <div class="list-group-item" v-for='(comment, index) in allComments'
            :key="index">
                <span class="comment_author">Author: <strong>{{
                    comment.name
                }}</strong>
                </span>
                <p>{{ comment.message }}</p>
                <div>
                    <a href="#" title="delete" v-on:click.prevent='deleteComment(index)'>
                        delete
                    </a>
                </div>
            </div>
        </div>
        <hr/>
    </div>
</template>

<script>
export default{
    data(){
        //onde sao declararadas as variaveis
        return{
            comments: [],
            newName: '',
            newMessage: ''
        }
    },
    methods: {
        //onde sao declaradas as funcoes
        addComment(){
            if(this.newMessage.trim()==''){
                return
            }
            this.comments.push({
                name: this.newName,
                message: this.newMessage
            })
            //apagar inputs dos formularios
            this.name = '';
            this.message = '';
        },
        deleteComment(index){
            this.comments.pop(index,1)
        }
    },
    computed: {
        //modifica o comportamento no frontend
        allComments(){
            return this.comments.map(comment =>({
                ...comment, //retorna as proprias propriedades do objeto
                 name: comment.name.trim() == '' ? 'Anonymous' : comment.name   
            }))
        }
    },
    watch: {
        //monitora alteracao em qualquer propriedade (parecido com o Onsnaphot)
        comments(val){
            console.log('val', val)
        }
    }
}
</script>
