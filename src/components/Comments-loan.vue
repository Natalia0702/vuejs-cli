<template>
  <div class="container">
  <h1>Solicitações de Empréstimo</h1>
  <hr/>
  <div class="form-todo form-group">
    <p>
      <input placeholder="name" type="text" name="user" class="form-control" v-model="name"/>
    </p>
    <p>
      <select class="form-select" aria-label="Default select example">
        <option selected>Instituição</option>
        <option value="1">One</option>
        <option value="2">Two</option>
        <option value="3">Three</option>
      </select>
    </p>
    <p>
      <textarea placeholder="comment" name="message" class="form-control" v-model="message"></textarea>
    </p>
      <button v-on:click="addComment" type="submit" class="btn btn-primary">Comentar </button>
  </div>
  <br>
  <div class="list-group">
    <div class="list-group-item" v-for="(comment, index) in allComments" :key="comment.id">
      <span class="comment_user">User: <strong>{{comment.name}}</strong></span>
      <p>{{comment.message}}</p>
      <a href="#" title="Delete" v-on:click.prevent="removeComment(index)">Delete</a>
    </div>
  </div>
  <hr/>
</div>
</template>

<script>
export default{
data(){
  return {
    comments: [],
    name: '',
    message:''
    }
  },
methods:{
    addComment(){
      if(this.message.trim() === ''){
        return;
      }
     this.comments.push({
        name: this.name,
        message: this.message
      });
      this.name = '';
      this.message = '';
    },
    removeComment(index){
      this.comments.splice(index, 1);
    }
  },
  computed:{
    allComments(){
      return this.comments.map(comment => ({
        ...comment,
        name: comment.name.trim() === '' ? 'Anônimo' : comment.name
      }))
    }
  },
  watch:{
    comments(val){
      console.log('val',val)
    }
  }
}
</script>

<style>
</style>
