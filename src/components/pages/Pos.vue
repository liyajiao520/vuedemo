<template>
  <div>
    <el-row >
      <el-col :span='7' class='white' id='order-height'>
        <el-tabs type="border-card">
          <el-tab-pane label="点餐">
            <el-table :data="tableData" border  style="width: 100%">
              <el-table-column prop="goodsName" label="商品名称" id="center"></el-table-column>
              <el-table-column prop="count" label="量" width="50"></el-table-column>
              <el-table-column prop="price" label="金额" width="70"></el-table-column>
              <el-table-column  label="操作" width="100" fixed="right">
                <template slot-scope="scope">
                  <el-button size="small"  type='text' @click="handleAdd(scope.$index, scope.row)">增加</el-button>
                  <el-button size="small"  type='text' @click="handleDelete(scope.$index, scope.row)">删除</el-button>
                </template>
              </el-table-column>
            </el-table>
            <div>总价:{{totalprice}}</div>
            <div>
              <el-col :span="8"><el-button type="warning" >挂单</el-button></el-col>
              <el-col :span="8"><el-button type="success" @click="Delete">删除</el-button></el-col>
              <el-col :span="8"><el-button type="warning" @click="Checkout">结账</el-button> </el-col>
            </div>
          </el-tab-pane>
          <el-tab-pane label="挂单" name="second">
            <el-table :data="tableData" border  style="width: 100%">
              <el-table-column prop="goodsName" label="商品名称" id="center"></el-table-column>
              <el-table-column prop="count" label="量" width="50"></el-table-column>
              <el-table-column prop="price" label="金额" width="70"></el-table-column>
              <el-table-column  label="操作" width="100" fixed="right">
                <template slot-scope="scope">
                  <el-button size="small"  type='text' @click="handleAdd(scope.$index, scope.row)">增加</el-button>
                  <el-button size="small"  type='text' @click="handleDelete(scope.$index, scope.row)">删除</el-button>
                </template>
              </el-table-column>
            </el-table>
            <div>总价:{{totalprice}}</div>
            <el-col :span="8"><el-button type="success" @click="Delete">删除</el-button></el-col>
            <el-col :span="8"><el-button type="warning" @click="Checkout">结账</el-button> </el-col>
          </el-tab-pane>
          <el-tab-pane label="外卖" name="third">
            <el-table :data="tableData" border  style="width: 100%">
              <el-table-column prop="goodsName" label="商品名称" id="center"></el-table-column>
              <el-table-column prop="count" label="量" width="50"></el-table-column>
              <el-table-column prop="price" label="金额" width="70"></el-table-column>
              <el-table-column  label="操作" width="100" fixed="right">
                <template slot-scope="scope">
                  <el-button size="small"  type='text' @click="handleAdd(scope.$index, scope.row)">增加</el-button>
                  <el-button size="small"  type='text' @click="handleDelete(scope.$index, scope.row)">删除</el-button>
                </template>
              </el-table-column>
            </el-table>
            <div>总价:{{totalprice}}</div>
            <el-col :span="8"><el-button type="success" @click="Delete">删除</el-button></el-col>
            <el-col :span="8"><el-button type="warning" @click="Checkout">结账</el-button> </el-col>
          </el-tab-pane>
        </el-tabs>
      </el-col>
      <!--商品展示-->
      <el-col :span="17">
        <div class="often-goods">
          <div class="title">常用商品</div>
          <div class="often-goods-list">
            <ul>
              <li v-for="Goods in oftenGoods" :key="Goods.goodsId" @click="add(Goods)">
                <span>{{Goods.goodsName}}</span>
                <span class="o-price">￥{{Goods.price}}元</span>
              </li>
            </ul>
          </div>
        </div>
        <div class="goods-type">
          <el-tabs type="border-card">
            <el-tabs>
              <el-tab-pane label="汉堡">
                <ul class='cookList'>
                  <li v-for="goods in type0Goods" :key="goods.goodsId" @click="add(goods)">
                    <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                    <span class="foodName">{{goods.goodsName}}</span>
                    <span class="foodPrice">￥{{goods.price}}元</span>
                  </li>
                </ul>
              </el-tab-pane>
              <el-tab-pane label="小食">
                <ul class='cookList'>
                  <li v-for="goods in type1Goods" :key="goods.goodsId" @click="add(goods)">
                    <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                    <span class="foodName">{{goods.goodsName}}</span>
                    <span class="foodPrice">￥{{goods.price}}元</span>
                  </li>
                </ul>
              </el-tab-pane>
              <el-tab-pane label="饮料">
                <ul class='cookList'>
                  <li v-for="goods in type2Goods" :key="goods.goodsId" @click="add(goods)">
                    <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                    <span class="foodName">{{goods.goodsName}}</span>
                    <span class="foodPrice">￥{{goods.price}}元</span>
                  </li>
                </ul>
              </el-tab-pane>
              <el-tab-pane label="套餐">
                <ul class='cookList'>
                  <li v-for="goods in type3Goods" :key="goods.goodsId" @click="add(goods)">
                    <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                    <span class="foodName">{{goods.goodsName}}</span>
                    <span class="foodPrice">￥{{goods.price}}元</span>
                  </li>
                </ul>
              </el-tab-pane>

            </el-tabs>
          </el-tabs>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Pos',
  data () {
    return {
      tableData: [],
      totalprice: 0,
      oftenGoods: [],
      type0Goods: [],
      type1Goods: [],
      type2Goods: [],
      type3Goods: []
    }
  },
  mounted () {
    var orderheight = document.body.clientHeight
    document.getElementById('order-height').style.height = orderheight + 'px'
    for (var i = 0; i < this.tableData.length; i++) {
      this.totalprice = (this.tableData[i].price) * (this.tableData[i].count) + this.totalprice
    }
  },
  created () {
    axios.get('http://jspang.com/DemoApi/oftenGoods.php')
      .then(response => {
        console.log(response)
        this.oftenGoods = response.data
      })
      .catch(error => {
        console.log(error)
        alert('网络错误，不能访问')
      })
    axios.get('http://jspang.com/DemoApi/typeGoods.php')
      .then(response => {
        console.log(response)
        this.type0Goods = response.data[0]
        this.type1Goods = response.data[1]
        this.type2Goods = response.data[2]
        this.type3Goods = response.data[3]
      })
      .catch(error => {
        console.log(error)
        alert('网络错误，不能访问')
      })
  },
  methods: {
    handleAdd (index, row) {
      this.totalprice = 0
      this.tableData[index].count = this.tableData[index].count + 1
      console.log(this.tableData[index].count)
      for (var i = 0; i < this.tableData.length; i++) {
        this.totalprice = (this.tableData[i].price) * (this.tableData[i].count) + this.totalprice
      }
    },
    handleDelete (index, row) {
      this.totalprice = 0
      row.count = row.count - 1
      if (row.count === 0) {
        this.tableData.splice(index, 1)
      }
      for (var i = 0; i < this.tableData.length; i++) {
        this.totalprice = (this.tableData[i].price) * (this.tableData[i].count) + this.totalprice
      }
    },
    Delete () {
      this.tableData = []
      this.totalprice = 0
    },
    Checkout () {
      console.log(this.tableData.length)
      if (this.tableData.length !== 0) {
        this.$message({
          message: '恭喜你，结账成功',
          type: 'success'
        })
      } else {
        this.$message({
          message: '清不要空结',
          type: 'warning'
        })
      }
      this.tableData = []
      this.totalprice = 0
    },
    add (goods) {
      this.totalprice = 0
      let isHave = false
      // 判断是否这个商品已经存在于订单列表
      for (let i = 0; i < this.tableData.length; i++) {
        console.log(this.tableData[i].goodsId)
        if (this.tableData[i].goodsId === goods.goodsId) {
          isHave = true //  存在
        }
      }
      //  根据isHave的值判断订单列表中是否已经有此商品
      if (isHave) {
        //  存在就进行数量添加
        let arr = this.tableData.filter(o => o.goodsId === goods.goodsId)
        arr[0].count++
      } else {
        //  不存在就推入数组
        let newGoods = {goodsId: goods.goodsId, goodsName: goods.goodsName, price: goods.price, count: 1}
        this.tableData.push(newGoods)
      }
      for (var i = 0; i < this.tableData.length; i++) {
        this.totalprice = (this.tableData[i].price) * (this.tableData[i].count) + this.totalprice
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .pos-order{
    background:white;
    border-right:1px solid #C0ccda;
  }
  .white{
    background:white
  }
.el-table th{
  text-align:center
}
.title{
  height: 20px;
  border-bottom:1px solid #D3DCE6;
  background-color: #F9FAFC;
  padding:10px;
}
.often-goods-list ul li{
  list-style: none;
  float:left;
  border:1px solid #E5E9F2;
  padding:10px;
  margin:5px;
  background-color:#fff;
}
.o-price{
  color:#58B7FF;
}
 .goods-type{
   clear:both;
 }
  .cookList li{
    list-style: none;
    width:23%;
    border:1px solid #E5E9F2;
    height: auot;
    overflow: hidden;
    background-color:#fff;
    padding: 2px;
    float:left;
    margin: 2px;

  }
  .cookList li span{
    display: block;
    float:left;
  }
  .foodImg{
    width: 40%;
  }
  .foodName{
    font-size: 15px;
    padding-left: 10px;
    color:brown;

  }
  .foodPrice{
    font-size: 16px;
    padding-left: 10px;
    padding-top:10px;
  }
  li:hover{
    cursor: pointer;
  }
</style>
