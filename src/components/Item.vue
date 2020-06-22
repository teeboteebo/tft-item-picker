<template>
  <div
    class="item"
    :class="(selected1 || selected2) && 'selected'"
    :style="tooltip && {cursor: 'pointer'}"
  >
    <v-tooltip
      transition="slide-y-transition"
      content-class="tooltip-custom"
      eager
      v-if="tooltip"
      :disabled="mobile"
      bottom
    >
      <template v-slot:activator="{ on, attrs }">
        <div class="img-wrap" v-bind="attrs" v-on="on">
          <div class="badges">
            <span v-if="selected1">1</span>
            <span v-if="selected2">2</span>
          </div>

          <v-img class="img" :src="img" />
        </div>
      </template>
      <ItemHover :item="item" />
    </v-tooltip>
    <v-img v-else class="img-big" :src="img" />
  </div>
</template>
<script>
import ItemHover from "./ItemHover";
export default {
  props: {
    item: {
      type: Object,
      default: {
        id: 0,
        name: "Select an item"
      }
    },
    selected1: {
      type: Boolean,
      default: false
    },
    selected2: {
      type: Boolean,
      default: false
    },
    tooltip: {
      type: Boolean,
      default: false
    }
  },
  components: {
    ItemHover
  },
  created() {},
  computed: {
    mobile() {
      try {
        document.createEvent("TouchEvent");
        return true;
      } catch (e) {
        return false;
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
$tooltip-background-color: black;
.item {
  border-radius: 3px;
  transition: 0.1s all;
  &.selected {
    transition: 0.1s all;
    padding: 2px;
    background-color: gold;
    box-shadow: 0 0 8px 2px gold;
    .img {
      opacity: 0.97;
    }
  }
  .img-wrap {
    position: relative;
    .badges {
      position: absolute;
      z-index: 1;
      bottom: calc(100% - 8px);
      width: 110%;
      text-align: left;
      span {
        text-align: center;
        font-weight: bold;
        box-shadow: 0 0 2px black;
        margin-right: 4px;
        font-size: 13px;
        background: linear-gradient(140deg, gold, #2e003d 100%);
        display: inline-block;
        width: 20px;
        height: 20px;
        border-radius: 40px;
      }
    }
  }
  .img-big {
    border: 1px solid rgba(255, 215, 0, 0.5);
  }
  p {
    margin-bottom: 0 !important;
  }
  .tooltip-custom {
    opacity: 1 !important;
    padding: 0;
  }
}
</style>