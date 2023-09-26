<template>
  <div class="popup">
    <h1>Popup</h1>
    <blockquote>
      <p>{{ state.quote }}</p>
      <cite>{{ state.author }}</cite>
    </blockquote>
  </div>
</template>
<script>
export default{
  data(){
    return {
      state: {
        quote: '',
        author: ''
      }
    }
  },
  async created(){
    try {
      const response = await fetch('https://zenquotes.io/api/random')
      const data = await response.json()
      if (Array.isArray(data)&&data.length>0){
        this.state.quote = data[0].q
        this.state.author = data[0].a
      } else{
        this.state.quote = 'No quote'
      }
    }catch(e){
      console.error(e)
      this.state.quote = 'Error quote'
    }
  }
}
</script>