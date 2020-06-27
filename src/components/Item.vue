<template>
  <div
    class="item"
    :class="(selected1 || selected2) && 'selected'"
    :style="tooltip && {cursor: 'pointer'}"
  >
    <div class="img-wrap">
      <div class="badges">
        <span v-if="selected1">1</span>
        <span v-if="selected2">2</span>
      </div>

      <v-img class="img" :src="img" />
    </div>
    <ItemHover v-if="!mobile" class="hover" :item="item" />
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
  background-color: #050613;
  position: relative;
  border-radius: 3px;
  transition: 0.1s all;
  &.selected {
    .img-wrap {
       transition: 0.1s all;
      opacity: 0.97;
      padding: 2px;
      box-shadow: 0 0 8px 2px gold;
      background-color: gold;
    }
  }
  .hover {
    display: none;
    z-index: 10;
  }
  &:hover {
    .img-wrap {
      transition: 0.1s all;
      opacity: 0.97;
      padding: 2px;
      
      box-shadow: 0 0 8px 2px gold;
      background-color: gold;
    }
    .hover {
      position: absolute;
      display: block;
      bottom: calc(100% + 16px);
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
  p {
    margin-bottom: 0 !important;
  }
}
</style>