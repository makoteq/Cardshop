<template>
  <div>
    <input
      class="input"
      type="text"
      placeholder="Search title.."
      name="search"
    />
    <loading v-show="loading" />
    <div class="container">
      <div v-for="item in info" :key="item.id" class="item">
        <div style=" text-align: center;" class="half">
          <img :src="item.img.url" width="50%" alt="" />
        </div>
        <div class="half">
          <span class="header">{{ item.title }}</span
          ><br />
          <span class="price">{{ item.price }}zł</span><br />
          <span class="qty"> Quantity:{{ item.qty }}</span>
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

import loading from "@/components/loading.vue";
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
  components: {
    loading
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
  margin: 0 auto;
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
.qty {
  font-size: 1em;
  font-weight: bold;
  color: #000000;
  text-align: right;
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
</style>
