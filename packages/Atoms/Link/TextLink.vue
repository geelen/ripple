<template>
  <rpl-link class="rpl-text-link" :class="{ 'rpl-text-link--underline': underline }" :href="url" :innerWrap="innerWrap">
    <rpl-text-label :theme="theme" :size="size" :underline="underline" :emphasis="emphasis">
      <rpl-text-icon :text="text" :symbol="iconSymbolFinal" :color="iconColor" :placement="iconPlacement" :size="iconSize" />
    </rpl-text-label>
  </rpl-link>
</template>

<script>
import {RplTextIcon} from '@dpc-sdp/ripple-icon'
import RplLink from './Link.vue'
import RplTextLabel from './TextLabel.vue'
import { isExternalUrl } from '@dpc-sdp/ripple-global/utils/helpers.js'

export default {
  name: 'RplTextLink',
  props: {
    iconSymbol: {default: null, type: String},
    iconColor: {default: 'primary', type: String},
    iconPlacement: {default: 'after', type: String},
    iconSize: {default: 'm', type: String},
    text: {default: null, type: String},
    url: {default: null, type: String},
    innerWrap: {default: true, type: Boolean},
    underline: {default: false, type: Boolean},
    theme: {default: 'light', type: String},
    size: {default: null, type: String},
    emphasis: {default: false, type: Boolean}
  },
  components: {
    RplTextIcon,
    RplLink,
    RplTextLabel
  },
  computed: {
    iconSymbolFinal () {
      if (isExternalUrl(this.url, this.rplOptions.hostname)) {
        return 'external_link'
      }
      return this.iconSymbol
    }
  }
}
</script>

<style lang="scss">
  @import "~@dpc-sdp/ripple-global/scss/settings";
  @import "~@dpc-sdp/ripple-global/scss/tools";

  $rpl-text-link-light-underline-hover: rpl-color('mid_neutral_2') !default;
  $rpl-text-link-dark-underline-hover: rpl-color('white') !default;
  $rpl-text-link-text-color-hover: rpl_color('primary') !default;
  $rpl-text-link-dark-text-color-hover: rpl-color('white') !default;

  .rpl-text-link {
    &--underline {
      &.rpl-link {
        &:hover,
        &:focus {
          text-decoration: none;
        }
      }
    }

    &:hover,
    &:focus {
      color: $rpl-text-link-text-color-hover;

      .rpl-text-label {
        color: $rpl-text-link-text-color-hover;

        &--small {
          &--underline {
            border-bottom-color: $rpl-text-link-light-underline-hover;
          }
        }

        &--large {
          &--underline {
            border-bottom-color: $rpl-text-link-light-underline-hover;
          }
        }

        &--dark {
          &--underline {
            color: $rpl-text-link-dark-text-color-hover;
            border-bottom-color: $rpl-text-link-dark-underline-hover;
          }
        }
      }
    }
  }
</style>
