<template>
  <div class="hello"> 
    <div class="terminal"> 
        <div class="terminal_text" id="terminal_text">
           {{data}}
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
.hello {
  display:flex;
  height:200px;
  justify-content: center;
  align-content: center;
}

.terminal{
    border-style:solid;
    width: 600px;
    border-width: 2px 0px 0px 0px;
    border-color: rgb(24,26,31);
    display:flex;
}

.terminal_text{
    overflow:scroll;
    background-color: rgb(33,37,43);
    caret-color: white;
    text-shadow: 0px 0px 0px #FFFFFF;
    -webkit-text-fill-color: transparent;
    font-size: 14px;
    font-weight: 500;
    letter-spacing:1px;
    padding:10px 10px 10px 10px;
    flex :1;
    border-style: none;
    width:100%
}


</style>
