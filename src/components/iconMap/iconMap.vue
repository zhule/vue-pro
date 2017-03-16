<template lang="html">
	<span class="iconMap" :class="iconClassMap[iconType]"></span>
</template>

<script>
export default {
	props: {
		iconType: Number
	},
	created () {
		this.iconClassMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
	}
}

</script>

<style lang="scss" scoped>
@import '../../common/scss/mixin';
.iconMap {
	display: inline-block;
    background-size: 100% 100%;
    background-repeat: no-repeat;
    width: 12px;
    height: 12px;
    &.decrease {
      @include bg-image('decrease_4');
    }
    &.discount {
      @include bg-image('discount_4');
    }
    &.guarantee {
      @include bg-image('guarantee_4');
    }
    &.invoice {
      @include bg-image('invoice_4');
    }
    &.special {
      @include bg-image('special_4');
    }
}

</style>