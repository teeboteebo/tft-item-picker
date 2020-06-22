<template>
  <div class="item" :class="selected && 'selected'" :style="tooltip && {cursor: 'pointer'}">
    <v-tooltip transition="slide-y-transition" content-class="tooltip-custom" eager v-if="tooltip" :disabled="mobile" bottom>
      <template v-slot:activator="{ on, attrs }">
        <v-img class="img" :src="img" v-bind="attrs" v-on="on" />
      </template>
      <ItemHover :item="item" />
    </v-tooltip>
    <v-img v-else class="img-big" :src="img" />
  </div>
</template>
<script>
import ItemHover from './ItemHover'
export default {
  props: {
    item: {
      type: Object,
      default: {
        id: 0,
        name: "Select an item"
      }
    },
    selected: {
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
  overflow: hidden;
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