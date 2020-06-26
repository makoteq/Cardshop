<template>
  <div
    class="containerCart
  "
  >
    <div class="list">
      <b-list-group>
        <b-list-group-item
          v-for="item in info"
          :key="item.id"
          style="cursor:pointer"
          >1x {{ item.title
          }}<span style="color:#ffca19"> {{ item.price }}zł</span>
        </b-list-group-item>
      </b-list-group>
    </div>
    <div>
      <img
        @click="clearStortage"
        class="delete"
        src="../assets/trash.svg"
        alt=""
      />
      <img @click="send" class="send" src="../assets/mail.svg" alt="" />
    </div>
    <div class="fullprice">Price:{{ fullprice }}zł</div>
  </div>
</template>
<script>
export default {
  name: "Cart",
  data() {
    return {
      info: null,
      fullprice: 0
    };
  },
  methods: {
    clearStortage() {
      localStorage.clear();
      this.info = JSON.parse(localStorage.getItem("data"));
      this.fullprice = 0;
    },
    send() {
      window.open(
        "mailto:makoteq@gmail.com?subject=cardshop&body=Shopping cart content:"
      );
    }
  },
  mounted() {
    this.info = JSON.parse(localStorage.getItem("data"));
    console.log(this.info);
    if (this.info != null) {
      this.info.forEach(element => {
        this.fullprice = this.fullprice + element.price;
        let price = this.fullprice.toFixed(2);
        console.log(price);
        this.fullprice = parseFloat(price);
      });
    }
    console.log(this.info);
  }
};
</script>
<style lang="scss">
.containerCart {
  margin: 0 auto;
  height: 80vh;
  width: 60%;
  padding: 2vw;
  margin-top: 20vh;
  text-align: center;
  font-weight: bold;
}
.send {
  margin: 2vh;
  max-width: 50px;
  cursor: pointer;
  transition: all 0.2s ease-in-out;
  &:hover {
    transform: scale(1.2);
  }
}
.list {
  width: 100%;
  text-align: center;
}
.delete {
  margin: 2vh;
  transition: all 0.2s ease-in-out;
  max-width: 50px;
  cursor: pointer;
  &:hover {
    transform: scale(1.2);
  }
}
.fullprice {
  font-size: 2em;
}
</style>
