<template>
  <div id="app">
    <Header 
      :currentScore='current_score' 
      :topScore='top_score' 
      :message='message'
    />

    <header class='header-jumbotron' @click='handleCardClick("hello")'>
      <h1>Click the icons to play!</h1>
      <p>This is a game of memorization.  The goal is to click all cards before clicking on one card twice.</p>
    </header>

    <GameBoard 
      :characters='characters' 
      @character-clicked='handleCardClick'
    />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Header from './components/Header';
import GameBoard from './components/GameBoard'

import characters from './assets/characters';

export default {
  name: 'app',

  components: {
    HelloWorld,
    Header,
    GameBoard
  },

  data: function() {
    return {
      current_score: 0,
      top_score: 0,
      max_score: characters.length,
      selected_characters: [],
      characters,
      message: 'Click on any image to begin!'
    }
  },

  methods: {
    handleCardClick: function(name) {
      console.log(name);

      let currentScore = this.current_score;
      let topScore = this.top_score;
      const gameBoard = document.getElementsByClassName('gameboard')[0];

      // get each gamepiece and remove 'shake' animation class
      const allCards = Array.from(document.getElementsByClassName('gamepiece'))
      allCards.forEach(card => card.classList.remove('shake'));

      gameBoard.classList.remove('win-game'); // remove game winning CSS styling

      // shuffle cards for the next round
      this.shuffle();

      // check if that character was already selected
      const found = this.selected_characters.filter(c => c === name).length;

      // add shake animation if they clicked a card that was already selected
      if (found) {
        this.current_score = 0;
        this.selected_characters = [];

        allCards.forEach(card => card.classList.add('shake'));

        return;
      }

      // add one to the score since they guessed correctly
      currentScore++;

      currentScore > topScore ? this.top_score = currentScore : null;

      this.selected_characters = this.selected_characters.concat(name);
      this.current_score = currentScore;

      if (currentScore === this.max_score) {
        gameBoard.classList.add('win-game');
      }

    },

    shuffle: function() {
      let array = this.characters.map(c => {
        return {
          name: c.name
        }
      });

      console.log(array);
      let currentIndex = array.length,
        temporaryValue, randomIndex;

      // While there remain elements to shuffle...
      while (0 !== currentIndex) {

        // Pick a remaining element...
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex -= 1;

        // And swap it with the current element.
        temporaryValue = array[currentIndex];
        array[currentIndex] = array[randomIndex];
        array[randomIndex] = temporaryValue;
      }

      this.characters = array.slice();
    }
  }
}
</script>

<style>
body {
  margin: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #282c34;
  min-height: 100vh;
  /* margin-top: 100px; */

}

#app {
  height: 100%;
}

.header-jumbotron {
  /* background-color: #282c34; */
  background-image: url(./assets/images/plexus_abstract_1080.png);
  background-size: cover;

  padding-top: 125px;
  padding-bottom: 50px;
  /* min-height: 100vh; */
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  /* font-size: calc(10px + 2vmin); */
  font-size: 1.5em;
  color: white;
}

.header-jumbotron p {
  width: 50%;
}


.win-game {
  animation: win-game 1s ease;
}


@keyframes win-game {
  0%    { border: none; }
  50%   { border: 5px solid green; }
  100%  { border: none; }
}

.shake {
  animation: shake .5s 0.125s;
}

@keyframes shake {
  0% { transform: translate(5px, 0px); }
  10% { transform: translate(-10px, 0px); }
  25% { transform: translate(10px, 0px); }
  40% { transform: translate(-10px, 0px); }
  55% { transform: translate(10px, 0px); }
  70% { transform: translate(-10px, 0px); }
  85% { transform: translate(10px, 0px); }
  100% { transform: translate(-5px, 0px); }
}
</style>
