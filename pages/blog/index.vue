<template>
  <div class="container mt-5">
    <ul>
      <li>
        <nuxt-link to="/blog/1">Articulo #1</nuxt-link>
      </li>
      <li>Articulo #2</li>
    </ul>
    <hr>
    <div class="row">
      <div class="col-md-3" v-for="(item, index) in articulos_0" :key="index">
        <h2>
          <nuxt-link :to="`/blog/${item.id}`">{{item.titulo}}</nuxt-link>
        </h2>
      </div>
    </div>
    <hr>   
    <!---->
    <div class="card my-2" v-for="(item, index) in articulos" :key="index">
      <div class="card-body">
        <nuxt-link :to="`blog/${item.id}`">{{item.title}}</nuxt-link>
        <p>{{item.body}}</p>
      </div>
    </div>
    <!---->
  </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
          articulos_0: [{
              id: 1,
              titulo: 'Titulo #1'
            },
            {
              id: 2,
              titulo: 'Titulo #2'
            },
            {
              id: 3,
              titulo: 'Titulo #3'
            },
            {
              id: 4,
              titulo: 'Titulo #4'
            },
            {
              id: 5,
              titulo: 'Titulo #5'
            }
          ],
          articulos: []
        }
      },
      async created() {
        try {
          const res = await axios.get('http://jsonplaceholder.typicode.com/posts?_limit=10');
          console.log(res.data);
          this.articulos = res.data;
        } catch (error) {
          console.log(error)
        }
      }
    }
</script>