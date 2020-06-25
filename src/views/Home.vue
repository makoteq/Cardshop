<template>
  <div>
    <input
      class="input"
      type="text"
      placeholder="Search title.."
      name="search"
    />
    <div class="container">
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
            style="cursor:pointer;"
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
      api_url: process.env.VUE_APP_API_URL || "http://localhost:1337"
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
    axios.get(this.api_url).then(response => (this.info = response.data));
  }
};
</script>
<style lang="scss">
.container {
  margin: 0 auto;
  height: 80vh;
  width: 100%;
  padding: 2vw;
  float: left;
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
</style>
