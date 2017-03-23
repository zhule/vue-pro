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
	      if (!this.detailWrapper) {
	        this.detailWrapper = new BScroll(this.$refs.detailWrapper, {
	          click: true
	        });
	      } else {
	        this.detailWrapper.refresh()
	      }
	    },
	    addCart(event) {
	      if (!event._constructed) {
	        return
	      }
	      this.$set(this.food, 'count', 1)
	      this.$root.eventHub.$emit('cart.add', event.target)
	    },
	
	},
	components: {
		cartcontrol
	}

}	

</script>

<style lang="scss" rel="stylesheet/scss">
.detailWrapper {
  position: fixed;
  left: 0;
  top: 0;
  bottom: 48px;
  width: 100%;
  background: white;
  transition: all 0.4s ease;
  &.move-enter-avtive,&.move-leave-active{
    transform: translate3d(0,0,0);
  }
  &.move-enter,&.move-leave-active{
    transform: translate3d(100%,0,0);
  }
}	
.foodDetail {
  .back {
    position: absolute;
    color: white;
    top: 12px;
    left: 6px;
    font-size: 20px;
    padding: 10px;
  }
  .info {
  	position: relative;
    box-sizing: border-box;
    width: 100%;
    padding: 18px;
	.title {
	      font-size:14px;
	      font-weight: 700;
	      color: rgb(7,17,27);
	      line-height: 14px;
	}
	.desc {
	      display: flex;
	      padding: 0;
	      padding-top: 8px;
	      font-size: 10px;
	      color: rgb(147,153,159);
	      line-height: 10px;
	      span:last-child {
	        padding-left: 12px;
		  }
	}
	.price {
	  display: flex;
	  padding-top: 18px;
	  font-size: 14px;
	  font-weight: 700;
	  color: rgb(240,20,20);
	  line-height: 24px;
	  .unit {
	    font-size: 10px;
	    font-weight: normal;
	  }
	  .oldPrice {
	    padding-left: 12px;
	    font-size: 10px;
	    font-weight: normal;
	    color: rgb(147,153,159);
	    line-height: 24px;
	  }
	}
	.shopCart {
	      position: absolute;
	      right: 18px;
	      bottom: 18px;
	      height: 24px;
	      text-align: center;
	      z-index: 2;
	      .text {
	        box-sizing: border-box;
	        height: 100%;
	        line-height: 24px;
	        color: white;
	        font-size: 10px;
	        padding: 0 12px;
	        border-radius: 12px;
	        background: rgb(0,160,220);
	        &.fade-enter-active, &.fade-leave-active{
	          transition: opacity .2s;
	        }
	        &.fade-enter, &.fade-leave-active{
	          opacity: 0;
	        }
	      }
	}
	.cartcontrol {
      position: absolute;
      right: 12px;
      bottom: 12px;
	}
  }

  
}

</style>