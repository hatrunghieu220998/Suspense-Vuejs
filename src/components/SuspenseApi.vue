<template>
  <div v-if="error">
    {{ error }}
  </div>
  <Suspense>
    <template #default>
      <div v-for="item in articleList" :key="item.id">
        <article>
          <h2>{{ item.title }}</h2>
          <p>{{ item.body }}</p>
        </article>
      </div>
    </template>
    <template #fallback> Articles loading... </template>
  </Suspense>
</template>
<script>
import axios from "axios";
import { onErrorCaptured, ref } from "vue";
export default {
  async setup() {
    const error = ref(null);
    onErrorCaptured((e) => {
      error.value = e;
      return true;
    });
    let articleList = await axios
      .get("https://jsonplaceholder.typicode.com/posts")
      .then((response) => {
        console.log(response.data);
        return response.data;
      })
      .catch();
    return {
      error,
      articleList,
    };
  },
};
</script>
