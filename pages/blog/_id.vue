<template>
  <div class="container">
    <div class="card">
      <div class="card-body">
        <h1>{{articulo.title}}</h1>
        <p class="small">{{articulo.userId}} - {{articulo.nombreAutor}}</p>
        <p>{{articulo.body}}</p>
        <nuxt-link to="/blog" class="btn btn-primary">Atras</nuxt-link>
      </div>
    </div>
    {{persona.apellido}}
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
    }
  },
  async created() {

  },
  // habilidad de nuxt
  // Espera realizar todas las peticiones a la DB para luego segir cargando el sitio de forma normal.
  // en comparacion con created, este no espera a llenar todas las variables y puede dar problemas de llenado.
  // con este metodo, no es posible acceder a todos los "articulos", esto es porque todavia no se crean las variables de "data" para recibirlos
  // los "this." no funcionan
  // "params" : Parametros de la URL
  async asyncData({
    isDev,
    route,
    store,
    env,
    params,
    query,
    req,
    res,
    redirect,
    error
  }) {
    try {
      const res = await axios.get(`http://jsonplaceholder.typicode.com/posts/${params.id}`);      
      const articulo = res.data;
      console.log(articulo)
      const resAutor = await axios.get(`http://jsonplaceholder.typicode.com/users/${res.data.userId}`);      
      console.log(resAutor)
      articulo.nombreAutor = resAutor.data.name;

      //Retorno extra de ejemplo
      const persona = { nombre : "edgardo" , edad : 29}
      persona.apellido = "vasquez"
      
      return {articulo, persona};

    } catch (error) {
      console.log(error)
      return {error: error}
    }
  },
}
</script>