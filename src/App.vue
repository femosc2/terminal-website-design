<template>
  <div id="app">
    <global-navigation @gNavClicked="setCurrentPage" />
    <router-view></router-view>
  </div>
</template>

<script>
import ProfessionalContainer from "./components/Professional/ProfessionalContainer"
import GlobalNavigation from "./components/GlobalNavigation/GlobalNavigation"

const axios = require("axios");

export default {
  name: "app",
  data: function() {
    return {
      ip: "",
      currentPage: "Personal"
    };
  },
  components: {
    ProfessionalContainer,
    GlobalNavigation
  },
  methods: {
    logIP() {
      // Log visitors to the site.
      let today = new Date();
      axios.get("https://api.ipify.org").then(response => {
        let resultArray = [];
        for (let key in response) {
          resultArray.push(response[key]);
        }
        this.ip = resultArray[0];
        let stringIp = this.ip.split(".");
        let firebaseIp = stringIp[0] + stringIp[1] + stringIp[2] + stringIp[3]; //Creates a address for Firebase (firebase cant process .)
        let firebaseInt = parseInt(firebaseIp, 10); // Convert the string to an Int as it wont work without it
        let loggedIp = { //Object which gets passed to the database
          ip: this.ip,
          time: today
        };
        setTimeout(() => {
          axios
            .put(
              "https://my-website-21d35.firebaseio.com/ipLog/" +
                firebaseInt +
                ".json",
              loggedIp
            )
            .then(response => {
              let postArray = [];
              for (let key in response) {
                postArray.push(response[key]);
              }
            });
        }, 2 * 1000);
      });
    },
    setCurrentPage(page) {
      this.currentPage = page
      console.log(page)
    }
  },
  created() {
    this.logIP();
  }
};
</script>

<style>
#app {
  font-family: "Quicksand", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding: 0;
  margin: 0 !important;
}

@keyframes blurIn {
  0% {
    filter: blur(15px);
  }
  100% {
    filter: blur(0px);
  }
}

@media only screen and (max-width: 1000px) {
  .projectCard {
    width: 100%;
    height: 20%;
  }
  h2 {
    font-size: 75px !important;
  }
}
</style>
