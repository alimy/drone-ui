<template>
  <div class="popup"
       :class="{ [`position-${position}`]: true, [`align-${align}`]: true, 'width-same': width === 'same' }"
       :style="style">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "Popup",
  props: {
    position: { type: String, required: true, validator: x => ["bottom"].includes(x) },
    align: { type: String, required: true, validator: x => ["center", "right", "both"].includes(x) },
    width: Number
  },
  computed: {
    style() {
      const result = {};

      if (this.position === "bottom") {
        if (this.align === "right") {
          result.width = `${this.width}px`;
        }

        if (this.align === "center") {
          result.marginLeft = `-${this.width / 2}px`;
        }
      }

      return result;
    }
  }
};
</script>

<style scoped lang="scss">
@import "../assets/styles/variables";

.popup {
  position: absolute;
  background: #fff;
  z-index: 1;
  border-radius: 3px;
  box-shadow: 0 2px 4px 0 $border-color;
  border: solid 1px #edeef1;
}

.popup.position-bottom {
  top: 100%;
  margin-top: 10px;
}

.popup.position-bottom.align-center {
  left: 50%;
}

.popup.position-bottom.align-right {
  right: 0;
}

.popup.position-bottom.align-both {
  right: 0;
  left: 0;
}
</style>

<style lang="scss">
@import "../assets/styles/variables";

.repo-link.hover-type-box-shadow:hover .repo-item {
  box-shadow: 0 4px 10px 0 rgba($color-text, 0.25);
}

.repo-link .repo-item h3 {
  color: $color-primary;
}

.repo-link .repo-item-inactive h3 {
  color: $color-text;
}
</style>
