<template>
  <div class="commodity" v-loading="loading" style="width: 100%;height:100%;">
     <div v-title data-title="商品管理">商户-商品管理</div>
      <!-- <header-Top></header-Top> -->
      <div class="content clearfix">
        <div class="quotation_store">
          <div class="quo_head">
              <!-- <p class="commodity">商品 > 询价管理> 询价单><span>潍坊山水水泥有限公司夏被包装盒询价单</span></p> -->
              <p class="commodity">商品 > 询价管理> 询价单</p>
          </div>
          <div class="quilt_box">
            <div class="inquirer">
            <!-- <p>询价方：中铁电气化铁路运营管理有限公司</p> -->
            <p>询价方：{{projectDetail.name}}</p>
            <!-- <p>询价标题：<span>中铁电气化铁路运营管理有限公司呼和公司包头运营维管段</span></p> -->
            <p>询价标题：<span>{{projectDetail.title}}</span></p>
            <!-- <p>收货地区：内蒙古 包头 固阳县 西斗铺镇内蒙古包头市固阳县西斗铺镇</p> -->
            <p>收货地区：{{projectDetail.prov_name}} {{projectDetail.city_name}} {{projectDetail.dist_name}} {{projectDetail.address}}</p>
            </div>
            <!-- <p class="quo_information">报价信息 <span>报含税价 | 发票需要包含运费 | 报价需要包含运费 | 必须对询价单全部物料报价</span></p> -->
            <p class="quo_information">报价信息 
              <span v-if="projectDetail.offer_type == 0">需要报含税价</span>
              <span v-if="projectDetail.offer_type == 1">允许对询价单部分物料报价</span>
              <span v-if="projectDetail.offer_type == 2">报价需要包含运费</span>
            </p>
            <div class="total_search">
              <p>共 <span>{{goodsList.length}}</span> 行物料</p>
              <el-input class="el-input1" placeholder="按照物料名称/编码快速查找" v-model="input" size="small">
                <el-button slot="append" icon="el-icon-search"></el-button>
              </el-input>
            </div>
            <div class="col_head">
              <p>行号</p>
              <p>物料信息</p>
              <p>项目编号</p>
              <p>数量</p>
              <p>最小起订量</p>
              <p>最小包装(必填)</p>
              <p>L/T(必填)</p>
              <p>未税单价</p>
              <p>未税小计(元)</p>
              <p>税率</p>
              <p>附件</p>
            </div>
            <!-- <div class="col_head1" v-for="i in 3" :key="i">
              <p>1</p>
              <p>包装<br>纸类包装容器<br>纸盒</p>
              <p>0101BJ202009260743</p>
              <p>
                <el-input v-model="input"></el-input><br>
                元/PCS
              </p>
              <p>
                <el-input v-model="input"></el-input>
              </p>
              <p>
                <el-input v-model="input"></el-input>
              </p>
              <p>
                <el-input v-model="input"></el-input>
              </p>
              <p>
                <el-input v-model="input"></el-input>
              </p>
              <p>
                <el-select v-model="value" placeholder="">
                  <el-option
                    v-for="item in options"
                    :key="item.value"
                    :label="item.label"
                    :value="item.value">
                  </el-option>
                </el-select>
              </p>
              <p>上传</p>
            </div> -->

            <div class="col_head1" v-for="(item, index) in goodsList" :key="index">
              <p>{{item.id}}</p>
              <p>{{item.title}}</p>
              <p>{{item.project_id}}</p>
              <p>{{item.number}}</p>
              <!-- <p><el-input v-model="project_id[index]"></el-input></p> -->
              <p>
                <!-- <input
                  type="text"
                  :value="listItem1"
                  :key="index"
                /><br> -->
                <!-- <input
                  type="text"
                  :v-model="input1"
                /><br> -->
                <el-input v-model="input1[index]" oninput="this.value = this.value.replace(/[^0-9.]/g, '').replace(/(\..*)\./g, '$1');"></el-input><br>
                元/PCS
              </p>
              <p>
                <!-- <input
                  type="text"
                  :value="listItem2"
                  :key="index"
                /> -->
                <!-- <input
                  type="text"
                  :v-model="input2"
                /> -->
                <el-input v-model="input2[index]" oninput="this.value = this.value.replace(/[^0-9.]/g, '').replace(/(\..*)\./g, '$1');"></el-input>
              </p>
              <p>
                <!-- <input
                  type="text"
                  :value="listItem3"
                  :key="index"
                /> -->
                <!-- <input
                  type="text"
                  :v-model="input3"
                /> -->
                <el-input v-model="input3[index]" oninput="this.value = this.value.replace(/[^0-9.]/g, '').replace(/(\..*)\./g, '$1');"></el-input>
              </p>
              <p>
                <!-- <input
                  type="text"
                  :value="listItem4"
                  :key="index"
                /> -->
                <!-- <input
                  type="text"
                  :v-model="input4"
                /> -->
                <el-input v-model="input4[index]" oninput="this.value = this.value.replace(/[^0-9.]/g, '').replace(/(\..*)\./g, '$1');"></el-input>
              </p>
              <p>
                <!-- <input
                  type="text"
                  :value="listItem5"
                  :key="index"
                /> -->
                <!-- <input
                  type="text"
                  :v-model="input5"
                /> -->
                <!-- <el-input :disabled="true" v-model="input5[index]"></el-input> -->
                <el-input :disabled="true" v-if="input4[index]" v-model="item.number * input4[index]"></el-input>
                <el-input :disabled="true" v-else v-model="input5"></el-input>
              </p>
              <p>
                <!-- <select :v-model="selected" placeholder="">
                  <option v-for="n in 100" :value="n" :key="n">{{ n }}</option>
                </select> -->
                <el-select v-model="selected[index]" @change="showTotal" placeholder="">
                  <el-option v-for="n in 100" :value="n" :key="n">{{ n }}</el-option>
                </el-select>
              </p>
              <!-- style="display: none;" -->
              <div style="margin-top: 5px">
                  <el-upload
                      :action="action"
                      :http-request="UploadImage"
                      :on-change="fileChange"
                      list-type="picture-card"
                      accept=".jpg,.png,.jpeg"
                      :show-file-list="false"
                      multiple
                      name="file"
                      :data="uploadData"
                      :on-preview="handlePictureCardPreview1"
                      :on-remove="handleRemove"
                    >
                    <img v-if="newUrl[index]" :src="URL + newUrl[index]" class="avatar" style="width: 50px;">
                    <p v-else style="color: #FFF; ">上传</p>
                    <!-- <i v-else class="el-icon-plus" style="width: 50px;"></i> -->
                  </el-upload>
                  <!-- <el-upload :headers = "headers" class="avatar-uploader" :action="uploadIMGURL" :data="uploadData"  :show-file-list="false" :on-success="handleAvatarSuccess" :before-upload="beforeUploade">
                    <img v-if="dialogImageUrl" :src="dialogImageUrl" class="avatar">
                    <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                  </el-upload> -->
              </div>
              <!-- <el-dialog :visible.sync="dialogVisible">
                <img width="100%" :src="dialogImageUrl" alt="" />
              </el-dialog> -->
            </div>

            <!-- <el-table
              ref="multipleTable"
              :data="goodsList"
              style="width: 100%">
              <el-table-column
                property="id"
                label="行号"
                width="70">
              </el-table-column>
              <el-table-column
                property="title"
                label="物料信息"
                width="195">
              </el-table-column>
              <el-table-column
                property="project_id"
                label="项目编号"
                width="80">
              </el-table-column>
              <el-table-column
                :property="input1"
                label="项目编号"
                width="120">
                <template>
                  <el-input v-model="input1"></el-input><br>
                元/PCS
                </template>
              </el-table-column>
              <el-table-column
                label="最小起订量"
                width="120">
                <template>
                  <el-input v-model="input2"></el-input><br>
                </template>
              </el-table-column>
              <el-table-column
                label="最小包装(必填)"
                width="120">
                <template>
                  <el-input v-model="input3"></el-input><br>
                </template>
              </el-table-column>
              <el-table-column
                label="L/T(必填)"
                width="120">
                <template>
                  <el-input v-model="input4"></el-input><br>
                </template>
              </el-table-column>
              <el-table-column
                label="未税单价"
                width="120">
                <template>
                  <el-input v-model="input5"></el-input><br>
                </template>
              </el-table-column>
              <el-table-column
                label="未税小计(元)"
                width="120">
                <template>
                  <el-select v-model="selected" placeholder="">
                    <el-option v-for="n in 100" :value="n" :key="n">{{ n }}</el-option>
                  </el-select>
                </template>
              </el-table-column>
              <el-table-column
                label="税率"
                width="120">
                <template>
                  <el-button>
                    编辑
                  </el-button>
                </template>
              </el-table-column>
            </el-table> -->

            <!-- <div class="total_price">
              <p class="price"><span>总计：</span><span>¥40000.00</span><span>（含运费：0.00）</span></p>
            </div> -->         
            <div class="total_price">
              <!-- <p class="price"><span>总计：</span><span>¥{{this.totalPrice}}</span><span>（含运费：0.00）</span></p> -->
              <p class="price"><span>总计：</span><span>¥{{this.totalPrice}}</span></p>
            </div>

            <!-- <div class="total_price">
              <p class="price" v-if="selected[index]"><span>总计：</span><span>¥{{this.totalPrice}}</span><span>（含运费：0.00）</span></p>
              <p class="price" v-else>¥{{((input4[index] * 0)/100 + input4[index]) * this.number}}</p>
            </div> -->

            <!-- <div class="trading_information">
              <h1 class="information">交易信息</h1>
              <p>交易方式：<span>担保交易</span></p>
              <p>支付方式：<span>支付宝、微信</span></p>
              <p>税务发票类型：
                <el-radio v-model="radio" label="1">增值税普通发票</el-radio>
                <el-radio v-model="radio" label="2">增值税专票(一般纳税人开具)</el-radio>
              </p>
            </div> -->
            <div class="other_instruction">
              <h1 class="instruction">其他说明</h1>
              <!-- <p>价格有效期：
                  <el-date-picker
                    v-model="value1"
                    type="daterange"
                    align="right"
                    start-placeholder="起始日期"
                    end-placeholder="结束日期"
                    default-value="2020-12-01">
                  </el-date-picker>
                  <span>（注意：采购商在价格有效期内才可以下单订购）</span>
              </p>
              <p>报价类型：&nbsp;&nbsp;&nbsp;&nbsp;<span>长期供货（价格协议）</span></p>
              <p>生产/备货周期：
                <el-input  class="el-input2" v-model="input6"></el-input>
                <span>天</span>
              </p>
              <p>交货期：<span>自下单后</span>
                <el-input  class="el-input2" v-model="input7"></el-input>
                <span>天内交货至指定地点</span>
              </p>
              <p>补充说明：
                <el-input
                  type="textarea"
                  :rows="3"
                  placeholder="Please input"
                  v-model="textarea">
                </el-input>
              </p>
              <p>报价方：&nbsp;&nbsp;&nbsp;&nbsp;<span>上海光泰包装材料有限公司</span></p>
              <p>联系方式：&nbsp;<span>1567599803</span></p>
              <p>
                <el-upload
                  class="upload-demo"
                  action="https://jsonplaceholder.typicode.com/posts/"
                  :on-change="handleChange">
                  <el-button type="primary">
                    <i class="el-icon-plus"></i>添加附件
                  </el-button>
                  <span>产品规格书、样品图等（支持.doc .docx .xls .xlsx .ppt .pptx .pdf .txt .gif .jpg .png .bmp .dwg等格式）</span>
                </el-upload>
              </p> -->
              <p v-if="ex_time">期望收货日期：
                <time-Plunge :timePlunge="ex_time" style="margin-top: -50px; margin-left: 60px;"></time-Plunge>
              </p>
              <p v-if="ex_time">报价截至日期：
                <time-Plunge :timePlunge="de_time" style="margin-top: -50px; margin-left: 60px;"></time-Plunge>
              </p>
              <p>联系人：{{projectDetail.user_name}}</p>
              <p>联系电话：{{projectDetail.mobile}}</p>
              <p>发货地：{{projectDetail.dist}}</p>
              <p>补充说明描述：{{projectDetail.notes}}</p>
              <p>供应商要求：{{projectDetail.requirements}}</p>
              <p>品质要求：{{projectDetail.quality}}</p>
            </div>
            <div class="inquiry_foot">
                <el-checkbox v-model="checked"></el-checkbox>
                <span>我已阅读并同意<a>《定制服务系统运营商城服务协议（供应商版）》</a></span>
            </div>
            <div class="inquiry_foot">
                <button @click="getOfferAdd">发表报价单</button>
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
import timePlunge from '@/components/page/time';
export default {
    name:'quotationStore',
    data (){
      return {
          loading:true,
          input: '',
          id: '',
          goods_id: [],
          project_id: [],
          number: [],
          input1: [],
          input2: [],
          input3: [],
          input4: [],
          input5: 0,
          input6: '',
          input7: '',
          options: [{
            value: 'Option1',
            label: 'Option1'
          }, {
            value: 'Option2',
            label: 'Option2'
          }],
          selected: [],
          value: '',
          radio: '1',
          value1: '',
          textarea: '',
          checked: true,
          projectDetail: [],
          ex_time: '',
          de_time: '',
          goodsList: [],
          totalPrice: 0,
          status: '',
          // listItem1: '',
          // listItem2: '',
          // listItem3: '',
          // listItem4: '',
          // listItem5: '',
          action: this.$store.state.image_api_url + "FileUpload/uploadImageToLocal/",
          uploadData: {
            sessionToken: "",
            imageToken: ""
          },
          dialogImageUrl: "",
          dialogVisible: false,
          fileList1: [],
          uploadFile: [],
          newUrl: []
      }
    },
    created(){
      setTimeout(() => {
        this.loading = false;
      }, 300);
      this.getProjectDetail();
    },
    methods:{
      handleChange(file, fileList) {
        this.fileList = fileList.slice(-3);
      },
      getProjectDetail() {
        this.$HTTP(this.$httpConfig.projectDetail, {
          id: this.$route.params.id
        })
        .then(res => {
          this.projectDetail = res.data.data;
          this.id = this.projectDetail.id;
          this.ex_time = this.projectDetail.expect_time;
          this.de_time = this.projectDetail.deadline_time;
          this.goodsList = res.data.data.goods;
          for (var a in this.goodsList) {
          this.goods_id.push(this.goodsList[a].goods_id);
          this.project_id.push(this.goodsList[a].project_id);
          this.number.push(this.goodsList[a].number);
          }
        })
        .catch(err => {
          console.log(err);
        });
      },
      showTotal() {
        // for(var i = 0; i < this.input4.length; i++) {
        //   if(this.input4) {
        //     this.sum += ((this.input4[i] * this.selected[i])/100 + this.input4[i]) * this.number[i]
        //   }
        //   else {
        //     this.sum = 0
        //   }
        // }
        var inp4 = this.input4;
        inp4 = inp4.map(Number);

        var sele = this.selected;
        var result = inp4.map((a,b) => a * sele[b])

        var divide = result.map((g) => g/100)

        var sum = divide.map((c,d) => c + inp4[d])

        var num = this.number;
        var multi = sum.map((e,f) => e * num[f])

        var total = 0;
        for (var i = 0; i < multi.length; i++) {
          if(!isNaN(multi[i])){
            total += multi[i]
          }
        }
        this.totalPrice = total.toFixed(2);
      },
      getOfferAdd() {
        var arr = this.input4;
        arr = arr.map(Number);

        var arr1 = this.number;
        var result = arr.map((v,i) => v * arr1[i])

        this.$HTTP(this.$httpConfig.offerAdd, {
          id: this.id,
          goods_id: this.goods_id,
          project_id: this.project_id,
          number: this.number,
          minimum: this.input1,
          packaging: this.input2,
          lt: this.input3,
          unit_price: this.input4,
          unit_subtotal: result,
          tax_rate: this.selected,
          pic_url: this.newUrl,
        })
        .then(res => {
          this.status = res.data.status;
          if(this.status == 1) {
            this.$router.push({
                path: "/inquiryPurchase"
            });
          }
        })
        .catch(err => {
          console.log(err);
        });
      },
      UploadImage(param) {
        this.$HTTP(this.$httpConfig.getGoodsImgCofig, {}, "post")
        .then(res => {
          let data = res.data.data;
          this.imageConf = data.config;
          // this.imageToken = data.token;
          // this.sToken = data.s_token;
          // this.uploadData.sessionToken = data.s_token;
          // this.uploadData.imageToken = data.token;
          const isLt2M = param.file.size / 1024 / 1024 < 3;
          if (!isLt2M) {
            this.$layer.msg("上传头像图片大小不能超过 2MB!");
            return;
          }

          var formData = new FormData();
          formData.append("file", param.file);
          formData.append("imageToken", data.token);
          formData.append("sessionToken", data.s_token);
          this.axios.post(this.$store.state.image_api_url + "FileUpload/uploadImageToLocal/", formData)
          .then(res => {
              if (res.data.status == 0 || res.data.code == 0) {
                  this.$message({
                    duration: 1000,
                    type: "error",
                    message: res.data.message
                  });
                  this.fileList1.splice(this.fileList1.length - 1);
              } else {
                  this.newUrl.push(res.data.data);
                  this.fileList1[this.fileList1.length - 1].url = this.URL + res.data.data;
                  this.uploadFile.push(res.data.data);
              }
          });
          }).catch(res => {
            let data = res.data.data;
            this.$layer.msg(data.token);
          });
      },
      fileChange(file) {
        console.log("fileChange");
        this.fileList1.push({ name: file.name, url: file.url });
      },
      handlePictureCardPreview1(url) {
        this.dialogImageUrl = url;
        this.dialogVisible = true;
      },
      handleRemove(file, index) {
        this.uploadFile.splice(index, 1);
        this.fileList1.splice(index, 1);
      },
    },
    components: {
      headerTop,
      MerchantFoot,
      timePlunge
    }
            
}
</script>

<style lang="less">
.el-upload--picture-card {
    background-color: #1A6DF8;
    border: 1px dashed #c0ccda;
    border-radius: 6px;
    box-sizing: border-box;
    width: 45px;
    height: 35px;
    line-height: 146px;
    vertical-align: top;
}
.el-upload__input {
  display: none !important;
}
</style>

<style lang="less" scoped>
.el-input-group {
    line-height: normal;
    display: inline-table;
    width: 22%;
    border-collapse: separate;
    border-spacing: 0;
}
.el-input1 {
  width: 22% !important;
}
.el-input {
    width: 80px;
}
.el-select {
    width: 80px;
}
.el-radio {
    color: #333;
    cursor: pointer;
    margin-right: 50px;
}
.el-input2 {
  width: 15% !important;
}
.el-textarea {
    position: relative;
    display: inline-block;
    width: 60%;
    vertical-align: bottom;
    font-size: 14px;
}
.el-icon-plus {
    padding-right: 10px;
}
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
        .quotation_store {
          // padding: 20px 20px;
          padding: 18px 0 18px 18px;
          .quo_head {
              padding-bottom: 20px;
              .commodity {
                  font-size: 12px;
                  color: #333;
                  span {
                      color: #D02629;
                  }
              }
          }
          .quilt_box {
            // width: 1187px;
            background: #fff;
            padding: 20px;
            .inquirer {
              padding-bottom: 10px;
              p {
                font-size: 14px;
                color: #333;
                line-height: 40px;
              }
              p:nth-of-type(2) {
                float: right;
                margin-top: -40px;
                span {
                  color: #1A6DF8;
                }
              }
            }
            .quo_information {
              font-size: 24px;
              color: #1A6DF8;
              padding: 20px 0;
              span {
                font-size: 14px;
                color: #666;
              }
            }
            .total_search {
              padding: 10px 0;
              display: flex;
              p {
                  font-size: 14px;
                  color: #464746;
                  padding-top: 5px;
                  span {
                    color: #1A6DF8;
                  }
              }
              p:nth-of-type(1) {
                  padding-right: 20px;
              }
            }
            .col_head {
                    // padding: 20px;
                    padding: 15px;
                    background: #F8F8F8;
                    display: flex;
                    margin-top: 20px;
                    p {
                        color: #000;
                        font-size: 13px;
                    }
                    p:nth-of-type(2) {
                        // padding: 0 110px 0 80px;
                        padding: 0 70px 0 50px;
                    }
                    p:nth-of-type(4) {
                        // padding: 0 35px 0 20px;
                        padding: 0 20px 0 10px;
                    }
                    p:nth-of-type(6) {
                        // padding: 0 42px 0 45px;
                        padding: 0 25px;
                    }
                    p:nth-of-type(8) {
                        // padding: 0 50px 0 65px;
                        padding: 0 40px;
                    }
                    p:nth-of-type(10) {
                        // padding: 0 75px 0 65px;
                        padding: 0 55px 0 45px;
                    }
                }
                .col_head1 {
                  // padding: 20px;
                  padding: 15px;
                  display: flex;
                  border-bottom: 1px solid #EEEEEE;
                  p {
                      color: #333;
                      font-size: 13px;
                      line-height: 25px;
                  }
                  // input {
                  //   -webkit-appearance: none;
                  //   background-color: #FFF;
                  //   background-image: none;
                  //   border-radius: 4px;
                  //   border: 1px solid #DCDFE6;
                  //   border-top-color: rgb(220, 223, 230);
                  //     border-right-color: rgb(220, 223, 230);
                  //     border-bottom-color: rgb(220, 223, 230);
                  //     border-left-color: rgb(220, 223, 230);
                  //   -webkit-box-sizing: border-box;
                  //   box-sizing: border-box;
                  //   color: #606266;
                  //   display: inline-block;
                  //   font-size: inherit;
                  //   height: 40px;
                  //   line-height: 40px;
                  //   outline: 0;
                  //   padding: 0 15px;
                  //   -webkit-transition: border-color .2s cubic-bezier(.645,.045,.355,1);
                  //   transition: border-color .2s cubic-bezier(.645,.045,.355,1);
                  //   width: 80px;
                  // }
                  // select {
                  //   background-color: #FFF;
                  //   background-image: none;
                  //   border-radius: 4px;
                  //   border: 1px solid #DCDFE6;
                  //     border-top-color: rgb(220, 223, 230);
                  //     border-right-color: rgb(220, 223, 230);
                  //     border-bottom-color: rgb(220, 223, 230);
                  //     border-left-color: rgb(220, 223, 230);
                  //   -webkit-box-sizing: border-box;
                  //   box-sizing: border-box;
                  //   color: #606266;
                  //   display: inline-block;
                  //   font-size: inherit;
                  //   height: 40px;
                  //   line-height: 40px;
                  //   outline: 0;
                  //   padding: 0 15px;
                  //   -webkit-transition: border-color .2s cubic-bezier(.645,.045,.355,1);
                  //   transition: border-color .2s cubic-bezier(.645,.045,.355,1);
                  //   width: 80px;
                  //   text-align: center;
                  // }
                  p:nth-of-type(1) {
                      width: 30px;
                      padding-left: 6px;
                      padding-top: 2px;
                      // color: #fff;
                  }
                  p:nth-of-type(2) {
                      // width: 230px;
                      width: 150px;
                      padding: 0 20px;
                  }
                  p:nth-of-type(3) {
                      width: 20px;
                  }
                  p:nth-of-type(4) {
                      // padding: 0 40px 0 50px;
                      padding: 0 15px 0 30px;
                      width: 20px;
                  }
                  p:nth-of-type(6) {
                      // padding: 0 35px;
                      padding: 0 18px;
                  }
                  p:nth-of-type(8) {
                      // padding: 0 35px;
                      padding: 0 18px;
                  }
                  p:nth-of-type(10) {
                      // padding: 0 35px;
                      padding: 0 18px;
                  }
                  p:nth-of-type(11) {
                      height: 30px;
                      background: #01B4EE;
                      color: #fff;
                      border-radius: 3px;
                      // padding: 5px 15px;
                      padding: 5px 10px;
                      cursor: pointer;
                  }
              }
              .total_price {
                padding: 20px 0;
                .price {
                  float: right;
                  span:nth-of-type(1) {
                    font-size: 14px;
                    color: #D02629;
                  }
                  span:nth-of-type(2) {
                    font-size: 18px;
                    color: #D02629;
                  }
                  span:nth-of-type(3) {
                    font-size: 14px;
                    color: #333333;
                  }
                }
              }
              // .trading_information {
              //   padding: 20px 0;
              //   .information {
              //     font-size: 24px;
              //     color: #1A6DF8;
              //     padding-bottom: 20px;
              //   }
              //   p {
              //     font-size: 14px;
              //     color: #333;
              //     padding: 30px 0 0 40px;
              //   }
              // }
              .other_instruction {
                padding: 20px 0 30px 0;
                .instruction {
                  font-size: 24px;
                  color: #1A6DF8;
                  padding-bottom: 20px;
                }
                p {
                  font-size: 14px;
                  color: #333;
                  padding: 30px 0 0 40px;
                }
                p:nth-of-type(1) {
                  span {
                    padding-left: 10px;
                  }
                }
                 p:nth-of-type(3) {
                  span {
                    padding-left: 10px;
                  }
                }
                p:nth-of-type(4) {
                  span:nth-of-type(1) {
                    padding-right: 10px;
                  }
                  span:nth-of-type(2) {
                    padding-left: 10px;
                  }
                }
                p:nth-of-type(8) {
                  // padding-left: 115px;
                  span {
                    color: #666666;
                    padding-left: 10px;
                  }
                }
              }
              .inquiry_foot {
                padding: 10px 115px;
                span {
                    font-size: 14px;
                    margin-left: 20px;
                    color: #333;
                    a {
                        color: #1A6DF7;
                    }
                }
                button {
                    background: #D02629;
                    color: #fff;
                    font-size: 14px;
                    width: 100px;
                    height: 38px;
                    border-radius: 3px;
                    border: none;
                }
            }
          }
        }
      }
   }
</style>