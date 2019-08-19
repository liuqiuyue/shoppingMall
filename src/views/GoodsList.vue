<template>
    <div>
  <Navheader></Navheader>
    <Bread>
    <span>Goods</span>
    </Bread>
      <div class="accessory-result-page accessory-page">
        <div class="container">
          <div class="filter-nav">
            <span class="sortby">Sort by:</span>
            <a href="javascript:void(0)" class="default cur">Default</a>
            <a href="javascript:void(0)" class="price">Price <svg class="icon icon-arrow-short"><use xlink:href="#icon-arrow-short"></use></svg></a>
            <a href="javascript:void(0)" class="filterby stopPop">Filter by</a>
          </div>
          <div class="accessory-result">
            <!-- filter -->
            <div class="filter stopPop" id="filter">
              <dl class="filter-price">
                <dt>Price:</dt>
                <dd><a href="javascript:void(0)" :class="{'cur':priceChecked==='all'}" @click="priceChecked='all'">All</a></dd>
                <dd v-for='(item,index) in priceFilter' :key='index' @click="priceChecked=index">
                  <a href="javascript:void(0)" :class="{'cur':priceChecked===index}">{{item.s}} - {{item.e}}</a>
                </dd>
              </dl>
            </div>

            <!-- search result accessories list -->
            <div class="accessory-list-wrap">
              <div class="accessory-list col-4">
                <ul>
                  <li v-for="(item,index) in goodsList" :key="index">
                    <div class="pic">
                      <a href="#"><img :src="'static/'+item.prodcutImg" alt=""></a>
                    </div>
                    <div class="main">
                      <div class="name">{{item.productName}}</div>
                      <div class="price">{{item.prodcutPrice}}</div>
                      <div class="btn-area">
                        <a href="javascript:;" class="btn btn--m">加入购物车</a>
                      </div>
                    </div>
                  </li>
                </ul>
              </div>
            </div>
          </div>
        </div>
      </div>
   <NavFooter></NavFooter>
    </div>
</template>
<script>
import Navheader from '@/components/Header'
import NavFooter from '@/components/Footer'

import Bread from '@/components/Bread'
import axios from 'axios';
    export default{
        components: {
          Navheader,
          NavFooter,
          Bread
        },
        data(){
            return {
                goodsList:[],
                priceFilter:[{s:0,e:100},{s:101,e:200},{s:201,e:300}],
                priceChecked:'all'
            }
        },
        mounted(){
            this.getGoods()
        },
        methods:{
          getGoods(){
            axios.get('/goods').then((res)=>{
              this.goodsList=res.data.result
            })
          }
        }
        
    }
</script>
