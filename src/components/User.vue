<template>
  <h3>Hello from User component</h3>
  <h5>{{ user }}</h5>
</template>

<script>
export default {
  name: "UserComponent",
  async setup() {
    const promise = new Promise((resolve, reject) => {
      setTimeout(function () {
        reject("Success");
      }, 2000);
      console.log(resolve);
    });
    const user = await promise;
    return {
      user,
    };
  },
};
</script>

<style></style>
