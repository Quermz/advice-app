<template>
  <div class="container">
    <h4 class="adviceNumber">{{ `ADVICE #${response.id}` }}</h4>
    <p class="adviceContent">
      {{ `"${response.advice}"` }}
    </p>
    <div class="buttonContainer">
      <img src="./assets/pattern-divider-desktop.svg" class="divider" />
      <button
        v-on:click="apiResponse"
        :disabled="wait"
        :class="{ wait: wait, go: !wait }"
        class="test"
      >
        <h1 v-if="wait">!</h1>
        <img v-else src="./assets/icon-dice.svg" alt="" />
      </button>
    </div>
  </div>
</template>

<script>
  import axios from "axios";
  export default {
    name: "App",
    components: {},
    created() {
      this.apiResponse();
    },
    data() {
      return {
        response: "",
        wait: false,
      };
    },
    methods: {
      apiResponse: async function () {
        try {
          this.response = await axios({
            method: "get",
            url: "	https://api.adviceslip.com/advice",
          });
          this.response = this.response.data.slip;
          this.wait = true;
          setTimeout(() => {
            this.wait = false;
            console.log("test");
          }, 2000);
        } catch (e) {
          console.log(e);
        }
      },
    },
  };
</script>

<style>
  * {
    box-sizing: border-box;
    padding: 0px;
    font-family: "Manrope", sans-serif;
    font-size: 28px;
    margin: 0px;
  }
  body {
    overflow: hidden;
    margin: 0px;
  }
  #app {
    margin: 0px;
    height: 100vh;
    width: 100vw;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #202632;
    box-shadow: inset 0 0 100px RGBA(68, 69, 91, 0.05);
  }

  .container {
    width: 20rem;
    background-color: #313a49;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 1.25rem;
    border-radius: 0.5rem;
  }

  .adviceNumber {
    font-size: 0.5rem;
    letter-spacing: 0.05rem;
    margin-bottom: 1.25rem;
    color: hsl(150, 100%, 66%);
  }

  .adviceContent {
    text-align: center;
    margin-bottom: 1.25rem;
    overflow: hidden;
    color: hsl(193, 38%, 86%);
  }

  .buttonContainer {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .divider {
    padding-bottom: 1.25rem;
  }

  .test {
    margin: 0px;
    height: 2.5rem;
    width: 2.5rem;
    border-radius: 50%;
    position: absolute;
    transform: translate(0%, 1.75rem);
    border: 0px;
    background-color: hsl(150, 100%, 66%);
    transition: box-shadow 0.2s ease;
  }

  .wait {
    background-color: red;
  }
  .go:hover {
    cursor: pointer;
    box-shadow: 0px 0px 20px 2px hsl(150, 100%, 66%);
  }
</style>
