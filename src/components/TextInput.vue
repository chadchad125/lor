<template>
    <div>
      <label for="fname">{{title}}</label><br>
      <input type="text" :name="title" value="">
    </div>
</template>

<script>
export default {
  name: 'TextInput',
  props: {
    title: String,
    fieldName: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
