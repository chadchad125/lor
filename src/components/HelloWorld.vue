<template>
  <div class="hello">
    <button @click="AddInput('textInput')">Add TextInput</button>
    <button @click="AddInput('textArea')">Add TextArea</button>
    <br>
    <hr/>
    <form action="/action_page.php">
      <div v-for="(item, inx) in data" :key="inx">
        <TextInput v-if="item.type === 'textInput'" :title="item.text"/>
        <TextArea v-if="item.type === 'textArea'" :title="item.text"/>
      </div>
    </form> 
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      data: [
        {
          type: "textInput",
          text: "first name"
        },
        {
          type: "textInput",
          text: "Last name"
        },
        {
          type: "textArea",
          text: "What are your views on the world?"
        },
      ]
    }
  },
  methods: {
    AddInput(type){
      let textInputTemplate = {type:"textInput",text:"input"};
      let textAreaTemplate = {type:"textArea",text:"area"};
      switch(type){
        case "textInput": this.data.push(textInputTemplate); break;
        case "textArea": this.data.push(textAreaTemplate); break;
      }
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
textarea{
  width: 70%;
  height: 100px;
}
</style>
