
<script lang="ts">
import Vue, { VNode } from 'vue'

export default Vue.extend({
  props: {
    type: {
      type: String,
      default: 'horizontal'
    },
    dashed: {
      type: Boolean,
      default: false
    }
  },
  render(h: any): VNode {
    const { type, dashed } = this
    return h(
      'div',
      {
        class: {
          divider: true,
          [`divider-${type}`]: true,
          'divider-dashed': !!dashed
        },
        props: this.$attrs
      },
      [
        this.$slots.default &&
          h(
            'span',
            {
              class: 'divider-inner-text'
            },
            this.$slots.default
          )
      ]
    )
  }
})
</script>

<style lang="scss">
@import '~theme/theme.scss';

.divider {
  font-family: $font-family;
  font-size: $font-size-base;
  line-height: $line-height-base;
  color: $text-color;
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  list-style: none;

  background: $border-color-split;

  &,  // for compatiable
  &-vertical {
    margin: 0 8px;
    display: inline-block;
    height: 0.9em;
    width: 1px;
    vertical-align: middle;
    position: relative;
    top: -0.06em;
  }
  &-horizontal {
    display: block;
    height: 1px;
    width: 100%;
    margin: 24px 0;
  }
  &-horizontal &-with-text {
    display: table;
    white-space: nowrap;
    text-align: center;
    background: transparent;
    font-weight: 500;
    color: $heading-color;
    font-size: $font-size-lg;
    margin: 16px 0;

    &:before,
    &:after {
      content: '';
      display: table-cell;
      position: relative;
      top: 50%;
      width: 50%;
      border-top: 1px solid $border-color-split;
      transform: translateY(50%);
    }
  }
  &-inner-text {
    display: inline-block;
    padding: 0 24px;
  }
  &-horizontal &-with-text-left {
    display: table;
    white-space: nowrap;
    text-align: center;
    background: transparent;
    font-weight: 500;
    color: $heading-color;
    font-size: $font-size-base;
    margin: 16px 0;

    &:before {
      content: '';
      display: table-cell;
      position: relative;
      top: 50%;
      width: 5%;
      border-top: 1px solid $border-color-split;
      transform: translateY(50%);
    }
    &:after {
      content: '';
      display: table-cell;
      position: relative;
      top: 50%;
      width: 95%;
      border-top: 1px solid $border-color-split;
      transform: translateY(50%);
    }
    &-inner-text {
      display: inline-block;
      padding: 0 10px;
    }
  }

  &-horizontal &-with-text-right {
    display: table;
    white-space: nowrap;
    text-align: center;
    background: transparent;
    font-weight: 500;
    color: $heading-color;
    font-size: $font-size-base;
    margin: 16px 0;

    &:before {
      content: '';
      display: table-cell;
      position: relative;
      top: 50%;
      width: 95%;
      border-top: 1px solid $border-color-split;
      transform: translateY(50%);
    }
    &:after {
      content: '';
      display: table-cell;
      position: relative;
      top: 50%;
      width: 5%;
      border-top: 1px solid $border-color-split;
      transform: translateY(50%);
    }
    &-inner-text {
      display: inline-block;
      padding: 0 10px;
    }
  }
  &-dashed {
    background: none;
    border-top: 1px dashed $border-color-split;
  }
  &-horizontal &-with-text &-dashed {
    border-top: 0;
    &:before,
    &:after {
      border-style: dashed none none;
    }
  }
}
</style>
