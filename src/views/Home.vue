<template>
  <div>
    <input
      class="input"
      type="text"
      placeholder="Search title.."
      name="search"
    />

    <div v-show="loading" class="sk-circle">
      <div class="sk-circle1 sk-child"></div>
      <div class="sk-circle2 sk-child"></div>
      <div class="sk-circle3 sk-child"></div>
      <div class="sk-circle4 sk-child"></div>
      <div class="sk-circle5 sk-child"></div>
      <div class="sk-circle6 sk-child"></div>
      <div class="sk-circle7 sk-child"></div>
      <div class="sk-circle8 sk-child"></div>
      <div class="sk-circle9 sk-child"></div>
      <div class="sk-circle10 sk-child"></div>
      <div class="sk-circle11 sk-child"></div>
      <div class="sk-circle12 sk-child"></div>
    </div>
    <div class="containerIn">
      <div v-for="item in info" :key="item.id" class="item">
        <div style=" text-align: center;" class="half">
          <img :src="item.img.url" width="50%" alt="" />
        </div>
        <div class="half">
          <span class="header">{{ item.title }}</span
          ><br />
          <span class="price">{{ item.price }}zł</span>
          <br />
          <img
            @click="add(item.id, item.title, item.price)"
            class="addtocart"
            src="../assets/shopping-cart.svg"
            width="40"
            alt=""
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from "axios";
export default {
  name: "Home",
  data() {
    return {
      info: null,
      api_url: process.env.VUE_APP_API_URL || "http://localhost:1337",
      loading: true
    };
  },
  methods: {
    add(id, title, price) {
      //push article to cart
      let data = [];
      if (JSON.parse(localStorage.getItem("data"))) {
        data = JSON.parse(localStorage.getItem("data"));
      }
      let index;
      if (data[0] == undefined) {
        index = 0;
      } else {
        index = data[data.length - 1].id;
      }
      data.push({ id: index + 1, title: title, price: price });
      localStorage.setItem("data", JSON.stringify(data));
    }
  },
  mounted() {
    axios
      .get(this.api_url)
      .then(response => (this.info = response.data))
      .catch(error => console.log(error))
      .finally(() => (this.loading = false));
  }
};
</script>
<style lang="scss">
.container {
  width: 100vw;
  min-height: 90vh;
}
.containerIn {
  margin: 0 auto;
  width: 90%;
  padding: 2vw;

  text-align: center;
  margin: 0 auto;
}
.header {
  font-size: 120%;
  font-weight: bold;
  font-family: Helvetica;
}
.price {
  font-size: 1.4em;
  font-weight: bold;
  color: rgb(45, 45, 189);
  text-align: left;
}
.item {
  max-width: 500px;
  text-align: left;
  min-height: 200px;
  margin: 0 auto;
}
.half {
  min-height: 100%;
  width: 50%;
  float: left;
}
.input {
  background-color: #f3f3f3;
  border: none;
  line-height: 1.5;
  font-weight: 600;
  padding: 10px;
  border-radius: 5px;
  margin: 20px;
  max-width: 80vw;
  min-width: 50vw;
  transition: all 0.4s;
  &:focus {
    outline: 0;
  }
}
.addtocart {
  cursor: pointer;
  transition: all 0.1s ease-in-out;
  width: 50px;
  border-radius: 15px;
  padding: 5px;
  &:active {
    transform: scale(1.2);
    background-color: #ffca19;
  }
}
.sk-circle {
  margin: 100px auto;
  width: 40px;
  height: 40px;
  position: relative;
}
.sk-circle .sk-child {
  width: 100%;
  height: 100%;
  position: absolute;
  left: 0;
  top: 0;
}
.sk-circle .sk-child:before {
  content: "";
  display: block;
  margin: 0 auto;
  width: 15%;
  height: 15%;
  background-color: #ffca19;
  border-radius: 100%;
  -webkit-animation: sk-circleBounceDelay 1.2s infinite ease-in-out both;
  animation: sk-circleBounceDelay 1.2s infinite ease-in-out both;
}
.sk-circle .sk-circle2 {
  -webkit-transform: rotate(30deg);
  -ms-transform: rotate(30deg);
  transform: rotate(30deg);
}
.sk-circle .sk-circle3 {
  -webkit-transform: rotate(60deg);
  -ms-transform: rotate(60deg);
  transform: rotate(60deg);
}
.sk-circle .sk-circle4 {
  -webkit-transform: rotate(90deg);
  -ms-transform: rotate(90deg);
  transform: rotate(90deg);
}
.sk-circle .sk-circle5 {
  -webkit-transform: rotate(120deg);
  -ms-transform: rotate(120deg);
  transform: rotate(120deg);
}
.sk-circle .sk-circle6 {
  -webkit-transform: rotate(150deg);
  -ms-transform: rotate(150deg);
  transform: rotate(150deg);
}
.sk-circle .sk-circle7 {
  -webkit-transform: rotate(180deg);
  -ms-transform: rotate(180deg);
  transform: rotate(180deg);
}
.sk-circle .sk-circle8 {
  -webkit-transform: rotate(210deg);
  -ms-transform: rotate(210deg);
  transform: rotate(210deg);
}
.sk-circle .sk-circle9 {
  -webkit-transform: rotate(240deg);
  -ms-transform: rotate(240deg);
  transform: rotate(240deg);
}
.sk-circle .sk-circle10 {
  -webkit-transform: rotate(270deg);
  -ms-transform: rotate(270deg);
  transform: rotate(270deg);
}
.sk-circle .sk-circle11 {
  -webkit-transform: rotate(300deg);
  -ms-transform: rotate(300deg);
  transform: rotate(300deg);
}
.sk-circle .sk-circle12 {
  -webkit-transform: rotate(330deg);
  -ms-transform: rotate(330deg);
  transform: rotate(330deg);
}
.sk-circle .sk-circle2:before {
  -webkit-animation-delay: -1.1s;
  animation-delay: -1.1s;
}
.sk-circle .sk-circle3:before {
  -webkit-animation-delay: -1s;
  animation-delay: -1s;
}
.sk-circle .sk-circle4:before {
  -webkit-animation-delay: -0.9s;
  animation-delay: -0.9s;
}
.sk-circle .sk-circle5:before {
  -webkit-animation-delay: -0.8s;
  animation-delay: -0.8s;
}
.sk-circle .sk-circle6:before {
  -webkit-animation-delay: -0.7s;
  animation-delay: -0.7s;
}
.sk-circle .sk-circle7:before {
  -webkit-animation-delay: -0.6s;
  animation-delay: -0.6s;
}
.sk-circle .sk-circle8:before {
  -webkit-animation-delay: -0.5s;
  animation-delay: -0.5s;
}
.sk-circle .sk-circle9:before {
  -webkit-animation-delay: -0.4s;
  animation-delay: -0.4s;
}
.sk-circle .sk-circle10:before {
  -webkit-animation-delay: -0.3s;
  animation-delay: -0.3s;
}
.sk-circle .sk-circle11:before {
  -webkit-animation-delay: -0.2s;
  animation-delay: -0.2s;
}
.sk-circle .sk-circle12:before {
  -webkit-animation-delay: -0.1s;
  animation-delay: -0.1s;
}

@-webkit-keyframes sk-circleBounceDelay {
  0%,
  80%,
  100% {
    -webkit-transform: scale(0);
    transform: scale(0);
  }
  40% {
    -webkit-transform: scale(1);
    transform: scale(1);
  }
}

@keyframes sk-circleBounceDelay {
  0%,
  80%,
  100% {
    -webkit-transform: scale(0);
    transform: scale(0);
  }
  40% {
    -webkit-transform: scale(1);
    transform: scale(1);
  }
}
</style>
