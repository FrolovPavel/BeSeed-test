<template>
  <svg xmlns="http://www.w3.org/2000/svg"
       :width="width"
       :height="height"
       :viewBox="`0 0 ${viewBox} ${viewBox}`"
  >
    <g :fill="iconColor">
      <component :is="`icon-${icon}`"/>
    </g>
  </svg>
</template>

<script>
import IconConfirmed from "@/components/Icons/IconConfirmed";
import IconVk from "@/components/Icons/IconVk";
import IconTooltip from "@/components/Icons/IconTooltip";
import IconSubscribers from "@/components/Icons/IconSubscribers";
import IconCoverageER from "@/components/Icons/IconCoverageER";
import IconReactionsER from "@/components/Icons/IconReactionsER";
import IconCoveragePost from "@/components/Icons/IconCoveragePost";
import IconCTR from "@/components/Icons/IconCTR";
import IconClose from "@/components/Icons/IconClose";

export default {
  name: "BaseIcon",
  components: {
    IconConfirmed,
    IconVk,
    IconTooltip,
    IconSubscribers,
    IconCoverageER,
    IconReactionsER,
    IconCoveragePost,
    IconCTR,
    IconClose
  },
  props: {
    icon: {
      type: String,
      default: 'box'
    },
    width: {
      type: [Number, String],
      default: 18
    },
    height: {
      type: [Number, String],
      default: 18
    },
    iconColor: {
      type: String,
      default: 'currentColor'
    },
    viewBox: {
      type: [Number, String],
      default: 32
    }
  }
}
</script>
