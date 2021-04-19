<template>
    <div>
      <label for="fname">{{title}}</label><br>
      <textarea :name="fieldName"></textarea>
    </div>
</template>

<script>
export default {
  name: 'TextArea',
  props: {
    title: String,
    fieldName: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
