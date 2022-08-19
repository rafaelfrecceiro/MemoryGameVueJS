<template>
  <div class="container">
    <div class="title">
      <h1>Memory Game</h1>
    </div>
    <div class="board">
      <div class="tile" v-for="(tile, index) in tiles" :key="index" @click="clickTile(tile, $event)">
        <img src=""/>
      </div>
    </div>
  </div>
</template>

<script>
import {shuffle} from 'lodash'

export default {
  data() {
    return {
      tiles: [
        {key: 1, name:'Charizard', imageShow:'', image: 'charizard.png'},
        {key: 1, name:'Charizard', imageShow:'', image: 'charizard.png'},
        {key: 2, name:'Bulbasaur', imageShow:'', image: 'bulbasaur.png'},
        {key: 2, name:'Bulbasaur', imageShow:'', image: 'bulbasaur.png'},
        {key: 3, name:'Caterpie', imageShow:'', image: 'caterpie.png'},
        {key: 3, name:'Caterpie', imageShow:'', image: 'caterpie.png'},
        {key: 4, name:'Charmander', imageShow:'', image: 'charmander.png'},
        {key: 4, name:'Charmander', imageShow:'', image: 'charmander.png'},
        {key: 5, name:'Koffing', imageShow:'', image: 'koffing.png'},
        {key: 5, name:'Koffing', imageShow:'', image: 'koffing.png'},
        {key: 0, name:'Pokeball', imageShow:'', image: 'pokeball.png'},
        {key: 6, name:'Machamp', imageShow:'', image: 'machamp.png'},
        {key: 6, name:'Machamp', imageShow:'', image: 'machamp.png'},
        {key: 7, name:'Metapod', imageShow:'', image: 'metapod.png'},
        {key: 7, name:'Metapod', imageShow:'', image: 'metapod.png'},
        {key: 8, name:'Mew', imageShow:'', image: 'mew.png'},
        {key: 8, name:'Mew', imageShow:'', image: 'mew.png'},
        {key: 9, name:'Mewtwo', imageShow:'', image: 'mewtwo.png'},
        {key: 9, name:'Mewtwo', imageShow:'', image: 'mewtwo.png'},
        {key: 10, name:'Onix', imageShow:'', image: 'onix.png'},
        {key: 10, name:'Onix', imageShow:'', image: 'onix.png'},
        {key: 11, name:'Raichu', imageShow:'', image: 'raichu.png'},
        {key: 11, name:'Raichu', imageShow:'', image: 'raichu.png'},
        {key: 12, name:'Pikachu', imageShow:'', image: 'pikachu.png'},
        {key: 12, name:'Pikachu', imageShow:'', image: 'pikachu.png'}
      ],
      attempt: 0,
      lastClicked: undefined
    }
  },
  created() {
    this.tiles = shuffle(this.tiles)
  },
  methods: {
    renderImageTile(image) {
      if(image == "") return false
      return require("./assets/set1/" + image)
    },
    cleanBoard(){
      this.tiles.forEach(tile => {
        tile.imageShow = ''
      })

      let tiles = document.getElementsByClassName('tile')
      for (let i = 0; i < tiles.length; i++) {
        tiles[i].classList.remove('tile-clicked')
        tiles[i].children[0].src = ""
      }
    },
    clickTile(tile, event){
      let elImg = event.target.children[0]
      let elDiv = event.target
      tile.imageShow = tile.image
      elImg.src = this.renderImageTile(tile.imageShow)
      elDiv.classList.add("tile-clicked")

      this.attempt++

      if(this.attempt == 1) {
        this.lastClicked = tile.name
        return
      }

      setTimeout(() => {
        if(this.attempt == 2) {
          if(this.lastClicked === tile.name) {
            alert("ACERTOU")
          }else{
            this.attempt = 0
          }
        }
      }, 100)

      setTimeout(() =>{
        this.cleanBoard()
      },1100)

    }
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Silkscreen&display=swap');

.container {
  display: flex;
  justify-content: center;
  align-content: center;
  padding-top: 1rem;
  flex-wrap: wrap;
}

.title {
  font-family: 'Silkscreen', cursive;
  font-size: 1.5rem;
  width: 100%;
  display: flex;
  justify-content: center;
  align-content: center;
  padding-bottom: 1rem;
}

.board {
  width: 750px;
  height: 750px;
  background-color: #171717;
  display: flex;
  flex-wrap: wrap;
  align-content: flex-start;
  border-radius: 10px;
}

.tile {
  width: 150px;
  height: 150px;
  border-radius: 10px;
  border: 2px solid #bc4949;
  background-color: #ce6060;
  display: flex;
  justify-content: center;
  align-content: center;
}

.tile:hover {
  background-color: #ef8f8f;
  cursor: pointer;
}

.tile-clicked{
  background-color: #8c3e3e;
}
</style>
