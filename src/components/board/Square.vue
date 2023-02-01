<template>
    <div class="square" @click="handle_square_click">
        <div class="internal">
            {{ get_symbol_for(val) }}
        </div>
    </div>
</template>
<script>
export default {
    props: ['val', 'x', 'y'],
    methods: {
        get_symbol_for(n) {
            switch (n) {
                case 1: return 'X';
                case 2: return 'O';
                default: return '';
            }
        },
        handle_square_click() {
            this.$emit('moveChosen', { x: this.x, y: this.y })
        }
    },
    name: 'Square'
}
</script>
<style scoped>
.square {
    width: 60px;
    height: 60px;
    background-color: #edc09f;
    color: red;
    display:flex;
}
.internal{
width:fit-content;
height:fit-content;
margin:auto;
font-size: larger;
}
</style>