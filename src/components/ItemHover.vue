<template>
  <div fluid class="item-hover">
    <v-row dense>
      <v-col cols="3" class="img">
        <v-img :src="img"></v-img>
      </v-col>
      <v-col cols="8" offset="1">
        <h4>{{item.name}}</h4>
        <div>
          <div class="caption item-stat" v-for="(stat, i) in stats" :key="`stat_${i}`">
            <div class="mr-2" v-if="stat.type">
              <img
                :title="stat.type"
                :src="`/img/stats/${stat.type}.svg`"
                alt="Item Stat Image"
                width="10"
              />
              +{{stat.value}}
            </div>
          </div>
        </div>
      </v-col>
    </v-row>
    <v-divider color="#eee" class="my-2"></v-divider>
    <v-row dense class="item-text">
      <v-col>
        <p class="caption">{{item.text}}</p>
      </v-col>
    </v-row>
  </div>
</template>
<script>
import items from "../assets/items.json";
export default {
  props: {
    item: {
      type: Object,
      default: undefined
    }
  },
  computed: {
    stats() {
      try {
        const children = this.item.children.map(childId => {
          return items.find(item => item.id === childId);
        });
        const stats = children.map(child => {
          if (child.stats[0]) {
            return child.stats[0];
          } else {
            return { type: null, value: null };
          }
        });
        if(stats[0]){
          return stats
        } else return this.item.stats
      } catch (err) {
        return [];
      }
    },
    id() {
      if (this.item.id.toString().length < 2) {
        return "0" + this.item.id.toString();
      } else {
        return this.item.id;
      }
    },
    img() {
      return `/img/items/${this.id}.png`;
    }
  }
};
</script>
<style lang="scss" scoped>
.item-hover {
  text-align: left;
  padding: 1rem;
  width: 300px;
  background-image: url("/img/bg-hover.jpg");
  background-size: cover;
  border: 2px solid;
  border-top-color: #ffd700;
  border-left-color: #ceaf00;
  border-right-color: #947e00;
  border-bottom-color: #695a00;
  .item-text {
    p {
      margin-bottom: 0;
    }
  }
  .item-stat {
    display: inline-block;
  }
}
</style>