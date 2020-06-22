<template>
  <div class="item-picker">
    <h4 class="text-left mt-5">Base Items</h4>
    <v-divider color="#eee"></v-divider>
    <v-row dense class="basic-items my-5">
      <v-col cols="2" sm="1" v-for="(item) in basicItems" :key="item.name">
        <div @click="() => toggleBasicItem(item)">
          <Item
            :tooltip="true"
            :item="item"
            :selected1="item === selected1 ? true : false"
            :selected2="item === selected2 ? true : false"
          />
        </div>
      </v-col>
    </v-row>
    <h4 class="text-left mt-5">Result</h4>
    <v-divider color="#eee"></v-divider>
    <v-row dense class="combinations my-5">
      <v-col v-if="result" cols="12">
        <ItemHover class="d-inline-block" :item="result" />
      </v-col>
      <v-col v-else class="center-center" cols="2" offset="5">
        <div>
          <Item :item="notSelected" />
          <p>...</p>
        </div>
      </v-col>
    </v-row>
    <v-btn @click="clear" color="error" class="clear-btn">Clear Selections</v-btn>
    <h4 class="text-left mt-5">Upgraded Items</h4>
    <v-divider color="#eee"></v-divider>
    <v-row dense class="upgraded-items my-5">
      <v-col cols="2" sm="1" v-for="(item) in upgradedItems" :key="item.name">
        <div @click="() => toggleUpgradedItem(item)">
          <ItemUpgraded
            :possible="possible.includes(item) ? true : false"
            :selected="result === item && true"
            :tooltip="true"
            :item="item"
          />
        </div>
      </v-col>
    </v-row>
  </div>
</template>
<script>
import items from "@/assets/items.json";
import Item from "../components/Item";
import ItemUpgraded from "../components/ItemUpgraded";
import ItemHover from "../components/ItemHover";
export default {
  name: "ItemPicker",
  components: {
    Item,
    ItemUpgraded,
    ItemHover
  },
  data() {
    return {
      items,
      selected1: undefined,
      selected2: undefined,
      notSelected: {
        id: 0,
        name: "Select an item"
      }
    };
  },
  methods: {
    clear() {
      this.selected1 = undefined;
      this.selected2 = undefined;
    },
    toggleBasicItem(item) {
      if (this.selected1 === item && this.selected2 === item) {
        return this.clear();
      }
      if (this.selected1 === item || this.selected2 === item) {
        if (this.selected1 === item) {
          if (this.selected1 && this.selected2) {
            return (this.selected1 = undefined);
          }
        } else if (this.selected2 === item) {
          if (this.selected1 && this.selected2) {
            return (this.selected2 = undefined);
          }
        }
      }
      if (this.selected1 !== item || this.selected2 !== item) {
        if (!this.selected1) {
          this.selected1 = item;
        } else if (!this.selected2) {
          this.selected2 = item;
        }
      }
    },
    toggleUpgradedItem(upgradedItem) {
      if (this.result === upgradedItem) {
        return this.clear();
      }
      this.selected1 = items.find(item => item.id === upgradedItem.children[0]);
      this.selected2 = items.find(item => item.id === upgradedItem.children[1]);
    }
  },
  computed: {
    basicItems() {
      return this.items.slice(0, 9);
    },
    upgradedItems() {
      return this.items.slice(9, -1);
    },
    possible() {
      if (this.selected1 && !this.selected2) {
        return this.items.filter(upgrade =>
          upgrade.children.includes(this.selected1.id)
        );
      } else if (!this.selected1 && this.selected2) {
        return this.items.filter(upgrade =>
          upgrade.children.includes(this.selected2.id)
        );
      } else if (!this.selected1 && !this.selected2) {
        return [];
      } else if (this.selected1 && this.selected2) {
        if (this.selected1 === this.selected2) {
          return this.items
            .filter(upgrade => upgrade.children[0] === this.selected1.id)
            .filter(upgrade => upgrade.children[1] === this.selected2.id);
        }
        return this.items
          .filter(
            upgrade =>
              upgrade.children[0] === this.selected1.id ||
              upgrade.children[1] === this.selected1.id
          )
          .filter(
            upgrade =>
              upgrade.children[1] === this.selected2.id ||
              upgrade.children[0] === this.selected2.id
          );
      }
    },
    result() {
      if (this.possible.length === 1) {
        return this.possible[0];
      } else undefined;
    }
  }
};
</script>
<style lang="scss" scoped>
.item-picker {
  text-align: center;

  .combinations {
    // background-color: rgba(0, 0, 0, 0.5);
    // border: 5px solid;
    // border-top-color: #ffd700;
    // border-left-color: #ceaf00;
    // border-right-color: #947e00;
    // border-bottom-color: #695a00;
    // background-image: url('/img/border.png');
    // background-size: cover;
    color: #eee;
    height: 240px;
    @media screen and (min-width: 800px) {
    }
    p {
      margin-bottom: 0;
    }
  }
  .center-center {
    display: flex;
    flex-direction: column;
    justify-content: space-around;
  }
}
</style>