<template>
<div class="container">
  <div class="hello"> 
    <div class="terminal"> 
        <div class="terminal_text" id="terminal_text">
           {{data}}
        </div>

        <div class="terminal_text2" id="terminal_text">
        </div>
    </div>
    
    <div>
      <div class="device"></div>
      <div class="gaia_ok"></div>
      <div class="gaia_upload"></div>  
      <div class="eth"></div> 
    </div>
  </div>
</div>
</template>

<script>
var senRawData = require('./SensorData.json')
var senData = senRawData.data
console.log(senData.length)
export default {

  name: 'rawdata',
  props: ['user'],
  data () {
    return {
      timer:"",
      count: 0,
      data:''
    }
  },
  methods: {
    sensorInput(){
      console.log(this.count)
      var t = senData[this.count].sensorSteam
      var textdiv = document.getElementById("terminal_text");
      var reg = /(http:\/\/|https:\/\/)((\w|=|\?|\.|\/|&|-)+)/g;
      var url = t.match(reg);
      console.log(url);
      if (url!=null){
        textdiv.innerHTML += '<a target="_blank" href="'+t+'">'+senData[this.count].sensorSteam+'</a><br>';
      }
      else{
        textdiv.innerHTML += t + '<br>';
      }
      textdiv.scrollTop = textdiv.scrollHeight;

      //this.data += senData[this.count].sensorSteam + ' \n '
      this.count = this.count + 1
      if (this.count == senData.length) this.count = 0
    },
    ssync(){
      this.timer = setInterval(this.sensorInput, 1000);
    }

  },
  mounted(){
    this.ssync()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container{
  display: block;
}
.hello {
  display:flex;
  flex-direction: column;
  height:100%;
  justify-content: center;
  align-content: center;
}

.terminal{
    border-style:solid;
    width: 100%;
    height: 200px;
    border-width: 2px 0px 0px 0px;
    border-color: rgb(150,173,189);
    display:flex;
    justify-content: center;
    align-content: center;
}
.terminal_text2{
    overflow-y:scroll;
    background-color: rgb(150,173,189);
    caret-color: white;
    text-shadow: 0px 0px 0px rgb(87, 80, 124);
    -webkit-text-fill-color: transparent;
    font-size: 14px;
    font-weight: 500;
    letter-spacing:1px;
    padding:10px 10px 10px 10px;
    border-style: none;
    width:30%
}
.terminal_text{
    overflow-y:scroll;
    background-color: rgb(150,173,189);
    caret-color: white;
    text-shadow: 0px 0px 0px rgb(87, 80, 124);
    -webkit-text-fill-color: transparent;
    font-size: 14px;
    font-weight: 500;
    letter-spacing:1px;
    padding:10px 10px 10px 10px;
    border-style: none;
    width:70%;
    scrollbar-base-color:#ff6600;
}


.gaia_ok{
    background: url(../assets/gaia_ok.png);
    height:100px;
    width:100px;
    background-size:100% 100%;
}

.gaia_upload{
    background: url(../assets/gaia_upload.png);
    height:100px;
    width:100px;
    background-size:100% 100%;
}

.eth{
    background: url(../assets/eth.png);
    height:100px;
    width:100px;
    background-size:100% 100%;
}

.device{
    background: url(../assets/device.png);
    height:100px;
    width:100px;
    background-size:100% 100%;
}


</style>
