<template>
  <div id="jokes-card">
    <h3>{{title}}</h3>
    <div v-for="joke in jokes" :key="joke.id">
      <p class="setup">{{joke.setup}}</p>
      <p class="punchline">{{joke.punchline}}</p>
    </div>
    <button class="btn" @click="getNJokes(1)">Get a Different Joke</button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Jokes",
  data() {
    return {
      title: "Random Dad Jokes",
      jokes: []
    };
  },
  methods: {
    getNJokes(n) {
      axios
        .get(
          `https://us-central1-dadsofunny.cloudfunctions.net/DadJokes/random/jokes/${n ||
            1}`,
          {
            headers: {
              Accept: "application/json"
            }
          }
        )
        .then(response => {
          console.log(response);
          this.jokes = response.data;
        })
        .catch(err => {
          alert(err);
        });
    }
  },
  created() {
    this.getNJokes();
  }
};
</script>

<style >
@import url("https://fonts.googleapis.com/css?family=Roboto:300,400,500&display=swap");
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  widows: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  flex-direction: column;
  font-family: "Roboto", sans-serif;
}

body {
  background-color: #fff3e0;
}

h3 {
  text-align: center;
  font-size: 2rem;
  margin-bottom: 20px;
}

#jokes-card {
  width: 600px;
  height: 300px;
  background-color: #fb8c00;
  border-radius: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  box-shadow: #212121 0 4px 8px -3px;
}

.setup {
  margin-bottom: 10px;
}

.punchline {
  margin-bottom: 20px;
}

p {
  font-size: 18px;
}

.btn {
  padding: 10px 15px;
  border-radius: 10px;
  outline: none;
  border: none;
  cursor: pointer;
  box-shadow: #212121 0 4px 8px -3px;
  background-color: #fff3e0;
}

.btn:active {
  background-color: black;
  color: #f4f4f4;
}
</style>