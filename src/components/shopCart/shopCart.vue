<template lang="html">
 <div class="shopCart">
 	<div class="content">
 		<div class="content-left" @click="">
 			<div class="logo-wrapper">
 				<div class="badge"></div>
 				<div class="logo">
 				   <i class="icon-shopping_cart"></i>
 				</div>
 			</div>
 			<div class="price" :class=""></div>
 			<div class="desc">
 				<!-- 另需要配送费￥{{}}元 -->
 			</div>
 		</div>
 		<div class="content-right"></div>
 	</div>
 </div>
</template>

<script>
export default {
  props: {
  	deliveryPrice: {
  	  type: Number,
  	  default: 0
  	}
  }
}	

</script>

<style lang="scss" rel="stylesheet/scss">
.shopCart {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  height: 48px;
  z-index: 50;
  .content {
  	display: flex;
  	background: #141d27;
  	.content-left {
  		flex: 1;
  		height: 48px;
  	    .logo-wrapper {
	        display: inline-block;
	        vertical-align: top;
	        position: relative;
	        height: 56px;
	        line-height: 56px;
	        border-radius: 50%;
	        width: 56px;
	        top: -10px;
	        background: #000;
	        margin:0 12px;
	        padding: 6px;
	        box-sizing: border-box;
	        text-align: center;
	        .badge {
	          position: absolute;
	          top: 0;
	          right: 0;
	          background: rgb(240,20,20);
	          color: white;
	          width: 24px;
	          height: 16px;
	          line-height: 16px;
	          font-size: 9px;
	          box-shadow: 0px 4px 8px 0px rgba(0,0,0,0.4);
	          font-weight: 700;
	          border-radius: 16px;
	          text-align: center;
	       }
		   .logo {
		      width: 100%;
		      height: 100%;
		      background: #2b343c;
		      border-radius: 50%;
		      font-size: 24px;
		      color: #80858a;
		      line-height: 44px;
		      font-weight: 700;
		      &.active {
		        background: rgb(0,160,220);
		        color: white;
		      }
		   }
        }
        .price {
	        display: inline-block;
	        vertical-align: top;
	        font-size: 16px;
	        margin-top: 12px;
	        padding-right: 12px;
	        box-sizing: border-box;
	        color: rgba(255,255,255,0.4);
	        font-weight: 700;
	        line-height: 24px;
	        border-right: 1px solid rgba(255,255,255,0.1);
	        &.active {
	          color: white;
	        }
        }
	    .desc {
		   position: relative;
		   display: inline-block;
		   vertical-align: top;
		   margin: 12px 0 0 12px;
		   font-size: 10px;
		   color: rgba(255,255,255,0.4);
		   font-weight: 700;
		   line-height: 24px;
	    }
  	 } // left end
  	 
	.content-right { //right start
	  flex: 0 0 105px;
      font-size: 12px;
      font-weight: 700;
      background: #2b343c;
      color: rgba(255,255,255,0.4);
      line-height: 48px;
      text-align: center;
	  &.enough {
        background: #00b43c;
        color: white;
	  }
	} //right end
  }

  .ball-container {
	 .ball {
	 	 position: fixed;
	     left: 32px;
	     bottom: 22px;
	     z-index: 200;
	     &.drop-enter,&.drop-enter-active {
	     	transition: all 0.4s cubic-bezier(0.49,-0.29,0.75,0.41);
	     	.inner {
	          width: 16px;
	          height: 16px;
	          border-radius: 50%;
	          background: rgb(0,160,220);
	          transition: all 0.4s linear;
	        }
	     }
	 }
  }

  .shopcart-list {
  	position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    background: white;
    transform: translate3d(0,-100%,0);
    z-index: -1;
    &.transHeight-enter-active,&.transHeight-leave-active {
      transition: all 0.5s;
    }
    &.transHeight-enter,&.transHeight-leave-active {
      transform: translate3d(0,0,0);
    }
    .list-header {
      height: 40px;
      line-height: 40px;
      background: #f3f5f7;
      border-bottom: 1px solid rgba(7,17,27,0.1);
      .title {
        display: inline-block;
        font-size: 14px;
        font-weight: 200;
        color: rgb(7,17,27);
        padding-left: 18px;
      }
      .empty {
        position: absolute;
        right: 8px;
        font-size: 12px;
        color: rgb(0,160,220);
        padding: 0 10px;
      }
    }
    .list-content {
      max-height: 217px;
      overflow: hidden;
	    .food {
	        position: relative;
	        display: flex;
	        height: 48px;
	        margin: 0 18px;
	        border-bottom: 1px solid rgba(7,17,27,0.1);
	        .name {
		       flex: 1;
		       font-size: 14px;
		       color: rgb(7,17,27);
		       line-height: 48px;
		       font-weight: 700;
	         }
	        .price {
	          font-size: 14px;
	          font-weight: 700;
	          color: rgb(240,20,20);
	          padding: 0 12px 0 18px;
	          line-height: 48px;
	         }
	        .cartcontrol-wrapper {
	          font-size: 14px;
	          margin-top: 6px;
	        }
        }

    }
  }

}	
.backdrop {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background: rgba(7,17,27,0.6);
  backdrop-filter: blur(10px);
  z-index: 40;
  &.fade-backdrop-enter-active,&.fade-backdrop-leave-active {
    transition: opacity 0.5s;
  }
  &.fade-backdrop-enter,&.fade-backdrop-leave-active {
    opacity: 0;
  }
}
</style>