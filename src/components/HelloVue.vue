<template>
    <div id="tableTest">
        <table>
            <!-- 表單標題 -->
            <tr><th>性別</th><th>名字</th><th>電話</th><th>E-mail</th></tr>
            <!-- 表單內容 -->
            <c-content
                v-for="s in shows"
                :key="s.sPhone"
                :sGender="s.sGender"
                :sName="s.sName"
                :sPhone="s.sPhone"
                :sMail="s.sMail"
            ></c-content>
            <!-- 分頁功能 -->
        </table>
        <pagination
            :perShow="perShow"
            :count="infos.length"
            :currentPage="currentPage"
            @click="click"
        />
        <!-- <div class="pagination">
            <ul>
                <pagination
                v-for="p in page"
                :key="p.page"
                :page="p.page"
                :type ="p.type"
                @getData="data"
                ></pagination>
            </ul>
        </div> -->
    </div>
</template>

<script>
import axios from 'axios'
import CContent from './CContent'
import pagination from './pagination'
export default {
    data(){
        return{
            infos:[],
            cPage:null,
            prePage:null,
            page:[
                {page:"<" ,type:""},
                {page:1 ,type:{liColor:true}},
                {page:2 ,type:""},
                {page:3 ,type:""},
                {page:4 ,type:""},
                {page:5 ,type:""},
                {page:"..." ,type:""},
                {page:null ,type:""},
                {page:">" ,type:""},
            ],
            shows:[],

            perShow: 10,
            currentPage: 1
        }
    },
    created: function() {
        // 取資料回來
        axios.get('https://randomuser.me/api/?results=500').then(r =>{
            // 將全部資料放進infos裡面
            for(let i =0 ;i<r.data.results.length;i++){
                this.infos.push({
                    gender: r.data.results[i].gender,
                    name: r.data.results[i].name.first + ' ' + r.data.results[i].name.last,
                    phone: r.data.results[i].cell,
                    mail: r.data.results[i].email
                })
            }
            //     // 將資料放進pages陣列裡(計算資料筆數需要幾個page)
            // this.page[7] = {page:(r.data.results.length/10)}

            // 一開始沒資料先放10筆進去
            for(let i = 0;i< this.perShow; i++){
                    this.shows.push({
                        sGender: this.infos[i].gender,
                        sName: this.infos[i].name,
                        sPhone: this.infos[i].phone,
                        sMail: this.infos[i].mail
                })
            }
        })
    },
    components:{
        CContent,
        pagination
    },
    methods:{
        data:function (value){
                
                
                // 判斷切換pagination畫面(如果是數字才執行動作)
                if(value>0 && value<=50){
                    // 清空陣列避免每次點按鈕會加資料上去
                    this.shows=[];
                        
                        if(value>4 && value<47){
                            if(value===5){
                                this.page[2].page = "..."
                                this.page[3].page = 4
                                this.page[4].page = 5
                                this.page[5].page = 6
                            }else if(value === 46 && this.page[6] !== "..."){
                                this.page[3].page = 45
                                this.page[4].page = 46
                                this.page[5].page = 47
                                this.page[6].page = "..."
                            }else{
                                if(value > this.page[4].page){
                                    this.page[3].page +=1
                                    this.page[4].page +=1
                                    this.page[5].page +=1
                                }else if(value <this.page[4].page){
                                    this.page[3].page -=1
                                    this.page[4].page -=1
                                    this.page[5].page -=1
                                }
                            }

                            
                            
                    }else if(value<5){
                        this.page[2].page = 2
                        this.page[3].page = 3
                        this.page[4].page = 4
                        this.page[5].page = 5
                        this.page[6].page = "..."
                        // 當前頁面變色
                        // if(this.cPage === null){
                        //     this.cPage = this.page[value].page
                        //     this.prePage = this.page[value].page
                        //     this.page[1].type = {liColor:false}
                        //     this.page[this.cPage].type = {liColor:true}
                        // }else{
                        //     this.prePage = this.cPage
                        //     this.cPage = this.page[value].page
                        //     this.page[this.prePage].type = {liColor:false}
                        //     this.page[this.cPage].type = {liColor:true}
                        // }
                        
                        //  console.log(this.cPage)
                        //  console.log(this.prePage)
                        // this.page[this.prePage].type = {liColor:false}
                        
                        
                        
                    }else if(value>46){
                        if(value === 47 || value === 50){
                            this.page[2].page = "..."
                            this.page[3].page = 46
                            this.page[4].page = 47
                            this.page[5].page = 48
                            this.page[6].page = 49
                        }
                    }
                    // 將資料傳入shows顯示畫面
                    for(let i = (value-1)*10;i< value*10;i++){
                            this.shows.push({
                                sGender: this.infos[i].gender,
                                sName: this.infos[i].name,
                                sPhone: this.infos[i].phone,
                                sMail: this.infos[i].mail
                            })
                        }
                }
        },
        click: function (value) {
            // 將資料傳入shows顯示畫面
            const data = []
            for(let i = (value-1)*10;i< value*10;i++){
                data.push({
                    sGender: this.infos[i].gender,
                    sName: this.infos[i].name,
                    sPhone: this.infos[i].phone,
                    sMail: this.infos[i].mail
                })
            }

            this.shows = data
            this.currentPage = value
        }
    }
}
</script>

<style scoped>

*{
    margin:0px;
    padding:0px;
}
#tableTest{
    
    width:50%;
    margin:50px auto;
    padding:10px;
    border:1px solid #DDD;
}
.pagination{
    font-size: 0px;
}
.pagination ul{
    margin-top:20px;
}
.pagination li{
    padding:10px;
    display:inline-block;
    border:1px solid #CCC;
    font-size: 14px;
    cursor: pointer;
}
.liColor{
    background-color: aqua;
}
#tableTest table{
    width:100%;
    border-collapse: collapse;
    text-align: center;
}
th{
    padding:10px;
}
tr:nth-child(odd){
    background-color: #DDD;
}
</style>


