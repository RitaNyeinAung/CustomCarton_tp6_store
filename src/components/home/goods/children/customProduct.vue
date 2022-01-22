<template>
  <div class="customProduct">
    <div class="g_att">
      <span class="att_details">商品详情</span>
      <el-tabs type="card" @tab-click="handleClick" v-model="changeTab">
        <el-tab-pane name="通用信息" label="通用信息">
          <div class="customize_details">
            <p>
              <span>*</span>商品名称：
              <el-input v-model="title"></el-input>
            </p>
            <p>请输入商品名,不能超过60个字符</p>
            <p>
              <span>*</span>最低数量：
              <el-input v-model="number" oninput="this.value = this.value.replace(/[^0-9.]/g, '').replace(/(\..*)\./g, '$1');"></el-input>
            </p>
            <p>
              <span>*</span>商品分类：
              <el-select @change="sendIdToSecondData" v-model="value" placeholder="">
                <el-option
                  v-for="item in firstData"
                  :key="item.value"
                  :label="item.class_name"
                  :value="item.id">
                </el-option>
              </el-select>
              <el-select @change="sendIdToThirdData" v-model="value1" placeholder="">
                <el-option
                  v-for="item in secondData"
                  :key="item.value"
                  :label="item.class_name"
                  :value="item.id">
                </el-option>
              </el-select>
              <el-select @change="sendIdToSpecInfo" v-model="value2" placeholder="">
                <el-option
                  v-for="item in thirdData"
                  :key="item.value"
                  :label="item.class_name"
                  :value="item.id">
                </el-option>
              </el-select>
            </p>
            <p>
              <!-- 数码印刷&nbsp;&nbsp;模板 -->
            </p>

            <p style="padding-top: 15px; padding-bottom: 5px; ">
              <span>*</span>模板: 
              <el-select class="el-select1" @change="getcustomTemplateDetail" v-model="value3" placeholder="">
                <el-option
                  v-for="item in templateList"
                  :key="item.value"
                  :label="item.name"
                  :value="item.id">
                </el-option>
              </el-select>
            </p>
            <!-- <p>制造尺寸</p> -->
            <p></p>

            <div v-for="(item, index) in templateDetail" :key="index" style="display: flex; ">
              <p class="leftp" style=""><span>*</span>{{item.name}}：</p>
              <div class="rightinput">
                  <el-input style="display: none;" v-model="checkInputID[index]" disabled></el-input>
                  <div class="add_input" v-for="(find0, ind) in item.value" :key="ind">
                    <el-input :style="(item.type == 'long' || item.type == 'wide' || item.type == 'high' || item.type == 'chief' || item.type == 'width' || item.type == 'thick') ? 'display: none' : '' " class="loopinput" v-model="find0.value" placeholder="规格参数"></el-input>
                    <el-input :style="(item.type == 'long' || item.type == 'wide' || item.type == 'high' || item.type == 'chief' || item.type == 'width') ? 'display: none' : '' " :class="(item.type == 'thick') ? 'loopinputprice1' : 'loopinputprice'" v-model="find0.price" placeholder="价格"></el-input>
                  </div>
                  <img @click="addInputMethod(checkInputID[index])" src="../../../../assets/yi-19.png" :style="(item.type == 'long' || item.type == 'wide' || item.type == 'high' || item.type == 'chief' || item.type == 'width' || item.type == 'thick') ? 'display: none; padding-left: 12px;' : 'padding-left: 12px;' " />
              </div>
            </div>
            <button @click="addCustomInfo" class="next_step">确认提交</button>
          </div>
        </el-tab-pane>
        <el-tab-pane name="商品相册" label="商品相册">
          <div class="photo_frame">
            <div class="img-list">
              <div
                class="img-content"
                v-for="(item, key) in fileList"
                :key="key"
              >
                <img :src="item.url" />
                <!-- 放大icon -->
                <div class="layer">
                    <i
                        class="el-icon-zoom-in"
                        @click="handlePictureCardPreview1(item.url)"
                    ></i>
                    <i
                        @click="handleRemove(item, key)"
                        class="el-icon-delete"
                    ></i>
                </div>
              </div>
              <div style="margin-top: 5px">
                <el-upload
                  class="img_up"
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
                >
                  <i class="el-icon-plus"></i>
                </el-upload>
              </div>
            </div>
          </div>
          <el-dialog :visible.sync="dialogVisible">
            <img width="100%" :src="dialogImageUrl" alt="">
          </el-dialog>
          <p style="height: 60px; width: 1000px; background: #fff; position: absolute;"></p>
          <button @click="addPicture" class="confirm_submit">确认提交</button>
        </el-tab-pane>
      </el-tabs>
    </div>
  </div>
</template>
<script>
export default {
  name: "customProduct",
  data() {
    return {
      activeName: 'first',
      title: '',
      number: 1,
      value: '',
      value1: '',
      value2: '',
      value3: '',
      firstData: '',
      secondData: '',
      thirdData: '',
      templateList: '',
      specInfo: '',
      templateDetail: [],
      nameArr: [],
      checkInputArr: [],
      checkInputArrPr: [],
      checkInputID: [],
      dialogImageUrl: '',
      dialogVisible: false,
      disabled: false,
      changeTab: '通用信息',
      fileList: [],
      action:  this.$store.state.image_api_url + "FileUpload/uploadImageToLocal/",
      uploadData: {
        sessionToken: "",
        imageToken: ""
      },
      uploadFile: [],
      nameValue: [],
      goodsId: 0,
      fileData: {}
    };
  },
  created() {
    this.getData();
      this.getCustomTemplateList();
  },
  methods: {
    addParameter(name) {
      this.nameArr.push({ "name": name })
    },
    addInputMethod(val) {
        let tempArr = [...this.templateDetail]
        tempArr.forEach((item, data) => {
            if(item.id == val) {
                this.templateDetail[data].value.push({ value: '', price: '' });
                // this.nameValue = this.templateDetail[data].value
                return;
            }
        })
        let sss = [...this.templateDetail]
        this.templateDetail = []
        this.templateDetail = sss
        
    },
    handleClick(tab, event) {
    },
    getData() {
        this.$HTTP(this.$httpConfig.getClassById, {
          goods_class_id: 0
        })
        .then(res => {
          this.firstData = res.data.data;
        })
        .catch(err => {
          console.log(err);
        });
    },
    sendIdToSecondData(id) {
      this.$HTTP(this.$httpConfig.getClassById, {
          goods_class_id: id
        })
        .then(res => {
          this.secondData = res.data.data;
        })
        .catch(err => {
          console.log(err);
        });
    },
    sendIdToThirdData(id1) {
      this.$HTTP(this.$httpConfig.getClassById, {
          goods_class_id: id1
        })
        .then(res => {
          this.thirdData = res.data.data;
        })
        .catch(err => {
          console.log(err);
        });
    },
    getCustomTemplateList() {
        this.$HTTP(this.$httpConfig.customTemplateList, {}, "post")
        .then(res => {
            this.templateList = res.data.data;
        })
        .catch(err => {
            console.log(err)
        });
    },
    sendIdToSpecInfo(id2) {
        this.$HTTP(this.$httpConfig.getGoodsSpecInfo, {
          id: id2
        }, "post")
        .then(res => {
            this.specInfo = res.data.data;
        })
        .catch(err => {
            console.log(err)
        });
    },
    getcustomTemplateDetail(id3) {
        this.$HTTP(this.$httpConfig.customTemplateDetail, {
          id: id3
        }, "post")
        .then(res => {
            if (res.data.status == 0) {
              this.nameArr = []
              this.checkInputID = []
              this.nameArr = []
              this.$message({
                duration: 1000,
                type: "error",
                message: res.data.message
              });
            }
            this.templateDetail = res.data.data;
            let tempLen  = this.templateDetail.length
            this.nameArr = []
            this.checkInputID = []
            for(let i = 0; i < tempLen; i++) {
                this.checkInputID.push(this.templateDetail[i].id)
                this.templateDetail[i]['value'] = [{ value: '', price: '' }]
                this.nameValue = this.templateDetail[i].value
            }
            this.nameArr = this.templateDetail
        })
        .catch(err => {
          this.nameArr = []
            this.checkInputID = []
            this.nameArr = []
            this.$message({
                duration: 1000,
                type: "error",
                message: err.data.message
            });
            console.log(err)
        });
    },
    addCustomInfo() {
      let tempLen  = this.templateDetail.length
      let valueInput = []
      let priceInput = []
      for(let i = 0; i < tempLen; i++) {
          valueInput.push([{value: ''}])
          priceInput.push([{price: ''}])
          let len = this.templateDetail[i].value
          for(let j = 0; j < len.length; j++) {
              if(len[j].value !== null && len[j].value !== "") {
                  let tempval = len[j].value
                  valueInput[i][j] = tempval
              } else if(this.templateDetail[i].type == 'long' || this.templateDetail[i].type == 'wide' || this.templateDetail[i].type == 'high' || 
                this.templateDetail[i].type == 'chief' || this.templateDetail[i].type == 'width' || this.templateDetail[i].type == 'price') {
                  valueInput[i][j] = "mm"
              } else {
                  valueInput[i][j] = ""
              }
              if(len[j].price !== null && len[j].price !== "") {
                  let tempprice = len[j].price
                  priceInput[i][j] = tempprice
                  
              } else {
                  priceInput[i][j] = ""
              }
          }
      }
      var data = {
          id: this.checkInputID,
          value: valueInput,
          price: priceInput//this.checkInputArrPr
      }
      this.$HTTP(this.$httpConfig.addCustomInfo, {
        title: this.title,
        number:this.number,
        class_one: this.value,
        class_two: this.value1,
        class_three: this.value2,
        template_id: this.value3,
        space: data
      }, "post")
      .then(res => {
        if(res.data.status == 1) {
          this.$message.success(res.data.message);
          this.goodsId = res.data.data;
          this.changeTab = '商品相册';
        }
      })
      .catch(err => {
          console.log(err)
      });
    },
    UploadImage(param) {
      this.$HTTP(this.$httpConfig.getGoodsImgCofig, {}, "post")
      .then(res => {
        let data = res.data.data;
        this.imageConf = data.config;
        const isLt2M = param.file.size / 1024 / 1024 < 3;
        if (!isLt2M) {
            this.$layer.msg("上传头像图片大小不能超过 2MB!");
            return;
        }

        var formData = new FormData();
        formData.append("file", param.file);
        formData.append("imageToken", data.token);
        formData.append("sessionToken", data.s_token);
        this.axios
          .post(
            this.$store.state.image_api_url +
                "FileUpload/uploadImageToLocal//",
            formData
          )
          .then(res => {
            if (res.data.status == 0) {
                this.$message({
                    duration: 1000,
                    type: "error",
                    message: res.data.message
                });
                this.fileList.splice(this.fileList.length - 1);
            } else {
                this.newUrl = res.data.data;
                this.fileList.push(this.fileData)
                this.fileList[this.fileList.length - 1].url =
                    this.URL + res.data.data;
                this.uploadFile.push(res.data.data);
            }
            if (res.data.code == 0) {
              this.$message({
                  duration: 2000,
                  type: "error",
                  message: res.data.message
              });
              this.fileList.splice(this.fileList.length - 1);
            }
          });
      })
      .catch(res => {
          let data = res.data.data;
          this.$layer.msg(data.token);
      });
    },
    difficulty() {
      return this.$httpConfig.upLoadImage;
    },
    fileChange(file) {
      // this.fileList.push({ name: file.name, url: file.url });
      this.fileData = { name: file.name, url: file.url }
    },
    handlePictureCardPreview1(url) {
      this.dialogImageUrl = url;
      this.dialogVisible = true;
    },
    handleRemove(file, index) {
      this.uploadFile.splice(index, 1);
      this.fileList.splice(index, 1);
    },
    addPicture() {
			this.$HTTP(this.$httpConfig.addGoodsPic, { 
        pic_url: this.uploadFile,
        goods_id: this.goodsId
        }, 'post').then(function (res) {
				this.$message.success(res.data.message);
			});
		}
  }
}
</script>

<style lang="less">
.img_up {
  .el-upload--picture-card {
    background-color: #fbfdff;
    border: 1px dashed #c0ccda;
    border-radius: 6px;
    box-sizing: border-box;
    width: 148px;
    height: 148px;
    line-height: 146px;
    vertical-align: top;
  }
  .el-upload__input {
    display: none !important;
  }
}
.el-tabs__nav-scroll {
    padding-left: 200px;
}
.el-tabs__item {
    padding: 0 20px;
    height: 40px;
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
    line-height: 40px;
    display: inline-block;
    list-style: none;
    font-size: 14px;
    font-weight: 500;
    color: #303133;
    position: relative;
    background: #EDEDED;
}
.el-tabs__item.is-active {
    color: #F7BC0A;
    background: #fff;
}
.el-tabs__item:hover {
    color: #F7BC0A;
    cursor: pointer;
}
</style>

<style lang="less" scoped>
.el-input {
    position: relative;
    font-size: 14px;
    display: inline-block;
    width: 26%;
    padding-left: 19px;
    padding-bottom: 10px;

}
.loopinput {
    position: relative;
    font-size: 14px;
    display: inline-block;
    width: 9rem;
    padding-left: 12px;
}
.loopinputprice {
    position: relative;
    font-size: 14px;
    display: inline-block;
    width: 6rem;
    padding-left: 5px;
}
.loopinputprice1 {
    position: relative;
    font-size: 14px;
    display: inline-block;
    width: 6rem;
    padding-left: 12px;
}
// .el-input1 {
//     position: relative;
//     font-size: 14px;
//     display: inline-block;
//     width: 18%;
//     padding-left: 20px;
// }
// .el-input2 {
//     position: relative;
//     font-size: 14px;
//     display: inline-block;
//     width: 28.2%;
//     padding-left: 20px;
// }
// .el-input3 {
//     position: relative;
//     font-size: 14px;
//     display: inline-block;
//     width: 19.6%;
//     padding-left: 20px;
// }
.el-input4 {
    position: relative;
    font-size: 14px;
    display: inline-block;
    width: 28.2%;
    padding-left: 20px;
    margin-top: 10px;
}
.el-select {
    display: inline-block;
    position: relative;
    padding-left: 20px;
    width: 26%;
}
.el-select1 {
    display: inline-block;
    position: relative;
    padding-left: 28px;
    width: 26.7%;
}
.customProduct {
  width: 1000px;
  padding-bottom: 80px;
  .g_att {
    .att_details {
      color: #333;
      float: left;
      font-size: 16px;
      padding-top: 10px;
    }
    .customize_details {
      padding: 40px;
      .leftp {
        width: 10%; 
        text-align: end; 
        margin-left: -22px; 
      }
      .rightinput {
        display: flex; 
        align-items: center; 
        flex-wrap: wrap; 
        width: 90%;
      }
      p {
        font-size: 12px;
        color: #666666;
        line-height: 50px;
        span {
          color: #FF0000;
          // padding-right: 5px;
        }
        img {
          width: 22px;
          height: 22px;
          margin: 14px 10px;
        }
      }
      .add_input {
        // margin-left: 74px;
        margin-left: 7px;
        margin-right: 1rem;
      }
      p:nth-of-type(2) {
        color: #999999;
        padding-left: 94px;
        margin-top: -15px;
      }
      p:nth-of-type(5) {
        color: #999999;
        padding-left: 94px;
        margin-top: -15px;
      }
      p:nth-of-type(6) {
        padding-left: 25px;
      }
      // p:nth-of-type(6) {
      //   color: #999999;
      //   padding-left: 94px;
      //   margin-top: -15px;
      // }
      // p:nth-of-type(9) {
      //   color: #999999;
      //   padding-left: 94px;
      //   margin-top: -15px;
      // }
      // p:nth-of-type(11) {
      //   color: #999999;
      //   padding-left: 94px;
      //   margin-top: -15px;
      // }
      // p:nth-of-type(13) {
      //   color: #999999;
      //   padding-left: 94px;
      //   margin-top: -15px;
      // }
      // .show_data {
      //   padding-left: 74px;
      //   .data_form {
      //     font-size: 12px;
      //     color: #666666;
      //     line-height: 50px;
      //     span {
      //       color: #FF0000;
      //       padding-right: 5px;
      //     }
      //     img {
      //       width: 22px;
      //       height: 22px;
      //       margin: 14px 10px;
      //     }
      //   }
      // }
      .show_data1 {
        padding-left: 74px;
        .data_form1 {
          font-size: 12px;
          color: #666666;
          line-height: 50px;
          span {
            color: #FF0000;
            padding-right: 5px;
          }
          img {
            width: 22px;
            height: 22px;
            margin: 14px 10px;
          }
        }
        .data_text1 {
          color: #999999;
          padding-left: 20px;
          margin-top: -15px;
        }
      }
      // .show_data2 {
      //   padding-left: 74px;
      //   .data_form2 {
      //     font-size: 12px;
      //     color: #666666;
      //     line-height: 50px;
      //     span {
      //       color: #FF0000;
      //       padding-right: 5px;
      //     }
      //     img {
      //       width: 22px;
      //       height: 22px;
      //       margin: 14px 10px;
      //     }
      //   }
      //   .data_text2 {
      //     color: #999999;
      //     padding-left: 20px;
      //     margin-top: -15px;
      //   }
      // }
    }
    .next_step {
      margin: 60px 0 0 94px;
      padding: 12px 100px;
      background: #F7BC0A;
      border: none;
      font-size: 14px;
      color: #fff;
      border-radius: 5px;
    }
    .confirm_submit {
      margin-top: 80px;
      padding: 12px 100px;
      background: #F7BC0A;
      border: none;
      font-size: 14px;
      color: #fff;
      border-radius: 5px;
    }
    .photo_frame {
      height: 150px;
      padding: 30px;
      border: 1px solid #DDDDDD;
      .img-list {
        overflow: hidden;
        width: 100%;
      }

      .img-list .img-content {
        float: left;
        position: relative;
        display: inline-block;
        width: 148px;
        height: 148px;
        margin: 5px 20px 20px 0;
        border: 1px solid #d1dbe5;
        border-radius: 4px;
        transition: all 0.3s;
        box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.12), 0 0 6px 0 rgba(0, 0, 0, 0.04);
        .active {
          border: 3px solid #ff0000;
        }
      }

      .img-list .img-content img {
        display: block;
        width: 100%;
        height: 100%;
        margin: 0 auto;
        border-radius: 4px;
      }

      .img-list .img-content .name {
        margin-top: 10px;
      }

      .img-list .img-content .name > div {
        width: 90%;
        text-overflow: ellipsis;
        overflow: hidden;
        height: 25px;
        line-height: 25px;
      }

      .img-list .img-content:hover .del,
      .img-list .img-content:hover .layer {
        opacity: 1;
      }

      .img-list .img-content .del,
      .img-list .img-content .layer {
        opacity: 0;
        transition: all 0.3s;
      }

      .img-list .img-content .del {
        position: absolute;
        bottom: 10px;
        right: 10px;
        color: #8492a6;
        cursor: pointer;
        font-size: 1.1em;
      }

      .img-list .img-content .layer {
        position: absolute;
        left: 0;
        right: 0;
        top: 0;
        height: 148px;
        color: #fff;
        text-align: center;
        z-index: 5;
        background-color: rgba(0, 0, 0, 0.4);
      }

      .img-list .img-content .layer i {
        font-size: 1.6em;
        margin-top: 60px;
        margin-left: 0.3rem;
      }
    }
  }
}
</style>