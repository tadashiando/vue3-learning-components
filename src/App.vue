<script>
import { defineComponent, ref, computed, onMounted } from 'vue';
import ButtonCounter from './components/ButtonCounter.vue'
import BlogPost from './components/BlogPost.vue';
import PaginatePost from './components/PaginatePost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';

export default defineComponent({
  setup() {
    const posts = ref([]);
    const postXpage = 5;
    const start = ref(0);
    const end = ref(postXpage);
    const postsLength = computed(() => {
      return posts.value.length;
    })
    const favorito = ref('Post');

    const loading = ref(true);

    const toggleFavourite = (title) => {
      favorito.value = title
    };

    const toggleNext = () => {
      if (end.value < posts.value.length) {
        start.value = start.value + postXpage;
        end.value = end.value + postXpage;
      }
    }

    const togglePrevious = () => {
      if (start.value > 0) {
        start.value = start.value - postXpage;
        end.value = end.value - postXpage;
      }
    }

    // onMounted(() => {
    //   fetchData();
    // })

    const fetchData = async () => {
      try {
        const res = await fetch('https://jsonplaceholder.typicode.com/posts')
        posts.value = await res.json();
      } catch (error) {
        console.log(error);
      } finally {
        loading.value = false;
      }
    }

    fetchData()

    return {
      end,
      favorito,
      loading,
      posts,
      postsLength,
      postXpage,
      start,
      toggleFavourite,
      toggleNext,
      togglePrevious
    }
  },
  components: { ButtonCounter, BlogPost, PaginatePost, LoadingSpinner }
})

</script>

<template>
  <LoadingSpinner v-if="loading" />
  <div class="container" v-else="loading">
    <h1>{{ favorito }}</h1>

    <PaginatePost class="mb-2" @next="toggleNext" :start="start" :end="end" :postsLength="postsLength"
      @previous="togglePrevious" />

    <BlogPost v-for="post in posts.slice(start, end)" :title="post.title" :message="post.message" :id="post.id"
      :colorText="post.colorText" @toggleFavourite="toggleFavourite" class="mb-2" />
  </div>
</template>