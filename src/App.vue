<!-- 
<script>
/
  components: { PaginatePost },/ import ButtonCounter from "./components/ButtonCounter.vue"; // import the component
// import BlogPost from "./components/BlogPost.vue"; // import the component
// import { ref } from "vue";

// const posts = ref([
//   { id: 1, title: "Post 1", body: "Descripcion 1" },
//   { id: 2, title: "Post 2", body: "Descripcion 2" },
//   { id: 3, title: "Post 3", body: "Descripcion 3" },
//   { id: 4, title: "Post 4" },
// ]);

// const favorito = ref("");
// const cambiarfavorito = (title) => {
//   favorito.value = title;
// };
// 
</script>

// <template>
// <div class="container mx-auto">
    // <h1>APP</h1>
    // <div class="flex space-x-4">
        //
        <ButtonCounter /> //use the component primera manera de escribirlo
        //
        <button-counter /> //use the component segunda manera de escribirlo
        // </div>
    // <h1 class="text-4xl font-semibold">Mi Post Favorito: {{ favorito }}</h1>
    //
    <BlogPost // v-for="post in posts" // :key="post.id" // :title="post.title" // :id="post.id" // :body="post.body" // @cambiarfavorito="cambiarfavorito" // />
    // </div>
// </template> -->

<script setup>
import BlogPost from "./components/BlogPost.vue";
import LoadingSpinner from "./components/LoadingSpinner.vue";
import PaginatePost from "./components/PaginatePost.vue";

import { computed, onUnmounted, ref } from "vue";

const posts = ref([]);
const postxpage = 10;
const inicio = ref(0);
const fin = ref(postxpage);
const loading = ref(true);

const favorito = ref("");

const cambiarfavorito = (title) => {
  favorito.value = title;
};
const eliminarfavorito = () => {
  favorito.value = "";
};

const next = () => {
  inicio.value = inicio.value + postxpage;
  fin.value = fin.value + postxpage;
};
const prev = () => {
  inicio.value = inicio.value - postxpage;
  fin.value = fin.value - postxpage;
};
const ini = () => {
  inicio.value = 0;
  fin.value = postxpage;
};
const fn = () => {
  inicio.value = posts.value.length - postxpage;
  fin.value = posts.value.length;
};


fetch("https://jsonplaceholder.typicode.com/posts")
  .then((response) => response.json())
  .then((data) => {
    posts.value = data;
  })
  .finally(() => {
    loading.value = false;
  });

  const maxlength = computed(() => {
  return posts.value.length;
});
</script>

<template>
  <LoadingSpinner v-if="loading"/>
  <div class="container mx-auto my-2" v-else>
    <h1>APP</h1>
    <div>
      <h1 class="text-4xl font-semibold">Mi Post Favorito: {{ favorito }}</h1>
      <paginate-post 
        class=" mt-1"
        @next="next"
        @prev="prev"
        :inicio="inicio"
        :fin="fin"
        :maxlength="maxlength"
        @ini="ini"
        @fn="fn"
        />
      <BlogPost
        v-for="post in posts.slice(inicio, fin)"
        :key="post.id"
        :title="post.title"
        :id="post.id"
        :body="post.body"
        @cambiarfavorito="cambiarfavorito"
        @eliminarfavorito="eliminarfavorito"
      />
    </div>
  </div>
</template>
