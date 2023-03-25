<template>
  <div class="container-gallery">
    <div class="cont-header">
      <p>Galería de memes</p>
      <p class="sub-header">Encuentra tus memes y comparte</p>
      <!-- <label>
        <input type="text" v-model="search">
    <button @click="ok">Search</button>
        </label> -->
    </div>
    <div class="grid-container">
      <div class="item" v-for="meme in memes" :key="meme.id">
        <h4 class="name">{{ meme.name }}</h4>
        <img :src="meme.url" alt="meme"  class="img" />
        <div class="actions">
         <button><img src="../assets/compartir.png"/></button>
          <label class="toggle-label">
            <input type="checkbox" />
            <span class="back">
              <span class="toggle"></span>
              <span class="icon label on"> 👍 </span>
              <span class="icon label off">👎</span>
            </span>
          </label>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
  return {
    memes: [],
    search: '',
    searchResults: [],
  };
},
methods: {
  ok() {
    axios.get('https://api.imgflip.com/search_memes', { params: { q: this.search } })
      .then(response => {
        this.searchResults = response.data.result;
      })
      .catch(error => {
        console.error(error);
      });
  },
},
mounted() {
  axios
    .get(`https://api.imgflip.com/get_memes?q=${this.search.toLowerCase()}`)
    .then((response) => {
      this.memes = response.data.data.memes;
      console.log(this.memes);
    })
    .catch((error) => {
      console.error(error);
    });
},

  computed: {},
};
</script>

<style>
.container-gallery {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background: #a196e5;
  background: -webkit-linear-gradient(top left, #a196e5, #bbff92);
  background: -moz-linear-gradient(top left, #a196e5, #bbff92);
  background: linear-gradient(to bottom right, #a196e5, #bbff92);
}
.cont-header {
  font-family: "Pacifico", cursive;
  font-size: 4rem;
}
.sub-header {
  font-size: 2rem;
  font-family: "Dosis", sans-serif;
}
.name{
  font-family: "Dosis", sans-serif;
}
.grid-container {
  width: 80%;
  column-gap: 16px;
  margin: 8px 16px;
}
.actions{
  display: flex;
  align-items: center;
  width: 100%;
  box-sizing: border-box;
  /* border: 2px solid red; */
}
button{
  margin-top: 1rem;
  margin-left: 1rem;
  width: 30px;
  border: none;
  background-color: transparent;
}
button img{
  width: 100%;
}
.img {
  width: 100%;
}
@media only screen and (max-width: 480px) {
  .grid-container {
    column-count: 1;
  }
}
@media only screen and (min-width: 481px) and (max-width: 620px) {
  .grid-container {
    column-count: 2;
  }
}
@media only screen and (min-width: 621px) and (max-width: 1023px) {
  .grid-container {
    column-count: 3;
  }
}
@media only screen and (min-width: 1024px) {
  .grid-container {
    column-count: 4;
  }
}
.grid-container .item {
  box-sizing: border-box;
  background: rgba(255, 255, 255, 0.45);
  -webkit-backdrop-filter: blur(4px);
  backdrop-filter: blur(4px);
  border-radius: 10px;
  margin: 8px 0;
  padding: 1rem;
  display: inline-flex;
  flex-direction: column;
  align-items: center;
}
.icon {
  display: flex;
  align-items: flex-start !important;
  
}

.toggle-label {
  position: relative;
  display: block;
  width: 100px;
  height: 50px;
  margin-top: 1rem;
}
.toggle-label input[type="checkbox"] {
  opacity: 0;
  position: absolute;
  width: 100%;
  height: 100%;
}
.toggle-label input[type="checkbox"] + .back {
  position: absolute;
  width: 100%;
  height: 100%;
  margin-left: 2rem;
  background: transparent;
  transition: background 50ms linear;

}
.toggle-label input[type="checkbox"]:checked + .back {
  background: transparent; /*green*/
}

.toggle-label input[type="checkbox"] + .back .toggle {
  box-sizing: border-box;
  display: block;
  position: absolute;
  content: " ";
  background: #e9e9e9;
  width: 40%;
  height: 80%;
  transition: margin 150ms linear;
  border: 1px solid transparent;
  border-radius: 0;
}
.toggle-label input[type="checkbox"]:checked + .back .toggle {
  margin-left: 50px;
}
.toggle-label .label {
  display: block;
  position: absolute;
  width: 40%;
  color: #ddd;
  text-align: center;
  font-size: 1.2rem;
}
.toggle-label .label.on {
  left: 0px;
}
.toggle-label .label.off {
  right: 0.8rem;
}

.toggle-label input[type="checkbox"]:checked + .back .label.on {
  color: #fff;
}
.toggle-label input[type="checkbox"] + .back .label.off {
  color: #fff;
}
.toggle-label input[type="checkbox"]:checked + .back .label.off {
  color: #ddd;
}
</style>
