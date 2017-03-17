<template lang="html">
  <!--goods start-->
  <div class="goods">
  	<div class="menu-wrapper" ref="menuWrapper">
  		<ul>
  			<li v-for="(item, index) in goods" @click="menuClick(index, $event)" :class="index = menuCurrentIndex ? 'menu-item-selected' : 'menu-item'">
  				<span class="text">
  					<iconMap v-show="item.type > 0" :iconType="item.type"></iconMap>
  					{{item.name}}
  				</span>
  			</li>
  		</ul>
  	</div>
  	<!--goods end--> 
  	<!-- foods-wrapper start-->
  	<div class="foods-wrapper" id="wrapper" ref="foodsWrapper">
		<ul>
			<li v-for="item in goods" class="food-list food-list-hook">
			    <h1>{{item.name}}</h1>
				<ul>
					<li v-for="food in item.foods" class="food-item" @click="goDetail(food);">
						<div class="icon">
							<img width="57" height="57" :src="food.icon" />
						</div>
						<div class="content">
							<h2>{{food.name}}</h2>
							<p class="description" v-show="food.description">{{food.description}}</p>
							<div class="sell-info">
								<span class="sellCount">月售: {{food.sellCount}}份</span>
								<span class="rating">好评率{{food.rating}}%</span>
							</div>
							<div class="price">
								<span class="newPrice"><span class="unit">￥</span>{{food.price}}</span>
							    <span class="oldPrice" v-show="food.oldPrice">￥{{food.oldPrice}}</span>
							</div>
							<div class="cartcontrol-wrapper">
								<cartcontrol :food="food"></cartcontrol>
							</div>
						</div>
					</li>
				</ul>
	  	    </li>
		</ul>
  	</div>
  	<!-- foods-wrapper end-->
   <shopCart :deliveryPrice="seller.deliveryPrice" :minPrice = "seller.minPrice" :selectFoods="selectFoods"></shopCart>
  </div>
</template>

<script>
import axios from 'axios'
import Vue from 'vue'
import iconMap from 'components/iconMap/iconMap'
import cartcontrol from 'components/cartcontrol/cartcontrol'
import shopCart from 'components/shopCart/shopCart'

export default {
	props: {
		seller: Object
	},
	created () {
	    axios.get('static/data.json').then((res) => {
	      this.goods = res.data.goods;
	      //this.$nextTick(() => {
	        //this._initScroll(); // 初始化scroll
	        //this._calculateHeight(); // 初始化列表高度列表
	      //})
	    });
	},
	data() {
	   return {
	      goods: [],
	      listHeight: [],
	      foodsScrollY: 0,
	      selectedFood: ''
	   }
    },
    computed: {
       menuCurrentIndex() {
	      for (let i = 0, l = this.listHeight.length; i < l; i++) {
	        let topHeight = this.listHeight[i]
	        let bottomHeight = this.listHeight[i + 1]
	        if (!bottomHeight || (this.foodsScrollY >= topHeight && this.foodsScrollY < bottomHeight)) {
	          return i
	        }
	      }
	      return 0
	   },
    },
	methods: {
	   menuClick(index, event) {
	      if (!event._constructed) {
	        return
	      }
	      this.foodsScroll.scrollTo(0, -this.listHeight[index], 300)
	   }
	},
	components: {
    	iconMap,
    	cartcontrol,
    	shopCart
	}

}
</script>

<style lang="scss" rel="stylesheet/scss">
@import '../../common/scss/mixin';
  .goods { 
    display: flex;
    position: absolute;
    top: 174px;
    bottom: 46px;
    width: 100%;
    overflow: hidden;
    .menu-wrapper {
      flex: 0 0 80px;
      width: 80px;
      background: #f3f5f7;
      margin-top: 2px;
      .menu-item-selected {
        background: white;
        font-weight: 700;
        margin-top: -1px;
      }
      .menu-item,.menu-item-selected {
        position: relative;
        display: table;
        height: 54px;
        line-height: 14px;
        width: 56px;
        padding: 0 12px;
        &:last-child:after {
          content: none;
        }
       }
      .menu-item:after {
          position: absolute;
          content: '';
          left: 12px;
          width: 56px;
          bottom: 0;
          border-bottom: 1px solid rgba(7,17,27,0.1);
      }
      .text {
          display: table-cell;
          vertical-align: middle;
          font-size: 12px;
          font-weight: 200;
          white-space: normal;
          line-height: 14px;
          .iconMap {
            vertical-align: middle;
          }
  	  }
   }

   .foods-wrapper {
      flex: 1;
      margin-top: 2px;
      .food-list {
        h1 {
          height: 26px;
          line-height: 26px;
          padding-left: 12px;
          font-size: 12px;
          color: rgb(147,153,159);
          background: #f3f5f7;
          border-left: 2px solid #d9dde1;
       }
      }
      .food-item {
        position: relative;
        display: flex;
        margin: 0 18px;
        padding: 18px 0;
        border-bottom: 1px solid rgba(7,17,27,0.1);
        .icon {
          flex: 0 0 57px;
        }
        &:last-child {
          border-bottom: none;
        }
        .content {
          flex: 1;
          padding-left: 10px;
          h2 {
            margin: 2px 0 8px 0;
            font-size: 14px;
            line-height: 14px;
            height: 14px;
            font-weight: 700;
            color: rgb(7,17,27);
           }
          .sell-info,.description {
            font-size: 10px;
            color: rgb(147,153,159);
            line-height: 10px;
            .sellCount {
              margin-right: 4px;
            }
          }
          .description {
            font-size: 10px;
            margin-bottom: 8px;
            line-height: 12px;
           }
          .price {
            font-size: 10px;
            font-weight: 700;
            line-height: 24px;
            .newPrice {
              font-size: 14px;
              color: rgb(240,20,20);
              .unit {
                font-size: 10px;
                font-weight: normal;
              }
             }
            .oldPrice {
              text-decoration: line-through;
              color: rgb(147,153,159);
              padding-left: 4px;
            }
          }
          .cartcontrol-wrapper {
            position: absolute;
            right: 0;
            bottom: 12px;
            z-index: 20;
		  }
		}
	  }
   }         
}
</style>