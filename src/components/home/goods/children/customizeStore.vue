<template>
  <div class="customize_store">
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

            <!-- <p>
              <span>*</span>尺寸类型：
              <el-input v-model="input1" placeholder="制造尺寸"></el-input>
              <img @click="addInputBox" src="../../../../assets/yi-19.png" />
            </p> -->
             <!-- <p v-for="(item, index) in templateDetail" :key="index">
              <span>*</span>{{item.name}}：
              <el-input style="display: none;" v-model="checkId" disabled></el-input>
              <input :type="item.type" v-model="checkValue" placeholder="制造尺寸" />
            </p> -->

            <div v-for="(item, index) in templateDetail" :key="index" style="display: flex; ">
              <p class="leftp" style=""><span>*</span>{{item.name}}：</p>
              <div class="rightinput">
                  <el-input style="display: none;" v-model="checkInputID[index]" disabled></el-input>
                  <div class="add_input" v-for="(find0, ind) in item.value" :key="ind">
                    <el-input class="loopinput" v-model="find0.value" placeholder="规格参数"></el-input>
                    <el-input class="loopinputprice" v-model="find0.price" placeholder="价格"></el-input>
                  </div>
                  <img @click="addInputMethod(checkInputID[index])" src="../../../../assets/yi-19.png" style="padding-left: 12px; " />
              </div>
            </div>

            <!-- <p v-if="this.templateDetail[0]" id="references13">
              <el-input style="display: none;" v-model="checkId0" disabled></el-input>
              <el-input v-model="checkValue0" placeholder="制造尺寸"></el-input>
              <img @click="addReference13" src="../../../../assets/yi-19.png" />
            </p> -->
            <!-- <div class="show_data" v-show="showData">
              <p class="data_form">
                <el-input class="el-input2" v-model="input21" placeholder="制造尺寸"></el-input>
                <img @click="addInputBox1" src="../../../../assets/yi-19.png" />
              </p>
            </div> -->

            <!-- <p id="references2">
              <span>*</span>纸箱尺寸：
              <el-input  v-model="references20" placeholder="长 cm" type="text"></el-input>
              <el-input  v-model="references21" placeholder="宽 cm" type="text"></el-input>
              <el-input  v-model="references22" placeholder="高 cm" type="text"></el-input>
              <img @click="addReference2" src="../../../../assets/yi-19.png" />
            </p> -->

            <!-- <p id="references2">
              <span>*</span>纸箱尺寸：
              <el-input v-model="input2" placeholder="长 cm"></el-input>
              <el-input v-model="input3" placeholder="宽 cm"></el-input>
              <el-input v-model="input4" placeholder="高 cm"></el-input>
              <img @click="addInputBox3" src="../../../../assets/yi-19.png" />
            </p> -->
            <!-- <p>非承压</p> -->
            <!-- <p></p>
            <div class="show_data1" v-show="showData3">
              <p class="data_form1">
                <el-input class="el-input2" v-model="input24" placeholder="长 cm"></el-input>
                <el-input class="el-input2" v-model="input25" placeholder="宽 cm"></el-input>
                <el-input class="el-input2" v-model="input26" placeholder="高 cm"></el-input>
                <img @click="addInputBox4" src="../../../../assets/yi-19.png" />
              </p> -->
              <!-- <p class="data_text1">非承压</p> -->
            <!-- </div>
            <div class="show_data1" v-show="showData4">
              <p class="data_form1">
                <el-input class="el-input2" v-model="input27" placeholder="长 cm"></el-input>
                <el-input class="el-input2" v-model="input28" placeholder="宽 cm"></el-input>
                <el-input class="el-input2" v-model="input29" placeholder="高 cm"></el-input>
                <img @click="addInputBox5" src="../../../../assets/yi-19.png" />
              </p> -->
              <!-- <p class="data_text1">非承压</p> -->
            <!-- </div>
            <div class="show_data1" v-show="showData5">
              <p class="data_form1">
                <el-input class="el-input2" v-model="input30" placeholder="长 cm"></el-input>
                <el-input class="el-input2" v-model="input31" placeholder="宽 cm"></el-input>
                <el-input class="el-input2" v-model="input32" placeholder="高 cm"></el-input>
              </p> -->
              <!-- <p class="data_text1">非承压</p> -->
            <!-- </div> -->

            <!-- <p>
              <span>*</span>物理特性：
              <el-input v-model="input5" placeholder="内装重量 1<x<50 kg"></el-input>
              <el-input v-model="input6" placeholder="仓储叠放 1<x<20 层"></el-input>
            </p> -->
            <!-- <p>正常</p> -->
            <!-- <p></p> -->

            <!-- <p id="references3">
              <span>*</span>产品承压：
              <el-input class="el-input1" v-model="references3" placeholder="非承压" type="text"></el-input>
              <img @click="addReference3" src="../../../../assets/yi-19.png" />
            </p>
            <p></p> -->

            <!-- <p>
              <span>*</span>产品承压：
              <el-input class="el-input1" v-model="input7" placeholder="非承压"></el-input>
              <img @click="addInputBox6" src="../../../../assets/yi-19.png" />
            </p> -->
            <!-- <p>一页成型</p> -->
            <!-- <p></p> -->
            <!-- <div class="show_data2" v-show="showData6">
              <p class="data_form2">
                <el-input class="el-input3" v-model="input33" placeholder="非承压"></el-input>
                <img @click="addInputBox7" src="../../../../assets/yi-19.png" />
              </p> -->
              <!-- <p class="data_text2">一页成型</p> -->
            <!-- </div>
            <div class="show_data2" v-show="showData7">
              <p class="data_form2">
                <el-input class="el-input3" v-model="input34" placeholder="非承压"></el-input>
                <img @click="addInputBox8" src="../../../../assets/yi-19.png" />
              </p> -->
              <!-- <p class="data_text2">一页成型</p> -->
            <!-- </div>
            <div class="show_data2" v-show="showData8">
              <p class="data_form2">
                <el-input class="el-input3" v-model="input35" placeholder="非承压"></el-input>
              </p> -->
              <!-- <p class="data_text2">一页成型</p> -->
            <!-- </div> -->

            <!-- <p id="references4">
              <span>*</span>存储环境：
              <el-input v-model="references4" placeholder="正常" type="text"></el-input>
              <img @click="addReference4" src="../../../../assets/yi-19.png" />
            </p> -->

            <!-- <p>
              <span>*</span>存储环境：
              <el-input v-model="input8" placeholder="正常"></el-input>
              <img @click="addInputBox9" src="../../../../assets/yi-19.png" />
            </p> -->
            <!-- <div class="show_data" v-show="showData9">
              <p class="data_form">
                <el-input class="el-input2" v-model="input36" placeholder="正常"></el-input>
                <img @click="addInputBox10" src="../../../../assets/yi-19.png" />
              </p>
            </div>
            <div class="show_data" v-show="showData10">
              <p class="data_form">
                <el-input class="el-input2" v-model="input37" placeholder="正常"></el-input>
                <img @click="addInputBox11" src="../../../../assets/yi-19.png" />
              </p>
            </div>
            <div class="show_data" v-show="showData11">
              <p class="data_form">
                <el-input class="el-input2" v-model="input38" placeholder="正常"></el-input>
              </p>
            </div> -->

            <!-- <p id="references5">
              <span>*</span>成型方式：
              <el-input v-model="references5" placeholder="一页成型" type="text"></el-input>
              <img @click="addReference5" src="../../../../assets/yi-19.png" />
            </p> -->
            
            <!-- <p>
              <span>*</span>成型方式：
              <el-input v-model="input9" placeholder="一页成型"></el-input>
              <img @click="addInputBox12" src="../../../../assets/yi-19.png" />
            </p> -->
            <!-- <div class="show_data" v-show="showData12">
              <p class="data_form">
                <el-input class="el-input2" v-model="input39" placeholder="一页成型"></el-input>
                <img @click="addInputBox13" src="../../../../assets/yi-19.png" />
              </p>
            </div>
            <div class="show_data" v-show="showData13">
              <p class="data_form">
                <el-input class="el-input2" v-model="input40" placeholder="一页成型"></el-input>
                <img @click="addInputBox14" src="../../../../assets/yi-19.png" />
              </p>
            </div>
            <div class="show_data" v-show="showData14">
              <p class="data_form">
                <el-input class="el-input2" v-model="input41" placeholder="一页成型"></el-input>
              </p>
            </div> -->

            <!-- <p id="references6">
              <span>*</span>面纸类型：
              <el-input v-model="references6" type="text"></el-input>
              <img @click="addReference6" src="../../../../assets/yi-19.png" />
            </p> -->

            <!-- <p>
              <span>*</span>面纸类型：
              <el-input v-model="input10"></el-input>
              <img @click="addInputBox15" src="../../../../assets/yi-19.png" />
            </p> -->
            <!-- <div class="show_data" v-show="showData15">
              <p class="data_form">
                <el-input class="el-input2" v-model="input42"></el-input>
                <img @click="addInputBox16" src="../../../../assets/yi-19.png" />
              </p>
              </div>
            <div class="show_data" v-show="showData16">
              <p class="data_form">
                <el-input class="el-input2" v-model="input43"></el-input>
                <img @click="addInputBox17" src="../../../../assets/yi-19.png" />
              </p>
            </div>
            <div class="show_data" v-show="showData17">
              <p class="data_form">
                <el-input class="el-input2" v-model="input44"></el-input>
              </p>
            </div> -->

            <!-- <p id="references7">
              <span>*</span>版面设定：
              <el-input v-model="references7" type="text"></el-input>
              <img @click="addReference7" src="../../../../assets/yi-19.png" />
            </p> -->

            <!-- <p>
              <span>*</span>版面设定：
              <el-input v-model="input11"></el-input>
              <img @click="addInputBox18" src="../../../../assets/yi-19.png" />
            </p> -->
            <!-- <div class="show_data" v-show="showData18">
              <p class="data_form">
                <el-input class="el-input2" v-model="input45"></el-input>
                <img @click="addInputBox19" src="../../../../assets/yi-19.png" />
              </p>
            </div>
            <div class="show_data" v-show="showData19">
              <p class="data_form">
                <el-input class="el-input2" v-model="input46"></el-input>
                <img @click="addInputBox20" src="../../../../assets/yi-19.png" />
              </p>
            </div>
            <div class="show_data" v-show="showData20">
              <p class="data_form">
                <el-input class="el-input2" v-model="input47"></el-input>
              </p>
            </div> -->

            <!-- <p id="references8">
              <span>*</span>开槽模切：
              <el-input v-model="references8" type="text"></el-input>
              <img @click="addReference8" src="../../../../assets/yi-19.png" />
            </p> -->
            
            <!-- <p>
              <span>*</span>开槽模切：
              <el-input v-model="input12"></el-input>
              <img @click="addInputBox21" src="../../../../assets/yi-19.png" />
            </p> -->
            <!-- <div class="show_data" v-show="showData21">
              <p class="data_form">
                <el-input class="el-input2" v-model="input48"></el-input>
                <img @click="addInputBox22" src="../../../../assets/yi-19.png" />
              </p>
            </div>
            <div class="show_data" v-show="showData22">
              <p class="data_form">
                <el-input class="el-input2" v-model="input49"></el-input>
                <img @click="addInputBox23" src="../../../../assets/yi-19.png" />
              </p>
            </div>
            <div class="show_data" v-show="showData23">
              <p class="data_form">
                <el-input class="el-input2" v-model="input50"></el-input>
              </p>
            </div> -->

            <!-- <p id="references9">
              <span>*</span>印刷面积：
              <el-input class="el-input1" v-model="references9" type="text"></el-input>
              <img @click="addReference9" src="../../../../assets/yi-19.png" />
            </p> -->

            <!-- <p>
              <span>*</span>印刷面积：
              <el-input class="el-input1" v-model="input13"></el-input>
              <img @click="addInputBox24" src="../../../../assets/yi-19.png" />
            </p> -->
            <!-- <div class="show_data2" v-show="showData24">
              <p class="data_form2">
                <el-input class="el-input3" v-model="input51"></el-input>
                <img @click="addInputBox25" src="../../../../assets/yi-19.png" />
              </p>
            </div>
            <div class="show_data2" v-show="showData25">
              <p class="data_form2">
                <el-input class="el-input3" v-model="input52"></el-input>
                <img @click="addInputBox26" src="../../../../assets/yi-19.png" />
              </p>
            </div>
            <div class="show_data2" v-show="showData26">
              <p class="data_form2">
                <el-input class="el-input3" v-model="input53"></el-input>
              </p>
            </div> -->

            <!-- <p id="references10">
              <span>*</span>数码表处：
              <el-input class="el-input1" v-model="references10" type="text"></el-input>
              <img @click="addReference10" src="../../../../assets/yi-19.png" />
            </p> -->

            <!-- <p>
              <span>*</span>数码表处：
              <el-input class="el-input1" v-model="input14"></el-input>
              <img @click="addInputBox27" src="../../../../assets/yi-19.png" />
            </p> -->
            <!-- <div class="show_data2" v-show="showData27">
              <p class="data_form2">
                <el-input class="el-input3" v-model="input54"></el-input>
                <img @click="addInputBox28" src="../../../../assets/yi-19.png" />
              </p>
            </div>
            <div class="show_data2" v-show="showData28">
              <p class="data_form2">
                <el-input class="el-input3" v-model="input55"></el-input>
                <img @click="addInputBox29" src="../../../../assets/yi-19.png" />
              </p>
            </div>
            <div class="show_data2" v-show="showData29">
              <p class="data_form2">
                <el-input class="el-input3" v-model="input56"></el-input>
              </p>
            </div> -->

            <!-- <p id="references11">
              <span>*</span>成箱方式：
              <el-input v-model="references11" type="text"></el-input>
              <img @click="addReference11" src="../../../../assets/yi-19.png" />
            </p> -->

            <!-- <p>
              <span>*</span>成箱方式：
              <el-input v-model="input15"></el-input>
              <img @click="addInputBox30" src="../../../../assets/yi-19.png" />
            </p> -->
            <!-- <div class="show_data" v-show="showData30">
              <p class="data_form">
                <el-input class="el-input2" v-model="input57"></el-input>
                <img @click="addInputBox31" src="../../../../assets/yi-19.png" />
              </p>
            </div> -->

            <!-- <p id="references12">
              <span>*</span>打包方式：
                <el-input class="el-input1" v-model="references12" type="text"></el-input>
              <img @click="addReference12" src="../../../../assets/yi-19.png" />
            </p> -->

            <!-- <p>
              <span>*</span>打包方式：
              <el-input class="el-input1" v-model="input16"></el-input>
              <img @click="addInputBox33" src="../../../../assets/yi-19.png" />
            </p> -->
            <!-- <div class="show_data2" v-show="showData33">
              <p class="data_form2">
                <el-input class="el-input3" v-model="input60"></el-input>
                <img @click="addInputBox34" src="../../../../assets/yi-19.png" />
              </p>
            </div> -->
           
            <button @click="addCustomInfo" class="next_step">确认提交</button>
          </div>
        </el-tab-pane>
        <el-tab-pane name="商品相册" label="商品相册">
          <div class="photo_frame">
            <!-- <el-upload
              action="#"
              list-type="picture-card"
              :auto-upload="false">
                <i slot="default" class="el-icon-plus"></i>
                <div slot="file" slot-scope="{file}">
                  <img
                    class="el-upload-list__item-thumbnail"
                    :src="file.url" alt=""
                  >
                  <span class="el-upload-list__item-actions">
                    <span
                      class="el-upload-list__item-preview"
                      @click="handlePictureCardPreview(file)"
                    >
                      <i class="el-icon-zoom-in"></i>
                    </span>
                    <span
                      v-if="!disabled"
                      class="el-upload-list__item-delete"
                      @click="handleDownload(file)"
                    >
                      <i class="el-icon-download"></i>
                    </span>
                    <span
                      v-if="!disabled"
                      class="el-upload-list__item-delete"
                      @click="handleRemove(file)"
                    >
                      <i class="el-icon-delete"></i>
                    </span>
                  </span>
                </div>
            </el-upload> -->
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
  name: "customizeStore",
  data() {
    return {
      activeName: 'first',
      title: '',
      // input2: '',
      // input3: '',
      // input4: '',
      // input5: '',
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
      // references: '',
      // references1: '',
      // references20: '',
      // references21: '',
      // references22: '',
      // references3: '',
      // references4: '',
      // references5: '',
      // references6: '',
      // references7: '',
      // references8: '',
      // references9: '',
      // references10: '',
      // references11: '',
      // references12: '',
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
      nameValue: []
    };
  },
  created() {
    this.getData();
      this.getCustomTemplateList();
  },
  methods: {
    // addReference: function(e) {
    //   e.preventDefault();
    //   var inputEl = '<p style="margin-left: 94px; "><input style="width: 134px; font-size: 14px; padding: 0 15px; border: 1px solid #DCDFE6;background-color: #FFF; background-image: none; border-radius: 4px; height: 38px; line-height: 38px;" v-model="references" type="text"></p>';
    //   $('#references').append(inputEl);
    // },
    // addReference1: function(e) {
    //   e.preventDefault();
    //   var inputEl1 = '<p style="margin-left: 94px; "><input style="width: 134px; font-size: 14px; padding: 0 15px; border: 1px solid #DCDFE6;background-color: #FFF; background-image: none; border-radius: 4px; height: 38px; line-height: 38px;" v-model="references1" type="text"></p>';
    //   $('#references1').append(inputEl1);
    // },
    // addReference2: function(e) {
    //   e.preventDefault();
    //   var inputEl2 = '<p style="margin-left: 94px; "><input style="width: 207px; margin-right: 23px; font-size: 14px; padding: 0 15px; border: 1px solid #DCDFE6;background-color: #FFF; background-image: none; border-radius: 4px; height: 38px; line-height: 38px;" v-model="references20" placeholder="长 cm" type="text"><input style="width: 207px; margin-right: 23px; font-size: 14px; padding: 0 15px; border: 1px solid #DCDFE6;background-color: #FFF; background-image: none; border-radius: 4px; height: 38px; line-height: 38px;" v-model="references21" placeholder="宽 cm" type="text"><input style="width: 207px; font-size: 14px; padding: 0 15px; border: 1px solid #DCDFE6;background-color: #FFF; background-image: none; border-radius: 4px; height: 38px; line-height: 38px;" v-model="references22" placeholder="高 cm" type="text"></p>';
    //   $('#references2').append(inputEl2);
    // },
    // addReference3: function(e) {
    //   e.preventDefault();
    //   var inputEl3 = '<p style="margin-left: 94px; "><input style="width: 134px; font-size: 14px; padding: 0 15px; border: 1px solid #DCDFE6;background-color: #FFF; background-image: none; border-radius: 4px; height: 38px; line-height: 38px;" v-model="references3" placeholder="非承压" type="text"></p>';
    //   $('#references3').append(inputEl3);
    // },
    // addReference4: function(e) {
    //   e.preventDefault();
    //   var inputEl4 = '<p style="margin-left: 94px; "><input style="width: 207px; font-size: 14px; padding: 0 15px; border: 1px solid #DCDFE6;background-color: #FFF; background-image: none; border-radius: 4px; height: 38px; line-height: 38px;" v-model="references4" placeholder="正常" type="text"></p>';
    //   $('#references4').append(inputEl4);
    // },
    // addReference5: function(e) {
    //   e.preventDefault();
    //   var inputEl5 = '<p style="margin-left: 94px; "><input style="width: 207px; font-size: 14px; padding: 0 15px; border: 1px solid #DCDFE6;background-color: #FFF; background-image: none; border-radius: 4px; height: 38px; line-height: 38px;" v-model="references5" placeholder="一页成型" type="text"></p>';
    //   $('#references5').append(inputEl5);
    // },
    // addReference6: function(e) {
    //   e.preventDefault();
    //   var inputEl6 = '<p style="margin-left: 94px; "><input style="width: 207px; font-size: 14px; padding: 0 15px; border: 1px solid #DCDFE6;background-color: #FFF; background-image: none; border-radius: 4px; height: 38px; line-height: 38px;" v-model="references6" type="text"></p>';
    //   $('#references6').append(inputEl6);
    // },
    // addReference7: function(e) {
    //   e.preventDefault();
    //   var inputEl7 = '<p style="margin-left: 94px; "><input style="width: 207px; font-size: 14px; padding: 0 15px; border: 1px solid #DCDFE6;background-color: #FFF; background-image: none; border-radius: 4px; height: 38px; line-height: 38px;" v-model="references7" type="text"></p>';
    //   $('#references7').append(inputEl7);
    // },
    // addReference8: function(e) {
    //   e.preventDefault();
    //   var inputEl8 = '<p style="margin-left: 94px; "><input style="width: 207px; font-size: 14px; padding: 0 15px; border: 1px solid #DCDFE6;background-color: #FFF; background-image: none; border-radius: 4px; height: 38px; line-height: 38px;" v-model="references8" type="text"></p>';
    //   $('#references8').append(inputEl8);
    // },
    // addReference9: function(e) {
    //   e.preventDefault();
    //   var inputEl9 = '<p style="margin-left: 94px; "><input style="width: 134px; font-size: 14px; padding: 0 15px; border: 1px solid #DCDFE6;background-color: #FFF; background-image: none; border-radius: 4px; height: 38px; line-height: 38px;" v-model="references9" type="text"></p>';
    //   $('#references9').append(inputEl9);
    // },
    // addReference10: function(e) {
    //   e.preventDefault();
    //   var inputEl10 = '<p style="margin-left: 94px; "><input style="width: 134px; font-size: 14px; padding: 0 15px; border: 1px solid #DCDFE6;background-color: #FFF; background-image: none; border-radius: 4px; height: 38px; line-height: 38px;" v-model="references10" type="text"></p>';
    //   $('#references10').append(inputEl10);
    // },
    // addReference11: function(e) {
    //   e.preventDefault();
    //   var inputEl11 = '<p style="margin-left: 94px; "><input style="width: 207px; font-size: 14px; padding: 0 15px; border: 1px solid #DCDFE6;background-color: #FFF; background-image: none; border-radius: 4px; height: 38px; line-height: 38px;" v-model="references11" type="text"></p>';
    //   $('#references11').append(inputEl11);
    // },
    // addReference12: function(e) {
    //   e.preventDefault();
    //   var inputEl12 = '<p style="margin-left: 94px; "><input style="width: 134px; font-size: 14px; padding: 0 15px; border: 1px solid #DCDFE6;background-color: #FFF; background-image: none; border-radius: 4px; height: 38px; line-height: 38px;" v-model="references12" type="text"></p>';
    //   $('#references12').append(inputEl12);
    // },
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

    // addReference13: function(e) {
    //   e.preventDefault();
    //   var inputEl13 = '<p style="margin-left: 94px; "><input style="width: 207px; font-size: 14px; padding: 0 15px; border: 1px solid #DCDFE6;background-color: #FFF; background-image: none; border-radius: 4px; height: 38px; line-height: 38px;" v-model="checkValue0" type="text"></p>';
    //   $('#references13').append(inputEl13);
    // },
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
      // var checkValue = []

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
        class_one: this.value,
        class_two: this.value1,
        class_three: this.value2,
        template_id: this.value3,
        space: data
      }, "post")
      .then(res => {
        if(res.data.status == 1) {
          this.$message.success(res.data.message);
          // this.$router.push({
          // name: "goodsRelease"
          // });
          this.changeTab = '商品相册';
        }
      })
      .catch(err => {
          console.log(err)
      });
    },
    // handleRemove(file) {
    //   console.log(file);
    // },
    // handlePictureCardPreview(file) {
    //   this.dialogImageUrl = file.url;
    //   this.dialogVisible = true;
    // },
    // handleDownload(file) {
    //   console.log(file);
    // },
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
      console.log("fileChange");
      this.fileList.push({ name: file.name, url: file.url });
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
      // if (this.uploadFile[0]) {
			// this.pic_url = this.uploadFile[0];
			// }
			// else if (this.uploadFile.length > 1) {
			// 	this.pic_url = this.uploadFile;
			// }
			this.$HTTP(this.$httpConfig.addGoodsPic, { 
        pic_url: this.uploadFile 
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
.customize_store {
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
      p:nth-of-type(4) {
        color: #999999;
        padding-left: 94px;
        margin-top: -15px;
      }
      p:nth-of-type(5) {
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