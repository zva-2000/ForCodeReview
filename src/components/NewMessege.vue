<template>
    <div class="NewMessege">
      <p>{{ NewMessege }}</p>
      <p>{{ NewImr }}</p>      
    </div>
</template>
  
<script>
  export default {
    props: {
        NewMessege: {
        type: String,
        required: true
      },
      NewImr: {
        type: String,
        required: true
      },
    }
  }
</script>
  
<style lang="scss" scoped>
.NewMessege {
  text-align: center;
  padding: 20px;
}
p {
  color: #ba3838;
}
</style>