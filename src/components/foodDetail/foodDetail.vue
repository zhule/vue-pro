<template lang="html">
	<div class="detailWrapper" ref="detailWrapper" v-show="showDetail">
		<div class="foodDetail">
			<div class="back" @click="showToggle()">
			    <i class="icon-arrow_lift"></i>
			</div>
			<img :src="food.image" height="425" width="100%">
			<div class="info">
			  <div class="title">{{food.name}}</div>
	          <div class="desc">
	            <span>月售{{food.sellCount}}</span>
	            <span>好评率{{food.rating}}%</span>
	          </div>
	          <div class="price">
	            <span class="unit">￥</span>{{food.price}}
	            <span class="oldPrice" v-show="food.oldPrice">￥{{food.oldPrice}}</span>
	          </div>
	          <div class="shopCart">
	            <transition name="fade">
	              <div class="text" @click="addCart($event)" v-show="!food.count">加入购物车</div>
	            </transition>
	          </div>
	          <cartcontrol :food="food"></cartcontrol>
			</div>
		</div>
	</div>
</template>

<script>
import BScroll from 'better-scroll'
import cartcontrol from 'components/cartcontrol/cartcontrol'

export default {
	props: {
		food: Object
	},
	created() {

	},
	mounted() {
		// console.log(this.detailWrapper);
		// console.log(this.$refs.detailWrapper);
	},
	data() {
	  return {
	  	showDetail:false
	  }
	},
	methods: {
		showToggle () {
		   this.showDetail = !this.showDetail
		   if (this.showDetail) {
		      this.$nextTick(() => {
		         this._initScroll();
		      })
		   }
		},
		_initScroll() {
			console.log(this.detailWrapper);
	      if (!this.detailWrapper) {
	        this.detailWrapper = new BScroll(this.$refs.detailWrapper, {
	          click: true
	        });
	      } else {
	        this.detailWrapper.refresh()
	      }
	    }
	
	},
	components: {
		cartcontrol
	}

}	

</script>

<style lang="scss" rel="stylesheet/scss">
	

</style>