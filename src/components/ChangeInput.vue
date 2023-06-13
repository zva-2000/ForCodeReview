<template>

<input type="text" v-model="note.title" v-if="index === curIndex">

<p v-bind="newTitle" @click="toChange" style="cursor: pointer" v-else>{{ note.title }}</p>

<button class="btn btnPrimary" @click="toChange">Change</button>

</template>

<script>

export default {
    data() {
    return {
        changeN: true,
    }
    },
    props: {
    note: {
      type: Object,
      required: true
    },
      index: {
      type: Number,
      required: true
      },
      notes: {
        type: Array,
        required: true
     },
    },
    methods: {
        toChange () {
            this.changeN = !this.changeN
            this.$emit('toChange', this.index)
        }
    }
  }



</script>

<style lang="scss">

</style>