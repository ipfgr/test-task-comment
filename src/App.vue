<template>
  <div class="container">
      <Comments/>
  </div>
</template>

<script>
import Comments from "@/components/Comments"
export default {
  name: 'App',
  components: {
    Comments
  }
}
</script>

<style>
    *{
        margin: 0;
        padding: 0;
        box-sizing: border-box;
        font-family: "Roboto", sans-serif;
    }
    .hide{
        display:none;
    }
    .container {
        display: flex;
        justify-content: center;
        align-items: center;
    }
</style>
