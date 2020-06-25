<template>
  <footer>
    <div class="copyright">
      <span class="copy">© 2020 makoteq</span>
    </div>
    <div @click="mail" class="more">
      <span class="morein">Contact</span>
    </div>
  </footer>
</template>

<script>
export default {
  name: "footerbar",
  methods: {
    mail() {
      window.open("mailto:makoteq@gmail.com");
    }
  }
};
</script>

<style lang="scss" scoped>
footer {
  width: 90%;
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 10vh;
  border-top: solid 1px rgb(194, 194, 194);

  .morein {
    cursor: pointer;
    text-align: right;
    color: black;
    &:hover {
      text-decoration: underline;
    }
  }
  .copyright {
    width: 60%;
    color: rgb(54, 106, 167);
    text-align: left;
  }
  .more {
    width: 20%;
    text-align: center;
  }
  a {
    text-decoration: none;
  }
}
</style>
