<template>
  <v-app>
    <v-app-bar app class="header" dark>
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="logo"
          contain
          src="/img/logo-hero.png"
          transition="scale-transition"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>
      <h2>TFT Item Picker</h2>
    </v-app-bar>

    <v-main>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",
  data: () => ({
    //
  })
};
</script>
<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  background: rgb(2, 0, 36);
  background: linear-gradient(
    140deg,
    rgba(2, 0, 36, 1) 0%,
    rgba(3, 3, 52, 1) 35%,
    rgba(46, 0, 61, 1) 100%
  );

  .header {
    background-color: #45005c;
    h2 {
      font-size: 1.5rem;
    }
    .logo {
      filter: brightness(5);
    }
  }
  main {
    background-image: url("/img/tft.jpg");
    background-size: cover;
    background-position: center;
  }
}
</style>