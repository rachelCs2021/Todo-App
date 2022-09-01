<template>
    <button v-show="!showAddTodo" @click="onClick" class="btn">{{text}}</button>
</template>

<script>
export default {
   name: "ButtonTodo",
    props: {
        text: String,
        color: String,
        showAddTodo: Boolean
    },
   methods: {
       onClick() {
           this.$emit('btn-click')
       }
   }
}
</script>

<style scoped>
   .btn {
       padding: 7px 14px;
       border-radius: 5px;
       background: var(--light);
       color: #fff;
       background-color: rgb(205, 50, 200);
       border-color: #ffffff;
       font-weight: 700;
       font-size: 15px;
   }
</style>