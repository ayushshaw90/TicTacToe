<template>
    <div class="board">
        <Square v-for="sq in board" :key="sq.x * 3 + sq.y" @moveChosen="handle_move" :x="sq.x" :y="sq.y" :val="sq.val">
        </Square>
    </div>
    <div>
        <Winner :winner="winner"></Winner>
    </div>
    <button @click="new_game" class="newgame">New game</button>
</template>



<style>
.board {
    display: grid;
    grid-template-columns: auto auto auto;
    gap: 4px;
    padding: 4px;
    background-color: #86b0e4;
    width: fit-content;
}
.newgame{
    background-color: rgb(45, 140, 178);
    border: 0px;
    color:white;
    padding: 8px 12px;
    font-size: larger;
    border-radius: 12px;
}
</style>

<script>
import Square from './Square.vue';
import Winner from './Winner.vue';

export default {
    data() {
        return {
            board: [
                { val: 0, x: 0, y: 0 }, { val: 0, x: 1, y: 0 }, { val: 0, x: 2, y: 0 },
                { val: 0, x: 0, y: 1 }, { val: 0, x: 1, y: 1 }, { val: 0, x: 2, y: 1 },
                { val: 0, x: 0, y: 2 }, { val: 0, x: 1, y: 2 }, { val: 0, x: 2, y: 2 }
            ],
            game_on: true,
            next_move: 1,
            winner: 0
        }
    },
    components: {
        Square,
        Winner
    },
    name: 'Board',
    methods: {
        handle_move(dat) {
            if (!this.game_on) {
                return;
            }
            if(this.board[dat.x+3*dat.y].val!==0){
                return;
            }
            const bbrd = this.board.map(e => {
                if (dat.x == e.x && dat.y == e.y) {
                    return { val: this.next_move, x: dat.x, y: dat.y }
                } else {
                    return e;
                }
            })
            this.board = bbrd;
            this.next_move = (this.next_move == 1) ? 2 : 1;
            //finding winner
            this.find_winner(bbrd)
        },
        find_winner(dat) {
            for (let i = 0; i < 3; i++) {
                if (dat[i * 3].val === dat[i * 3 + 1].val && dat[i * 3 + 2].val === dat[i * 3 + 1].val && dat[i * 3].val !== 0) {
                    this.game_on = false;
                    this.winner = dat[i * 3].val;
                    return;
                }
                if (dat[i].val === dat[i + 3].val && dat[i + 3].val === dat[i + 6].val && dat[i].val !== 0) {
                    this.game_on = false;
                    this.winner = dat[i].val;
                    return;
                }
            }
            if (dat[0].val === dat[4].val && dat[4].val === dat[8].val && dat[0].val !== 0) {
                this.game_on = false;
                this.winner = dat[0].val;
                return;
            }
            if (dat[2].val === dat[4].val && dat[4].val === dat[6].val && dat[2].val !== 0) {
                this.game_on = false;
                this.winner = dat[2].val;
                return;
            }
        },
        new_game(){
            this.board=[
                { val: 0, x: 0, y: 0 }, { val: 0, x: 1, y: 0 }, { val: 0, x: 2, y: 0 },
                { val: 0, x: 0, y: 1 }, { val: 0, x: 1, y: 1 }, { val: 0, x: 2, y: 1 },
                { val: 0, x: 0, y: 2 }, { val: 0, x: 1, y: 2 }, { val: 0, x: 2, y: 2 }
            ];
            this.game_on=true;
            this.next_move=1;
            this.winner=0;
        }
    }
}
</script>