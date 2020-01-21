<template>
<div id="app">
        <div class="add">
            编号：<input type="text" v-model="newiid"> 品牌名称：
            <input type="text" v-model="newname" @enter="adddata">
            <input type="button" value="添加" @click="adddata">
        </div>
        <div class="add">
            品牌名称：<input type="text" placeholder="请输入搜索条件" v-model="keyword">
        </div>
        <div class="biaoge">
            <table class="tb" >
                <tr>
                    <th>编号</th>
                    <th>品牌名称</th>
                    <th>创立时间</th>
                    <th>操作</th>
                </tr>
                <tr v-for="(item,index) in search(keyword)" :key="index">
                    <td>{{item.iid}}</td>
                    <td>{{item.name}}</td>
                    <td>{{item.time}}</td>
                    <td><label @click="set(item,index)">编辑</label>
                        <label @click="deldata(index)">删除</label></td>
                </tr>
            </table>
        </div>
        <div class="tan">
            <div class="tan1">
                <div class="bianhao">
                    <label>编 号：</label>
                </div>
                <input type="text" v-model="siid"></div>
            <div class="tan2">
                <div class="mingchen">品牌名称：</div>
                <input type="text" v-model="sname"></div>
            <button>取消</button>
            <button @click="update">确定</button>
        </div>
       <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page="currentPage4"
      :page-sizes="[1, 2, 3, 4]"
      :page-size="100"
      layout="total, sizes, prev, pager, next, jumper"
      :total="100"
      >
    </el-pagination>
    </div>
       </template>
    <script src="./axios.js"></script>

<script>
    export default {
  created () {
             this.fetchuserlist ();
            },
        data () {
            return {
                currentPage1: 5,
        currentPage2: 5,
        currentPage3: 5,
        currentPage4: 4,
                 newiid: '',
                newname: '',
                keyword: '',
                sname: '',
                siid: '',
                iid: '',
            userlist: [],
            lists: [],

            list: [],
                list: [{
                    iid: 33,
                    name: 'LV',
                    time: new Date()
                }, {
                    iid: 23,
                    name: 'L22V',
                    time: new Date()
                }, {
                    iid: 53,
                    name: 'LqqV',
                    time: new Date()
                } ]

            }
        },

        methods: {
              set (obj, indexx) {
                        this.siid = obj.iid
                         this.index = indexx
                        this.sname = obj.name
//  console.log(this.list.length)
                        console.log(this.list)
                },
                update () {
                    this.list[this.index].iid = this.siid
                 this.list[this.index].name = this.sname
                },
                adddata () {
                    this.list.push({
                        iid: this.newiid,
  name: this.newname,
                        time: new Date(),
                    })
                },
                search (word) {
                    return this.list.filter(obj => {
                        if (obj.name.includes(word)) return obj
                    })
                },
                deldata (x) {
                    this.list.splice(x, 1)
                },
                 handleSizeChange (val) {
        console.log(`每页 ${val} 条`);
      },
      handleCurrentChange (val) {
        console.log(`当前页: ${val}`);
      },

         fetchuserlist()  {
                this.$http.get('http://localhost:3000/posts')
                    .then(function(response)  {
console.log(response)
console.log(response.body[0].title)

response.body[0]. title=this.list.name,
              response.body[0].author=this.list.time,
             response.body[0].id=this.list.iid
response.body.forEach(item =>{this.lists.push(item);console.log(this.lists[0].id)})
                   })

        }}

 }
</script>
<style>
 #app {
            width: 600px;
            margin: 10px auto;
            position: relative;
        }

        .tb {
            border-collapse: collapse;
            width: 100%;
        }

        .tb th {
            background-color: #0094ff;
            color: white;
        }

        .tb td,
        .tb th {
            padding: 5px;
            border: 1px solid black;
            text-align: center;
        }

        .add {
            padding: 5px;
            border: 1px solid black;
            margin-bottom: 10px;
        }

</style>