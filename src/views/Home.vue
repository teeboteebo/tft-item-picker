<template>
  <v-container class="home my-sm-2">
    <div class="text">
      <h1>
        <v-icon dark>mdi-sword</v-icon>Team Fight Tactics
        <v-icon dark>mdi-sword</v-icon>
      </h1>
      <h2>Item Picker</h2>
      <v-divider color="#eee"></v-divider>
      <p class="mt-4">Either combine 2 standard items to see what the make together or select an upgraded item to see what it's made from.</p>
    </div>
    <ItemPicker />
  </v-container>
</template>

<script>
// @ is an alias to /src
import ItemPicker from "../components/ItemPicker.vue";
export default {
  name: "Home",
  components: {
    ItemPicker
  }
};
</script>
<style lang="scss" scoped>
.home {
  background-color: rgba(0, 0, 0, 0.5);
  color: #eee;
  padding: 1rem;
  max-width: 800px;
  .text {
    // padding: 1rem;
    // border-radius: 2px;
    // background-color: rgba(0, 0, 0, 0.5);
    h1 {
      font-size: 1.5rem;
    }
    h2 {
      margin-bottom: 0;
    }
    p {
      margin: 0;
    }
  }
}
</style>
