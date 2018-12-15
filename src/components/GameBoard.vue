<template>
    <div class="gameboard">
        <GamePiece 
            v-for='c in characters'
            :key='c.name'
            :character='c'
            v-on:character-clicked="$emit('character-clicked', $event)"         
        />
    </div>
</template>


<script>
import GamePiece from './GamePiece';

export default {
    name: 'GameBoard',

    components: {
        GamePiece
    },

    props: {
        characters: Array
    },

    data: () => {
        return {

        }
    },
    
    methods: {
        clicked: () => {
            console.log('clicked')
        }
    }
}
</script>


<style scoped>
.gameboard {
    display: flex;
    min-height: 50vh;
    flex-wrap: wrap;
    justify-content: center;
    align-content: space-around;
    /* width: 90%; */
    max-width: 1100px;
    margin: 0 auto;
    margin-top: 50px;

    padding: 0 100px 100px 100px;
}


</style>
