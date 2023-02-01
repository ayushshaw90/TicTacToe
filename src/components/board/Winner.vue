<template>

    <div v-if="winner !== 0">
        Winner is {{ winner=== 1 ? 'X' : 'O' }}
    </div>

</template>

<script>
export default {
    props: ['winner'],
    name: 'Winner'
}
</script>
<style scoped>
div {
    padding: 4px 6px;
    background-color: violet;
    font-size: larger;
    width:300px;
}
</style>