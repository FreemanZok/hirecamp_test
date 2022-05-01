<template>
  <div class="">
    <div class="text-center my-container px-4">
      <h2 class="mb-4 py-2">
        hello, this is a test...
      </h2>
      <div>
        <v-select :items="myItems" label="Solo field" solo></v-select>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",

  data: () => ({
    myItems:['Foo', 'Bar', 'Fizz', 'Buzz'],
  }),
};
</script>
<style lang="scss" scoped>
.my-container {
  max-width: 800px;
  margin: 0 auto;
  background: rgb(200, 248, 252);
  min-height: 100vh;
}
</style>