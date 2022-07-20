<template>
    <div>
        <h2>Lista de posts</h2>
        <PostsListaIten v-for="post in posts" :key="post.id" :post="post">
            <slot :meuEscopo="post"></slot>
        </PostsListaIten>
    </div>
</template>

<script>
import PostsListaIten from './PostsListaIten.vue'
export default {

    props: {
        posts: {
            type: Array,
            required:true
        }
    },
    components: {
         PostsListaIten
    }
}
</script>