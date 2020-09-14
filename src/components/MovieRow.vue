<template>
  <div>
    <h2>{{title}}</h2>

  </div>
</template>

<script>
export default {
  name: "MovieRow",
  props: {
    title: String,
    items: Array
  },
  mounted() {
    console.log(this.items);
  }
}

</script>

<style scoped>

</style>