<template>
  <nav>
    <router-link to="/">
      <div>
        <img
          src="../assets/energy.svg"
          class="energy"
          width="120"
          alt=""
        /></div
    ></router-link>
    <router-link to="/cart"
      ><img src="../assets/shopping-cart.svg" class="cart" width="50" alt=""
    /></router-link>
  </nav>
</template>

<script>
export default {
  name: "navbar"
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
nav {
  min-height: 10vh;
  width: 100%;
  margin-bottom: 5vh;
}
img {
  cursor: pointer;
  margin: 20px;
  transition: all 0.2s ease-in-out;
  &:hover {
    transform: scale(1.2);
  }
}
.energy {
  float: left;
  border-radius: 15px;
  padding: 10px;

  &:hover {
    background-color: #ffca19;
  }
}
.cart {
  float: right;
}
.search {
  float: right;
}
</style>
