 <template>
 
  <div class="slider" >
    <p>您需要通过以下验证</p>
    <div class="sliderBox" >
      <div class="progress" :style="'width:'+left+'px'"></div>
      <span class="sliderSpn"  :style="'left:'+left+'px'" @mousedown="getX">
        <i :class="sliderInner" :style="'color:'+sliderColor+';background-color:'+bgColor"></i></span>
        <span :style="'color:'+color" class="tips">{{tip}}</span>
      
        <transition>
            <div class="blink" v-if="binkFlag">
                </div>
        </transition>
         

      

       
    </div>
  </div>
</template>
<script>
function goBack(start,obj,prop){
 
  var step=-10
  
var timer=  setInterval(() => {
    
    start+=step
    obj[prop]=start
   
   if(start<=0){
    obj[prop]=0
    clearInterval(timer)
   }
  }, 80);
}
export default {
  data(){
    return {
     left:0,
     X:0, 
     parentWidth:260,
     childWidth:40,
     tip:'请按住滑块，拖到最右边',
     color:'',
     sliderInner:'el-icon-d-arrow-right',
     sliderColor:'',
     bgColor:'',
     binkFlag:true,
     
    
     
    }
  },
  created(){
   var timeid=setInterval(()=>{
     
     this.binkFlag=!this.binkFlag
     if(this.left==this.parentWidth-this.childWidth){
       clearInterval(timeid)
       this.binkFlag=false
     }
   },2000)
  },
  methods:{
    
    getX(e){
      if(this.left!=this.parentWidth-this.childWidth){
         this.X=e.clientX     
      }
     
     
      
    },
    move(e){
  
   
      if(this.X!==0){
        
          this.left=e.clientX-this.X
         if(this.left<0){
           this.left=0
         }else if(this.left>=this.parentWidth-this.childWidth){
           this.left=this.parentWidth-this.childWidth
           this.X=0
           this.tip='验证通过'
           this.color='#fff'
           this.sliderInner='el-icon-check'
           this.sliderColor='#fff'
           this.bgColor='#7ac23c'
           this.binkFlag=false
           
         }
      }
     
    },
    up(){
    
     if(this.left<this.parentWidth-this.childWidth && this.left!==0){
      
      goBack(this.left,this,'left')
      
     }else if(this.left==0){

     }else{
       this.left=this.parentWidth-this.childWidth
       
     }
    this.X=0;

      
     
    },
    
    
  },
  mounted(){

      document.onmousemove=this.move
      document.onmouseup=this.up
      
 
   
  
  }
  
  
  
}
</script>
<style lang="scss" scoped>
.slider{
  width: 300px;
  height: 120px;
  background-color:#fff;

  p{
    padding: 20px;
    margin: 0;
  }
 
  .sliderBox{
   width: 260px;
   height: 32px;
   background-color: #e8e8e8;
   margin: 0 20px;
   position: relative;
   font-size: 12px;
    line-height: 32px;

    .tips{
      position: absolute;
      left:0;
      width: 100%;
      text-align: center;

      z-index: 2
    }

    .progress{
     position: absolute;
     left:0;
     background:#7ac23c;
     height:100%;
     z-index: 1
    
    }

   .sliderSpn{
     position: absolute;
     width: 40px;
     height: 32px;
     background-color: #fff;
     left:0;
     border:1px solid #e8e8e8;
     color: #e8e8e8;
     text-align: center;
     line-height: 32px;
     font-size: 18px;
     cursor: move;
     z-index: 3
   
     

   }
   .blink{
     width: 15px;
    height: 15px;
    background-color: #e8e8e8;
    position: absolute;
     left:45px;
     top:8px;
     z-index: 3;
   }

   .v-enter{
     opacity: 0;
      
   }
   .v-enter-active{
     animation: blink 1s linear  ;
   }
   

  }

  
}

 

  @keyframes blink {
    0%{
      transform: translateX(0)
    }
    100%{
      transform: translateX(150px)
    }
  }

[class*=" el-icon-"], [class^=el-icon-]{
  border-radius: 50%
}
</style>