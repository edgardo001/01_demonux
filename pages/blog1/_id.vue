<template>
  <div class="container">
    <div class="card">
      <div class="card-body">
        <h1>{{articulo.title}}</h1>
        <p class="small">{{articulo.userId}} - {{usuario.email}}</p>
        <p>{{articulo.body}}</p>
        <nuxt-link to="/blog1" class="btn btn-primary">Atras</nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return{
        articulo: '',
        usuario: '',
    }
  },
  async created() {
    try {
      const res = await axios.get(`http://jsonplaceholder.typicode.com/posts/${this.$route.params.id}`);      
      this.articulo = res.data;

      const resAutor = await axios.get(`http://jsonplaceholder.typicode.com/users/${this.articulo.userId}`);      
      this.usuario = resAutor.data;
    } catch (error) {
      console.log(error)
    }
  }
}
</script>