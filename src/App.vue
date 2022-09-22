<template>
  <h2>
    Suspense là một tính năng mới kết xuất thành phần default/fallback cho đến
    khi thành phần chính tìm nạp dữ liệu.
    <br />
    Suspense là tạm dừng render component chính của chúng ta, thay vào đó hiển
    thị 1 nội dung khác, và cho tới khi nào component chính của chúng ta được
    download về nếu đó là async component (lazy load) hoặc cho tới khi nào hoàn
    thành một công việc async nào đó ở trong setup.
    <br />
    Vue 3 cũng cung cấp cho ta 1 hook đó là onErrorCaptured để bắt lỗi nếu trong
    quá trình xử lý các tác vụ trong setup() khi xảy ra lỗi.
  </h2>
  <div v-if="error">
    Error loading component
    {{ error }}
  </div>
  <Suspense v-else>
    <template #default>
      <user-component></user-component>
    </template>
    <template #fallback>
      <div>Loading...</div>
    </template>
  </Suspense>
  <button @click="suspenseApiStautus = !suspenseApiStautus">Suspense API</button>
  <SuspenseApi v-if="suspenseApiStautus"></SuspenseApi>
</template>

<script>
import { onErrorCaptured, ref } from "vue";
import User from "./components/User.vue";
import SuspenseApi from "./components/SuspenseApi.vue"
export default {
  name: "App",
  data() {
    return{
      suspenseApiStautus: false,
    }
  },
  components: {
    UserComponent: User,
    SuspenseApi
},
  setup() {
    const error = ref(null);
    onErrorCaptured((e) => {
      error.value = e;
      return true;
    });

    return {
      error
    }
  },
};
</script>

<style></style>
