<template>
    <div class="ratingselect">
        <div class="rating-type border-1px">
            <span class="block positive"  :class="{'active':selectType===2}" @click="select(2,$event)">{{desc.all}} <span class="count">{{ratings.length}}</span> </span>
            <span class="block positive"  :class="{'active':selectType===0}" @click="select(0,$event)">{{desc.positive}}<span class="count" >{{positives.length}}</span></span>
            <span class="block negative" :class="{'active':selectType===1}" @click="select(1,$event)">{{desc.negative}}<span class="count">{{negatives.length}}</span></span>
        </div>
        <div class="switch" @click="switchContent">
            <span class="icon-check_circle" :class="{'on':onlyContent===true}"></span>
            <span class="text">只看有内容的评价</span>
        </div>
    </div>
</template>
<script>
const POSITIVE=0;
const NAGATIVE=1;
const ALL=2;
export default {
props:{
    ratings:{type:Array,default(){
        return [];
    }},
    selectType:{
       type:Number,
       default:ALL
    },
    onlyContent:{
        type:Boolean,
        default:true,
    },
    desc:{
        type:Object,
        default(){
            return {
                all:"全部",
                positive:'满意',
                negative:'不满意'
            }
        }
    }
} ,
methods: {
    select(type,event){
        if(!event._constructed){
            return ;
        }
        this.selectType=type;
        this.$dispatch('select',type)

    },
    switchContent(){
        if(!event._constructed){
            return ;
        }   
        this.onlyContent=!this.onlyContent;
        // console.log(this.onlyContent)
        this.$dispatch('switch',this.onlyContent)
    }
},
computed: {
    positives(){
        return this.ratings.filter((rating)=>{
            return rating.rateType==POSITIVE;
            // console.log(1)
        })
    },
    negatives(){
        return this.ratings.filter((rating)=>{
            return rating.rateType==NAGATIVE;
        })
    }
},
       
}
</script>
<style lang="stylus">
@import "../../common/stylus/mixin";
 .ratingselect
     .rating-type
       padding 18px 0
       margin 0 18px
       border-1px(rgba(7,17,27,0.1))
       font-size 0
       .block
           display inline-block
           padding 8px 12px
           margin-right 8px
           border-radius 2px
           color rgb(77,85,93)
           font-size 12px
           line-height 16px
           &.active
               color #fff
           .count
               margin-left 2px
               font-size 8px
               
           &.positive
               background rgba(0,160,220,0.2)
               &.active
                  background rgb(0,160,220)
           &.negative
               background rgba(77,85,93,0.2)
               &.active
                   background rgb(77,85,93)
     .switch
       padding 12px 18px
       line-height 24px
       border-bottom 1px solid rgba(7,17,27,0.1)
       color rgb(147,153,159)
       font-size 0px
       .icon-check_circle
          margin-right 4px
          font-size 24px
          display inline-block
          vertical-align top
          &.on
            color #00c850
       .text
          font-size 12px
          
            

            

</style>
