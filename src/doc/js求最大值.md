
//Math.max()

### 求一个数字数组中的最大值
  #### 方法1
     var array = [1,3,5,7,9]
     //首先数组Array的原型链上是没有max方法的 但是我们可以借用Math对象的max方法
     let r = Math.max.apply(null,array)
     console.log(r) //9
  #### 方法2
     var arr = [1,3,5,7,9]
     let res = arr.sort(function(a,b){
       //return a-b 正序排列
        return b-a //倒序排列   
      })
      console.log(res[0]) //倒序排列后 数组的第一个为最大值
  ### 方法3
     常规循环
    
### 求一个对象数组中的对象某个属性的最大值
  #### 方法1
    var list = [
         {
           score:99
         },
         {
           score:88
         },
         {
           score:85
         },
    ]
    let l = Math.max.apply(null,list.map(item=>{
          return item.score
       }))
       console.log(l)

  #### 方法2
     var list = [
         {
           score:99
         },
         {
           score:88
         },
         {
           score:85
         },
    ]
    let l = list.sort(function(a,b){
        return b.score - a.score  
      })
      console.log(l[0].score)
 #### 方法3
   常规循环

#### 求一个对象中属性的最大值
   var obj = {
         lessons:{
           js:100,
           php:90,
           jaav:64,
           net:65  
         }
       }
   #### 方法1
      let res = Math.max.apply(null,Object.values(obj.lessons))
      console.log(res)
   #### 方法2
      function max(arr){
         return arr.sort((a,b)=>{
           return b-a  
         })  
       }
       let r = max(Object.values(obj.lessons))[0]
       console.log(r)
   #### 方法3
      function getMax(obj){
         let max = 0
         let o = Object.values(obj)
         for(var i=0;i<o.length;i++){
           if(o[i]>max) {
             max = o[i] 
           }
         }
         return max 
       }
       console.log(getMax(obj.lessons))
  