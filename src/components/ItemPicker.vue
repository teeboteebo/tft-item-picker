<template>
  <div class="item-picker">
    <h4 class="text-left mt-5">Base Items</h4>
    <v-divider color="#eee"></v-divider>
    <v-row dense class="basic-items my-5">
      <v-col cols="2" sm="1" v-for="(item) in items.slice(0,9)" :key="item.name">
        <div @click="() => toggleBasicItem(item)">
          <Item
            :tooltip="true"
            :item="item"
            :selected="item === selected1 || item === selected2 ? true : false"
          />
        </div>
      </v-col>
    </v-row>
    <v-row dense class="combinations my-5">
      <v-col cols="2">
        <div v-if="selected1">
          <Item :item="selected1" />
          <p>{{selected1.name}}</p>
          <p v-if="selected1.desc">{{selected1.desc}}</p>
        </div>
        <div v-else>
          <Item :item="notSelected" />
          <p>...</p>
          <p v-if="result && result.desc">{{result.desc}}</p>
        </div>
      </v-col>
      <v-col cols="2" class="center-center">
        <v-icon size="36" color="#eee">mdi-plus</v-icon>
      </v-col>
      <v-col cols="2">
        <div v-if="selected2">
          <Item :item="selected2" />
          <p>{{selected2.name}}</p>
          <p v-if="selected2.desc">{{selected2.desc}}</p>
        </div>
        <div v-else>
          <Item :item="notSelected" />
          <p>...</p>
        </div>
      </v-col>
      <v-col class="center-center">
        <v-icon size="36" color="#eee">mdi-equal</v-icon>
      </v-col>
      <v-col cols="2">
        <div v-if="result">
          <Item :item="result" />
          <p>{{result.name}}</p>
        </div>
        <div v-else>
          <Item :item="notSelected" />
          <p>...</p>
        </div>
      </v-col>
    </v-row>
    <v-btn @click="clear" color="error" class="clear-btn">Clear Selections</v-btn>
    <h4 class="text-left mt-5">Upgraded Items</h4>
    <v-divider color="#eee"></v-divider>
    <v-row dense class="upgraded-items my-5">
      <v-col cols="2" sm="1" v-for="(item) in items.slice(9,-1)" :key="item.name">
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
export default {
  name: "ItemPicker",
  components: {
    Item,
    ItemUpgraded
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
  updated() {
    console.log(`
    ---------\n
    sel1: ${this.selected1}
    sel2: ${this.selected2}
    res: ${this.result}
    pos: ${JSON.stringify(this.possible)}
    ---------\n
    `);
  },
  methods: {
    clear() {
      console.log("CLEARRRR");

      this.selected1 = undefined;
      this.selected2 = undefined;
    },
    toggleBasicItem(item) {
      console.log(`CHECKING: ${item.name}`);

      if (this.selected1 === item && this.selected2 === item) {
        console.log("It's in both");
        return this.clear();
      }

      if (this.selected1 === item || this.selected2 === item) {
        console.log("It's in 1 or 2");

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
        console.log("not both");
        if (!this.selected1) {
          console.log(`Not 1, Selecting: ${item.name}`);

          this.selected1 = item;
        } else if (!this.selected2) {
          console.log(`Not 2, Selecting: ${item.name}`);
          this.selected2 = item;
        }
      }
    },
    toggleUpgradedItem(upgradedItem) {
      if (this.result === upgradedItem) {
        console.log("callin clear");

        return this.clear();
      }
      this.selected1 = items.find(item => item.id === upgradedItem.children[0]);
      this.selected2 = items.find(item => item.id === upgradedItem.children[1]);
    }
  },
  computed: {
    possible() {
      if (this.selected1 && !this.selected2) {
        return items.filter(upgrade =>
          upgrade.children.includes(this.selected1.id)
        );
      } else if (!this.selected1 && this.selected2) {
        return items.filter(upgrade =>
          upgrade.children.includes(this.selected2.id)
        );
      } else if (!this.selected1 && !this.selected2) {
        return [];
      } else if (this.selected1 && this.selected2) {
        return items
          .filter(upgrade => upgrade.children[0] === this.selected1.id)
          .filter(upgrade => upgrade.children[1] === this.selected2.id);
      }
    },
    result() {
      if (this.possible.length === 1) {
        console.log(this.possible[0]);
        return this.possible[0];
      } else undefined;
    }
  }
};
</script>
<style lang="scss" scoped>
.item-picker {
  text-align: center;
  .basic-items {
  }
  .combinations {
    background-color: rgba(0, 0, 0, 0.5);
    border: 5px solid;
    border-top-color: #ffd700;
    border-left-color: #ceaf00;
    border-right-color: #947e00;
    border-bottom-color: #695a00;
    // background-image: url('/img/border.png');
    // background-size: cover;
    color: #eee;
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