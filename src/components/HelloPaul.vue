<template>
  <div id='calculate'>
    <div class="calBlock"><p>{{message}}</p></div>
    <div class="buttonBlock">
        <c-button 
            v-for="b in buttons"
            :key="b.name"
            :name="b.name"
            :type="b.type"
            @numberclick="number"
            @operatorclick="cal"
        ></c-button>
    </div>
    <div class="clearfix"></div>
  </div>
</template>

<script>
import CButton from './CButton'
export default {
  name: "HelloPaul",
  data() {
    return {
        message:"0",
        sum:0,
        operation:"",
        operating:"",

        buttons: [
            { name: '%', type: '' },
            { name: '√', type: '' },
            { name: 'x2', type: '' },
            { name: '1/x', type: '' },

            { name: 'CE', type: '' },
            { name: 'C', type: '' },
            { name: '→', type: '' },
            { name: '÷', type: '' },

            { name: '7', type: 'number' },
            { name: '8', type: 'number' },
            { name: '9', type: 'number' },
            { name: 'X', type: '' },

            { name: '4', type: 'number' },
            { name: '5', type: 'number' },
            { name: '6', type: 'number' },
            { name: '-', type: '' },

            { name: '1', type: 'number' },
            { name: '2', type: 'number' },
            { name: '3', type: 'number' },
            { name: '+', type: '' },

            { name: '±', type: '' },
            { name: '0', type: 'number' },
            { name: '.', type: '' },
            { name: '=', type: '' }
        ]
    };
  },
  components: {
      CButton
  },
  methods:{
    // 數字鍵的功能
    number:function (value){
        // 數字鍵不為0時的判斷
        if(value !== "0"){
            if(this.message === "0"){
                this.message = value;
            }else if(this.operating !==""){
                this.message = value;
                this.operating = "";
            }else{
                this.message += value;
            }
        // 數字鍵為0的判斷
        }else{
            if(this.message === "0"){
                
            }else{
                this.message += value;
            }
        }
    },
    cal:function (value){
        switch(value){
            case "√":
                this.message = (Math.sqrt(parseFloat(this.message))).toString();
                break;
            case "x2":
                this.message = (parseFloat(this.message)*parseFloat(this.message)).toString();
                break;
            case "1/x":
                this.message = (1/(parseFloat(this.message))).toString();
                break;
            case "C":
                this.sum = 0;
                this.message = "0";
                this.operation = "";
                break;
            case "→":
                if(this.message.length<2){
                    this.message = "0";
                }else{
                    this.message = this.message.substring(0,this.message.length-1);
                }
                break;
            case "CE":
                this.message = "0";
                break;
            case ".":
                if(this.message.indexOf(".") === -1){
                    this.message += "."; 
                }
                break;
            case "±":
                if(this.message.indexOf("-") === -1){
                    if(this.message === "0"){
                        
                    }else{
                        this.message = '-' + this.message;
                    } 
                }
                break;
            // 加減乘除功能
            case "+":
                if(this.operation !== "+"){
                    this.sum += parseFloat(this.message);
                    this.operation = "+";
                    this.operating = "do";
                }
                break;
            case "-":
                if(this.operation !== "-"){
                    // 讓初始值不為0
                    if(this.sum == 0){
                        this.sum = parseFloat(this.message);
                        this.operation = "-";
                        this.operating = "do";
                    }else{
                // 減號運作流程
                        this.sum -= parseFloat(this.message);
                        this.operation = "-";
                        this.operating = "do";
                    }
                } 
                break;
            case "X":
                if(this.operation !== "X"){
                    // 讓初始值不為0
                    if(this.sum == 0){
                    this.sum = parseFloat(this.message);
                    this.operation = "X";
                    this.operating = "do";
                }else{
                // 減號運作流程
                    this.sum -= parseFloat(this.message);
                    this.operation = "X";
                    this.operating = "do";
                }
            }
                break;
            case "÷":
                if(this.operation !== "÷"){
                    // 讓初始值不為0
                    if(this.sum == 0){
                    this.sum = parseFloat(this.message);
                    this.operation = "÷";
                    this.operating = "do";
                }else{
                // 減號運作流程
                    this.sum -= parseFloat(this.message);
                    this.operation = "÷";
                    this.operating = "do";
                }
            }
                break;
            case "=":
                if(this.operation === "+"){
                    this.message = (this.sum + parseFloat(this.message)).toString();
                }else if(this.operation === "-"){
                    this.message = (this.sum - parseFloat(this.message)).toString();
                }else if(this.operation === "X"){
                    this.message = (this.sum * parseFloat(this.message)).toString();
                }else if(this.operation === "÷"){
                    this.message = (this.sum / parseFloat(this.message)).toString();
                }
                this.operation = "";
                this.sum = 0;
                break;
            }    
    },
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  margin: 0;
  padding: 0;
}
#calculate {
  width: 400px;
  /* height:600px; */
  background-color: rgba(0, 0, 0, 0);
  border: 1px solid #000;
  margin: 5% auto;
}
.calView {
  margin: 10px auto;
  width: 396px;
  height: 50px;
  text-align: right;
  background-color: #aaa;
}
.calBlock {
  margin: auto;
  width: 396px;
  height: 100px;
  font-size: 36px;
  text-align: right;
  line-height: 100px;
}
.buttonBlock {
  width: 400px;
}
.calButton {
  width: 96px;
  float: left;
  margin: 2px;
  background-color: #bbb;
  height: 50px;
  text-align: center;
  line-height: 50px;
  cursor: pointer;
}
.calButton:hover {
  background: #000;
  color: #fff;
}
.number {
  background-color: #ddd;
}
.clearfix {
  clear: both;
}
</style>
