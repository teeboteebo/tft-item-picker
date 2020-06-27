<template>
  <v-container class="home my-sm-2">
    <div class="text">
      <h1>
        <v-icon dark>mdi-sword</v-icon>Team Fight Tactics - Cheat Sheet
        <v-icon dark>mdi-sword</v-icon>
      </h1>
      <v-divider color="#eee"></v-divider>
      <p class="mt-4">Use this tool in order to find the desired item combination, by either:</p>
      <ul>
        <li>selecting two base items to see what they create together.</li>
        <li>select one upgraded item to see what two base items are combined for it.</li>
      </ul>
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
