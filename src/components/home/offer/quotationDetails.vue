<template>
  <div class="commodity" v-loading="loading" style="width: 100%;height:100%;">
     <div v-title data-title="商品管理">商户-商品管理</div>
      <!-- <header-Top></header-Top> -->
      <div class="content clearfix">
        <div class="quotation_details">
          <div class="quo_head">
              <p class="commodity">商品 > 报价管理> 报价单详情</p>
          </div>
          <div class="bidder">
            <img src="../../../assets/background.png" />
            <p class="bidder_text">报价方</p>
            <div class="materials">
              <p class="materials_com">上海光泰包装材料有限公司</p>
              <div class="contact">
                <!-- <p>
                  联系人：胡鹏<br>
                  联系电话：15675999803<br>
                  与贵司累计成交金额：0 元
                </p>
                <p>
                  注册资本：150.0万元/人民币元<br>
                  与贵司累计报价次数：1次
                </p>
                <p>
                  主营行业：/<br>
                  与贵司累计成交单数：0单
                </p> -->
                <p>
                  联系人：{{details.bus_name}}<br>
                  联系电话：{{details.mobile}}<br>
                  与贵司累计成交金额：{{details.price_sum}} 元
                </p>
                <p>
                  注册资本：{{details.registered_capital}}万元/人民币元<br>
                  <!-- 企业名称：{{details.company_name}} -->
                  与贵司累计报价次数：{{details.offer_num}} 次
                </p>
                <p>
                  企业类型：{{details.enterprise_type}}<br>
                  <!-- 店铺名：{{details.shop_name}} -->
                  与贵司累计成交单数：{{details.order_num}} 单
                </p>
              </div>
            </div>
          </div>
          <div class="information">
            <div class="quo_in">
              <div class="text">
              <span class="quo_line"></span>
              <span class="quo_text">报价信息</span>
              </div>
              <!-- <p>报价状态：<span>已报价</span></p>
              <p>报价时间：<span>2020年10月12日 15:36:48</span></p>
              <p>报价类型：<span>协议价格（长期供货）</span></p>
              <p>价格有效期：<span>2020年10月15日 - 2020年10月18日（还剩6天）</span></p>
              <p>共<span>1 </span>行物料&nbsp;&nbsp;&nbsp;&nbsp;已报价<span>1 </span>行&nbsp;&nbsp;物料</p> -->
              <p>报价状态：<span></span></p>
              <p>报价时间：<span>{{details.create_time}}</span></p>
              <!-- <p>报价类型：{{details.offer_num}}<span></span></p>
              <p>价格有效期：<span></span></p> -->
              <p>是否中标：<span></span></p>
              <p>共<span> </span>行物料&nbsp;&nbsp;&nbsp;&nbsp;已报价<span> </span>行&nbsp;&nbsp;物料</p>
            </div>
            <div class="mat_in">
              <p>行号</p>
              <p>物料信息</p>
              <p>项目编号</p>
              <p>最小起订量</p>
              <p>最小包装(必填)</p>
              <p>L/T(必填)</p>
              <p>未税单价</p>
              <p>未税小计(元)</p>
              <p>税率</p>
              <p>附件</p>
            </div>
            <div class="packaging_paper">
              <p>{{project.id}}</p>
              <p @click="goodsDetail(details.goods_id)" style="color: #2ac845">{{details.title}}</p>
              <el-dialog  :visible.sync="menuRoleVisible">
                <table width="100%" cellspacing="0" cellpadding="0" class="logistics_x">
                  <tr>
                    <td align="right" class="black">商品名称:</td>
                    <td>
                      <el-input v-model="goodsTitle.title" class="el-input" disabled="true">
                      </el-input>
                    </td>
                  </tr>
                  <tr>
                    <td align="right" class="black">商品描述:</td>
                    <td>
                      <el-input v-model="goodsTitle.description"  class="el-input" type="textarea">
                      </el-input>
                    </td>
                  </tr>
                  <tr>
                    <td align="right" class="black">补充说明:</td>
                    <td>
                      <el-input v-model="goodsTitle.explain"  class="el-input" type="textarea">
                      </el-input>
                    </td>
                  </tr>
                  <tr>
                    <td align="center" colspan="2" class="black">商品规格</td>
                  </tr>
                </table>
                <el-table
                    tooltip-effect="dark"
                    ref="multipleTable"
                    :data="gridData"
                    width="700"
                    height="300"
                >
                  <el-table-column show-overflow-tooltip prop="name" label="规格"></el-table-column>
                  <el-table-column show-overflow-tooltip prop="value" label="值"></el-table-column>
                </el-table>
              </el-dialog>
              <p>{{details.project_id}}</p>
              <p>{{details.minimum}}</p>
              <p>{{details.packaging}}</p>
              <p><span>{{details.lt}}</span></p>
              <p><span>¥{{details.unit_price}}</span></p>
              <p><span>¥{{details.unit_subtotal}}</span></p>
              <p>{{details.tax_rate}}%</p>
              <p>
                  <img :src="URL + details.pic_url" class="imgcss" />
              </p>
            </div>
            <div class="total">
              <!-- <p>产品总额：<span>¥100000.00 </span><span>（含运费：¥0.00）</span></p> -->
              <p>产品总额：<span>¥{{details.total_price}} </span><span>（含运费：¥0.00）</span></p>
            </div>
            <div class="trading_information">
              <div class="info">
              <span class="info_line"></span>
              <span class="info_text">交易信息</span>
              </div>
              <p>交易方式：<span>担保交易</span></p>
              <!-- <p>备货周期：<span></span></p> -->
              <p>交货期：<span>自下单后 {{dayD}} 天内交货至指定地点</span></p>
              <p>收货地：<span>{{project.prov_name}} {{project.city_name}} {{project.dist_name}}</span></p>
              <p>税务发票：<span>提供增值税专用发票 （自行开票）</span></p>
              <!-- <p>附件：<span>{{details.pic_url}}</span></p> -->
              <p>补充说明：<span></span></p>
            </div>
          </div>
        </div>
      </div>
      <!-- <Merchant-Foot></Merchant-Foot> -->
  </div>
</template>
<script>
import headerTop from '@/components/header/top'; //头部
import MerchantFoot from '@/components/foot/foot'; //脚部
export default {
    name:'quotationDetails',
    data (){
      return {
          loading:true,
          details: '',
          project: '',
          dayD: '',
          menuRoleVisible:false,
          gridData:[],
          goodsTitle:{

        },
      }
    },
    created(){
      this.getProjectDetail();
      setTimeout(() => {
        this.loading = false;
        }, 300);
    },
    methods:{
      getProjectDetail() {
        this.$HTTP(this.$httpConfig.offerDetail, {
          id: this.$route.params.id
        })
        .then(res => {
          this.details = res.data.data;
          this.project = this.details.project;
          var now_time = new Date().getDate()
          this.computationTime(now_time, res.data.data.project.delivery_time);
        })
        .catch(err => {
          console.log(err);
        });
      },
      computationTime(now_Time, timestamp) {
        let t = null;
        let now = new Date(now_Time * 1000);
        let endTime = new Date(timestamp * 1000);
        if (now > endTime) {
          t = now.getTime() - endTime.getTime();
        } else {
          t = endTime.getTime() - now.getTime();
        }
        if (t > 0) {
          let day = Math.floor(t / 86400000);
          this.dayD = day;
        }
      },
      /*商品详情*/
      goodsDetail(goods_id) {

        this.$HTTP(this.$httpConfig.customizedDetailById, {
          id: goods_id,
        }).then(res => {
          this.menuRoleVisible =true;
          this.goodsTitle = res.data.data;
          this.gridData = res.data.data.space;

        }).catch(err => {
          console.log(err);
        });
      },
    },
    components: {
      headerTop,
      MerchantFoot,
    }
            
}
</script>

<style lang="less" scoped>
.commodity {
  position: relative;
  .content {
    // width: 1266px;
    width: 1025px;
    color: #a4a5a7;
    margin: 0 auto;
    overflow: hidden;
    background: #f1f1f1;
    padding-bottom: 80px;
    .quotation_details {
      // padding: 20px 20px;
      padding: 18px 0 18px 18px;
      .quo_head {
        padding-bottom: 20px;
        .commodity {
          font-size: 12px;
          color: #333;
        }
      }
      .bidder {
        height: 205px;
        padding: 0 20px;
        background: #fff;
        .bidder_text {
          font-size: 14px;
          color: #fff;
          margin: -30px 0 0 11px;
        }
        .materials {
          padding: 20px 30px;
          .materials_com {
            font-size: 14px;
            color: #496AB4;
            padding: 8px 0;
          }
          .contact {
            display: flex;
            p {
              width: 400px;
              font-size: 14px;
              color: #333;
              line-height: 30px;
            }
          }
        }
      }
      .information {
        background: #fff;
        margin-top: 20px;
        .quo_in {
          padding: 30px 20px 20px 20px;
          .text {
            padding-bottom: 10px;
            margin-bottom: 15px;
            border-bottom: 1px solid #f1f1f1;
            .quo_line {
              padding: 4px 8px;
              border-left: 5px solid #D02629;
            }
            .quo_text {
              font-size: 18px;
              color: #333;
            }
          }
          p {
            font-size: 14px;
            color: #333;
            line-height: 30px;
            span {
              padding-left: 10px;
            }
          }
          p:nth-of-type(4) {
            padding-top: 20px;
            span {
              color: #4494F9;
            }
          }
        }
        .mat_in {
          margin: 0 5px;
          // padding: 25px;
          padding: 15px;
          display: flex;
          border: 1px solid #DDDDDD;
          p {
            font-size: 13px;
            color: #000;
          }
          p:nth-of-type(2) {
            // padding: 0 80px 0 100px;
            padding: 0 65px;
          }
          p:nth-of-type(4) {
            // padding: 0 25px 0 35px;
            padding: 0 18px;
          }
          p:nth-of-type(6) {
            // padding: 0 60px 0 55px;
            padding: 0 50px 0 20px;
          }
          p:nth-of-type(8) {
            // padding: 0 55px 0 55px;
            padding: 0 55px;
          }
          p:nth-of-type(10) {
            // padding-left: 100px;
            padding-left: 60px;
          }
        }
        .imgcss {
          width: 35px;
        }
        .packaging_paper p { 
          display: flex;
          align-items: center;
        }
        .packaging_paper {
          margin:0 5px;
          // padding: 25px;
          padding: 15px;
          display: flex;
          border-left: 1px solid #DDDDDD;
          border-right: 1px solid #DDDDDD;
          border-bottom: 1px solid #DDDDDD;
          p {
            font-size: 13px;
            color: #000;
          }
          .logistics_x {
            tr {
              td {
                padding: 5px;
                .el-input {
                  width: 400px;
                }
                .ss {
                  margin: 0;
                }
                b {
                  color: #ff0000;
                }
                .notes {
                  padding-left: 15px;
                }
                input,
                select {
                  padding-left: 5px;
                  width: 288px;
                  height: 32px;
                  border: 1px solid #cccccc;
                }
                textarea {
                  padding-left: 5px;
                  padding-top: 5px;
                  min-height: 50px;
                  border: 1px solid #cccccc;
                }
              }
            }
          }
          span {
            color: #D02629;
          }
          p:nth-of-type(1) {
            // width: 50px;
            width: 40px;
            padding-left: 10px;
          }
          p:nth-of-type(2) {
            padding: 0 10px;
            // width: 200px;
            width: 150px;
          }
          p:nth-of-type(3) {
            padding: 0 10px;
            // width: 50px;
            width: 40px;
          }
          p:nth-of-type(4) {
            padding: 0 10px;
            // width: 100px;
            width: 70px;
          }
          p:nth-of-type(5) {
            padding: 0 10px;
            // width: 80px;
            width: 50px;
          }
          p:nth-of-type(6) {
            padding: 0 10px;
            width: 100px;
          }
          p:nth-of-type(7) {
            padding: 0 10px;
            width: 100px;
          }
          p:nth-of-type(8) {
            padding: 0 10px;
            width: 100px;
          }
          p:nth-of-type(9) {
            padding: 0 10px;
            // width: 70px;
            width: 50px;
          }
          p:nth-of-type(10) {
            color: #496AB4;
            padding-left: 20px;
          }
        }
        .total {
          margin:0 5px;
          // padding: 25px;
          padding: 20px 20px 50px 0;
          border-left: 1px solid #DDDDDD;
          border-right: 1px solid #DDDDDD;
          border-bottom: 1px solid #DDDDDD;
          p {
            font-size: 13px;
            color: #000;
            // padding-left: 880px;
            // padding-left: 680px;
            float: right;
            span:nth-of-type(1) {
              font-size: 18px;
              color: #D02629;
            }
            span:nth-of-type(2) {
              color: #999999;
            }
          }
        }
        .trading_information {
          padding: 40px 20px 60px 20px;
          .info {
            padding-bottom: 10px;
            margin-bottom: 15px;
            border-bottom: 1px solid #f1f1f1;
            .info_line {
              padding: 4px 8px;
              border-left: 5px solid #D02629;
            }
            .info_text {
              font-size: 18px;
              color: #333;
            }
          }
          p {
            font-size: 14px;
            color: #333;
            line-height: 30px;
            span {
              padding-left: 10px;
            }
          }
          p:nth-of-type(6) {
            span {
            color: #496AB4;
            }
          }
        }
      }
    }
  }
}
</style>