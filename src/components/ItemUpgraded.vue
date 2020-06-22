<template>
  <div
    class="item"
    :class="possible && 'possible' || selected && 'selected'"
    :style="tooltip && {cursor: 'pointer'}"
  >
    <div class="img-wrap">
      <v-img class="img" :src="img" />
    </div>
    <ItemHover v-if="!mobile" class="hover" :item="item" />
  </div>
</template>
<script>
import ItemHover from "./ItemHover";
export default {
  components: {
    ItemHover
  },
  props: {
    item: {
      type: Object,
      default: {
        id: 0,
        name: "Select an item"
      }
    },
    tooltip: {
      type: Boolean,
      default: false
    },
    selected: {
      type: Boolean,
      default: false
    },
    possible: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      test: true
    };
  },

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
.item {
  position: relative;
  border-radius: 3px;
  transition: 0.1s all;
  &.possible {
    transition: 0.1s all;
    padding: 2px;
    background-color: gold;
    box-shadow: 0 0 8px 2px gold;

    .img-wrap {
      transition: 0.1s all;
      opacity: 0.97;
      padding: 2px;
      background-color: #00aeff;
      box-shadow: 0 0 8px 2px #00aeff;
    }
  }
  .hover {
    display: none;
    z-index: 10;
  }
  &:hover {
    .hover {
      position: absolute;
      display: block;
      bottom: calc(100% + 16px);
    }
  }
  p {
    margin-bottom: 0 !important;
  }
}
</style>