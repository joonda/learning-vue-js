<template>
    <h1>{{ appTitle }}</h1>
    <button @click="changeTitle">button</button>
</template>

<script>
    export default {
        props: ['appTitle'],
        methods: {
            changeTitle() {
                this.$emit('change')
            }
        }
    }
</script>

<style scoped>

</style>