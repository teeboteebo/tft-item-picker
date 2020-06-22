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
      <h2 class="font-weight-light text-h6 text-md-h5">Teebo's Item Picker</h2>
    </v-app-bar>
    <v-main>
      <router-view></router-view>
    </v-main>
    <v-footer>
      <v-container class="footer">
        <v-row>
          <v-col>
            <p>This site aims to help out newer players to TFT, <a href="https://euw.leagueoflegends.com/en/featured/events/teamfight-tactics"  rel="noreferrer" target="_blank">Team Fight Tactics</a>. All the different available items can be confusing to keep track of and this is a simple tool to play around with.</p>
            <p>With this TFT item combiner, you can select either two base items to see what they upgrade to. Or you can select the upgraded item that you want to see what combination of base items are used for it.</p>
            <p>
              If you want to reach out to me for a bug report or anything else, you can do that by contacting me via
              <a href="https://twitter.com/teebo__" rel="noreferrer" target="_blank">Twitter</a>. The site will be updated when time's available.
            </p>
            <p>// Teebo</p>
          </v-col>
        </v-row>
      </v-container>
    </v-footer>
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
    background: rgb(2, 0, 36);
    background: linear-gradient(
      140deg,
      rgba(2, 0, 36, 1) 0%,
      rgba(3, 3, 52, 1) 35%,
      rgba(46, 0, 61, 1) 100%
    );
    @media screen and (min-width:800px){
      padding: 0 calc((100vw - 832px) / 2)
    }
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
  footer {
    background: rgb(2, 0, 36);
    background: linear-gradient(
      140deg,
      rgba(2, 0, 36, 1) 0%,
      rgba(3, 3, 52, 1) 35%,
      rgba(46, 0, 61, 1) 100%
    );
    .footer {
      max-width: 800px;
      margin: 0 auto;
      color: #eee;
      font-size: 0.8rem;
    }
  }
}
</style>