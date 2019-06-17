<template>
  <div class="hello">
    <!-- <button v-on:click="getdata">点击</button>
    <div v-for="t in info" v-bind:key="t.id">
      <p>{{ t.id }}</p>
    </div> -->
    <!-- <img src="../assets/bg2.jpg" alt=""> -->
    <div id="maskLayer" class="maskLayer" @click="closeDiv()">
      <div class="detail">
        <span>Name:</span>
        <p id="author"></p>
        <span>Message:</span>
        <p id="message"></p>
        <span id="TO">To:</span>
        <p id="to"></p>
        <span>Date:</span>
        <p id="date"></p>
      </div>
    </div>
    <!-- 整体部分 -->
    <div id="box">
      <!-- 展示留言部分 -->
      <div class="liuyan" >
        <div class="circle" @click="showDiv(t.id)"  v-for="t in info" v-bind:key="t.id">
          <p :id="'author'+t.id">{{t.author}}</p>
          <p :id="'message'+t.id">{{t.message}}</p>
          <p :id="'receiver'+t.id" style="display: none">{{t.receiver}}</p>
          <p :id="'date'+t.id" style="display: none">{{t.created_at}}</p>
        </div>
      </div>
      <!-- 点击换页 -->
      <div class="change">
        <a href="#" @click="getdata()">戳一戳</a>
      </div>
      <!-- 发布新的留言 -->
      <div class="write">
        <p class="board">留言板</p>
        <!-- <form method="post" action="https://youthapi.sdut.edu.cn/api/messageboard/insertdata"> -->
          <input type="text" name="author" placeholder="Name" value="" required v-model="author">
          <br>
          <input type="text" name="message" placeholder="Say your heart sound..." value="" required v-model="message">
          <br>
          <input type="text" name="receiver" placeholder="TO:" value="" v-model="receiver">
          <br>
          <input class="anniu" type="submit" value="@Sent" @click="postData">
        <!-- </form> -->
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data: function() {
    return {
      info: null,
      page:1,
      path:"https://easy-mock.com/mock/5cff245675c07b75126d9a13/api/messageboard/getdata/page" ,
      address:'',
      last_page:'',
      author:'',
      message:'',
      receiver:'',
      box:'https://easy-mock.com/mock/5cff245675c07b75126d9a13/api/messageboard/getdata/page'
    };
  },
  props: {
    msg: String
  },
   created(){
    this.getdata()
  },
  methods: {
    getdata: function() {
      this.path = this.box;
      this.path = this.path +  '=' + this.page;
      if(this.page == this.last_page)
      {
        this.page = 1;
      }
      else{
        this.page++;
      }
      this.axios({
        method: "post",
        url:this.path 
      }).then(res => {
        // console.log(res.data.data[0]);

        this.info = res.data.data;
        this.address = res.data;
       this.last_page = this.address.last_page;
        // console.log(this.page);
        // console.log(this.path);
        // console.log(this.last_page);
      });
      
  },
  postData:function(){
    
// console.log(this.author);
      this.axios({
    method:"post",
    url:"https://easy-mock.com/mock/5cff245675c07b75126d9a13/api/messageboard/getdata/page=1",
    data:{
        name:this.author,
        message:this.message,
        receiver:this.receiver
    }
}).then((res)=>{
    // console.log(res.data);
})

  },
    showDiv:function(q){
        var obj = document.getElementById('receiver'+ q);
        if(obj.innerText == 'NULL'){
          document.getElementById('to').style.display = 'none';
          document.getElementById('TO').style.display = 'none';
        }
		    document.getElementById('maskLayer').style.display = 'block';   
        document.getElementById('box').style.opacity = '0.3';  
        document.getElementById('author').innerHTML = document.getElementById('author'+ q).innerHTML;  
        document.getElementById('message').innerHTML = document.getElementById('message'+ q).innerHTML;  
        document.getElementById('date').innerHTML = document.getElementById('date'+ q).innerHTML;  
        document.getElementById('to').innerHTML = document.getElementById('receiver'+ q).innerHTML;  
        
    },
    closeDiv:function(){
      document.getElementById('maskLayer').style.display = 'none';   
        document.getElementById('box').style.opacity = '1';
    }
   
    }
  
 
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.circle {
    border-radius: 50%;
    width: 100px;
    height: 100px;
    margin: 5px;
    cursor: pointer;
}
.circle {
    box-shadow: 0px 4px 10px 1px #ffffff inset;
   color: currentColor;
   display: inline-block;
   text-decoration: none;
   animation: rise  timing-function delay iteration-count direction fill-mode;
   transition: transform 0.4s linear, box-shadow 0.15s linear, margin 0.1s linear, width 0.1s linear, height 0.1s linear;
 }
.circle p {
    color: rgb(10, 0, 0);
    font-size: 17px;
    text-overflow: ellipsis;
    white-space: nowrap;
    word-wrap: break-word;
    word-break: break-all;
    overflow: hidden;
}
.circle {
    animation: rise 3s  infinite;
    
  }
.liuyan {
    display: flex;
    justify-content:space-between;
    flex-wrap: wrap;
    padding-top: 20px;
    text-align: center;
}
.write {
    margin: 0 auto;
    height: 300px;
    text-align: center;
    border: 1px #fff;
    background-color:rgba(255, 255, 255,0.3);
}
input {
    text-align: center;
    border-radius: 10px;
    width: 300px;
    height: 45px;
    outline: none;
    font-size: 18px;
    border: none;
    font-weight: 700;
    margin: 5px;
    background-color:rgba(255, 255, 255,0.6);
}
.board {
    padding: 10px 0 0 0;
    font-weight: 700;
}
.anniu{
    /* background-color: #b4daf5; */
    background-color: #b4daf5;
}

 
.maskLayer {  
    position: fixed;  
    /* text-align:center;   */
    display: none;
    color: black;
    height: 100%;
    width: 100%;
    z-index: 99;
   
}
.maskLayer p {
    text-indent: 2em;
    margin: 0 auto;
    padding-bottom: 10px;
    text-decoration: underline rgb(184, 174, 174);
}
span {
    color: #3b5f77;
}
.detail {
    margin: 0 auto;
    width: 300px;
    height: auto;
    text-align: left;
    padding: 5px 5px 0px 10px;
    font-size: 20px;
    border: 1px rgb(245, 176, 176) solid;
    border-radius: 20px;
    margin: 170px auto;
    background-color: rgba(255, 255, 255, 0.7);
}
.detail input {
    border-radius: 10px;
    width: 150px;
    height: 40px;
}
.change {
    text-align: center;
    
}

a {
    color: rgb(53, 49, 49);
    cursor:pointer;
}

  @keyframes rise {
    0% {
      transform: translatey(0em);
    }

    50% {
      transform: translatey(-0.5em);
    }

    100% {
      transform: translatey(0em);
    }
  }

</style>
