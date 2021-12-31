<template>
  <div class="hello">
    <img alt="Vue logo" src="../assets/logo.png" />
    <h1>Jokes Bapack-Bapack Generator</h1>

    <button @click="showresult()">Generate Joke</button>
    <div v-if="result">
      <p>{{ result }}</p>
    </div>
    <div v-if="result2">
      <p>{{ result2 }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "HelloWorld",

  data() {
    return {
      result: "",
      result2: "",

      clicked: false,
    };
  },
  methods: {
    async showresult() {
      if (this.clicked) return;
      this.clicked = true;
      let config = {
        method: "GET",
        url: "https://dad-jokes.p.rapidapi.com/random/joke",
        headers: {
          "x-rapidapi-host": "dad-jokes.p.rapidapi.com",
          "x-rapidapi-key":
            "4293d06347mshbb87001f7ab55f9p11811bjsn7801b504908f",
        },
      };
      // axios
      //   // .request(config)
      //   .then(function () {
      //     console.log($result);
      //   })
      //   .catch(function (error) {
      //     console.error(error);
      //   });'

      const response = await axios.get(
        "https://dad-jokes.p.rapidapi.com/random/joke",
        config
      );
      console.log(response.data);
      this.result = response.data.body[0].setup;
      this.result2 = response.data.body[0].punchline;

      setTimeout(() => {
        this.clicked = false;
      }, 5000);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
p {
  color: black;
}
</style>
