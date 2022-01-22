<template>
	<!-- 店铺 -店铺设置 -->
	<div class="classify">
		<div class="g_att">
			<h1 class="t_title">
				<span class="size16">店铺设置</span>
			</h1>
			<div class="notes-box">
				<div class="notes_title">温馨提示</div>
				<div class="notes_content">
					<p>您填写的信息将在店铺前台展示给买家，请认真填写</p>
				<p>请在2分钟内添加图片，否则保存后点击“确认提交”按钮重新进入此页面修改。</p>
				</div>
				<div class="info-s">s-h-o-p-s-n</div>
			</div>
			<h1 class="t_title heading">
				<span class="size14">店铺基本信息</span>
			</h1>
			<table width="100%" border="0" cellspacing="0" cellpadding="0" class="list info">
				<tr>
					<td align="right" class="black">
						<b>*</b> 店铺名称：</td>
					<td>
						<el-input placeholder="请输入内容" v-model="shop_name" class="el-input" clearable>
						</el-input>
					</td>
				</tr>
				<tr>
					<td align="right" class="black">
						<b>*</b> 企业名称：</td>
					<td>
						<el-input placeholder="请输入内容" v-model="company_name" class="el-input" disabled clearable>
						</el-input>
					</td>
				</tr>
				<tr>
					<td align="right" class="black">
						<b>*</b> 工商注册号：</td>
					<td>
						<el-input placeholder="请输入内容" v-model="code" class="el-input" disabled clearable>
						</el-input>
					</td>
				</tr>
				<tr>
					<td align="right" class="black">
						<b>*</b> 企业法人：</td>
					<td>
						<el-input placeholder="请输入内容" v-model="name" class="el-input" disabled clearable>
						</el-input>
					</td>
				</tr>
				<tr>
					<td align="right" class="black">
						<b>*</b> 企业类型：</td>
					<td>
						<el-input placeholder="请输入内容" v-model="enterprise_type" class="el-input" disabled clearable>
						</el-input>
					</td>
				</tr>
				<tr>
					<td align="right" class="black">
						<b>*</b> 注册资本：</td>
					<td>
						<el-input placeholder="请输入内容" v-model="registered_capital" class="el-input" disabled clearable>
						</el-input>
					</td>
				</tr>
				<tr>
					<td width="13%" align="right" class="black">
						<b>*</b> 工商营业执照电子版： </td>
					<td width="80%" id="input-box">
						<img :src="URL+electronic_version" alt="" class="shop_img">
						<!-- <img v-show="electronic_version" :src="URL+electronic_version" alt="" class="shop_img">
						<el-upload :action="action" list-type="picture-card" accept=".jpg,.png,.jpeg" name="file" :limit=1 :on-exceed="exceeding1" :data="uploadData" :before-upload="beforeUploade1" :file-list="fileList1" :on-success="success1" :on-preview="handlePictureCardPreview1" :on-remove="handleRemove1">
							<i class="el-icon-plus"></i>
						</el-upload>
						<p>文件格式 GIF, JPG, JPEG, PNG 文件大小80k 以内，建议尺寸宽度介于{{imageConf.min_width}}~{{imageConf.max_width}},高度介于{{imageConf.min_height}}~{{imageConf.max_height}}</p>
						<el-dialog :visible.sync="dialogVisible1">
							<img width="100%" :src="dialogImageUrl1" alt="">
						</el-dialog> -->
					</td>
				</tr>
				<tr>
					<td align="right" class="black">
						<b>*</b> 业务联系人：</td>
					<td>
						<el-input placeholder="请输入内容" v-model="bus_name" class="el-input" disabled clearable>
						</el-input>
					</td>
				</tr>
				<tr>
					<td align="right" class="black">
						<b>*</b> 业务联系电话：</td>
					<td>
						<el-input placeholder="请输入内容" v-model="mobile" class="el-input" disabled clearable>
						</el-input>
					</td>
				</tr>
				<tr>
					<td align="right" class="black">
						<b>*</b> 经营模式：</td>
					<td>
						<el-input  v-model="grade_name" class="el-input" disabled clearable>
						</el-input>
					</td>
				</tr>
				<tr>
					<td align="right" class="black">
						<b>*</b> 开票能力：</td>
					<td style="padding-left: 20px;">
						<!-- <el-input placeholder="请输入内容" v-model="invoice" class="el-input" clearable>
						</el-input> -->
						<el-radio v-model="invoice" :label="0" disabled>增值税专用发票</el-radio>
                    	<el-radio v-model="invoice" :label="1" disabled>普通发票</el-radio>
					</td>
				</tr>
				<tr>
					<td align="right" class="black">
						<b>*</b> 合作买家：</td>
					<td>
						<el-input placeholder="请输入内容" v-model="buy" class="el-input" disabled clearable>
						</el-input>
					</td>
				</tr>
				<tr>
					<td align="right" class="black">
						<b>*</b> 店铺状态：</td>
					<td style="padding-left: 20px;">
						<!-- <el-input placeholder="请输入内容" v-model="store_state" class="el-input" clearable>
						</el-input> -->
						<el-radio v-model="store_state" :label="0" disabled>关闭</el-radio>
                    	<el-radio v-model="store_state" :label="1" disabled>开启</el-radio>
					</td>
				</tr>
				<tr>
					<td align="right" class="black">
						<b>*</b> 有效时长：</td>
					<td style="padding-left: 20px;" v-if="effect_time == 0">
						<el-radio v-model="effect_time" :label="0" disabled>长期</el-radio>
                    	<el-radio v-model="effect_time" :label="1" disabled>有效期</el-radio>
					</td>
					<td v-if="effect_time == 1">
						<el-date-picker style="width: 150px;" v-model="st_time" type="date" value-format="yyyy-MM-dd" placeholder="选择日期"></el-date-picker>
							—
						<el-date-picker style="width: 150px;" v-model="en_time" type="date" value-format="yyyy-MM-dd" placeholder="选择日期"></el-date-picker>
					</td>
				</tr>
				<tr>
					<td align="center" class="black">
						<b>*</b> 供货类目设计品牌代理：</td>
					<td>
						<el-input placeholder="请输入内容" v-model="brand_agent" class="el-input" disabled clearable>
						</el-input>
					</td>
				</tr>
				<tr>
					<td width="13%" align="center" class="black">
						<b>*</b> 供货类目设计品牌代理凭证： </td>
					<td width="80%" id="input-box">
						<img :src="URL+brand_agent_img" alt="" class="shop_img">
						<!-- <img v-show="brand_agent_img" :src="URL+brand_agent_img" alt="" class="shop_img">
						<el-upload :action="action" list-type="picture-card" accept=".jpg,.png,.jpeg" name="file" :limit=1 :on-exceed="exceeding2" :data="uploadData" :before-upload="beforeUploade2" :file-list="fileList2" :on-success="success2" :on-preview="handlePictureCardPreview2" :on-remove="handleRemove2">
							<i class="el-icon-plus"></i>
						</el-upload>
						<p>文件格式 GIF, JPG, JPEG, PNG 文件大小80k 以内，建议尺寸宽度介于{{imageConf.min_width}}~{{imageConf.max_width}},高度介于{{imageConf.min_height}}~{{imageConf.max_height}}</p>
						<el-dialog :visible.sync="dialogVisible2">
							<img width="100%" :src="dialogImageUrl2" alt="">
						</el-dialog> -->
					</td>
				</tr>
				<tr>
					<td align="center" class="black">
						<b>*</b> 供货类目涉及限售或危化品：</td>
					<td>
						<el-input placeholder="请输入内容" v-model="categroy" class="el-input" disabled clearable>
						</el-input>
					</td>
				</tr>
				<tr>
					<td width="13%" align="center" class="black">
						<b>*</b> 供货类目涉及限售或危化品凭证： </td>
					<td width="80%" id="input-box">
						<img :src="URL+categroy_img" alt="" class="shop_img">
						<!-- <img v-show="categroy_img" :src="URL+categroy_img" alt="" class="shop_img">
						<el-upload :action="action" list-type="picture-card" accept=".jpg,.png,.jpeg" name="file" :limit=1 :on-exceed="exceeding3" :data="uploadData" :before-upload="beforeUploade3" :file-list="fileList3" :on-success="success3" :on-preview="handlePictureCardPreview3" :on-remove="handleRemove3">
							<i class="el-icon-plus"></i>
						</el-upload>
						<p>文件格式 GIF, JPG, JPEG, PNG 文件大小80k 以内，建议尺寸宽度介于{{imageConf.min_width}}~{{imageConf.max_width}},高度介于{{imageConf.min_height}}~{{imageConf.max_height}}</p>
						<el-dialog :visible.sync="dialogVisible3">
							<img width="100%" :src="dialogImageUrl3" alt="">
						</el-dialog> -->
					</td>
				</tr>
				<tr>
					<td align="right" class="black">
						<b>*</b> 备注：</td>
					<td>
						<el-input placeholder="请输入内容" v-model="remarks" class="el-input" disabled clearable>
						</el-input>
					</td>
				</tr>
				<tr>
					<td align="right" class="black">
						<b>*</b> 店铺销量：</td>
					<td>
						<el-input placeholder="请输入内容" v-model="store_sales" class="el-input" disabled clearable>
						</el-input>
					</td>
				</tr>
				<tr>
					<td align="right" class="black">
						<b>*</b> 店铺收藏数量：</td>
					<td>
						<el-input placeholder="请输入内容" v-model="store_collect" class="el-input" clearable disabled>
						</el-input>
					</td>
				</tr>
				<!-- <tr>
					<td align="right" class="black">
						<b>*</b> 店铺排序：</td>
					<td>
						<el-input placeholder="请输入内容" v-model="store_sort" class="el-input" clearable>
						</el-input>
					</td>
				</tr>
				<tr>
					<td align="right" class="black">
						<b>*</b> 是否自营店铺：</td>
					<td style="padding-left: 20px;">
						<el-radio v-model="is_own" :label="0">否</el-radio>
                    	<el-radio v-model="is_own" :label="1">是</el-radio>
					</td>
				</tr>
				<tr>
					<td align="right" class="black">
						<b>*</b> 是否推荐：</td>
					<td style="padding-left: 20px;">
						<el-radio v-model="status" :label="0">否</el-radio>
                    	<el-radio v-model="status" :label="1">是</el-radio>
					</td>
				</tr>
				<tr>
					<td align="right" class="black">
						<b>*</b> 开店时常：</td>
					<td>
						<el-input placeholder="请输入内容" v-model="shop_long" class="el-input" clearable>
						</el-input>
					</td>
				</tr> -->
				<tr>
					<td align="right" class="black">
						<b>*</b> 开店用户名称：</td>
					<td>
						<el-input placeholder="请输入内容" v-model="user_name" class="el-input" disabled clearable>
						</el-input>
					</td>
				</tr>
				<tr>
					<td width="13%" align="right" class="black">
						<b>*</b> 店铺 LOGO： </td>
					<td width="80%" id="input-box">
						<img v-show="store_logo" :src="URL+store_logo" alt="" class="shop_img">
						<el-upload :action="action" list-type="picture-card" accept=".jpg,.png,.jpeg" name="file" :limit=1 :on-exceed="exceeding" :data="uploadData" :before-upload="beforeUploade" :file-list="fileList" :on-success="success" :on-preview="handlePictureCardPreview" :on-remove="handleRemove">
							<i class="el-icon-plus"></i>
						</el-upload>
						<p>文件格式 GIF, JPG, JPEG, PNG 文件大小80k 以内，建议尺寸宽度{{imageConf.min_width}},高度{{imageConf.min_height}}</p>
						<el-dialog :visible.sync="dialogVisible">
							<img width="100%" :src="dialogImageUrl" alt="">
						</el-dialog>
					</td>
				</tr>
				<!-- <tr>
					<td width="13%" align="right" class="black nothing">
						<b>*</b> 店铺简介：
						<p class="none"></p>
					</td>
					<td width="80%">
						<el-input type="textarea" :autosize="{ minRows: 2, maxRows: 5}" :rows="2" class="el-input" placeholder="请输入内容" v-model="description">
						</el-input>
						<p>店铺简介会加入到 SEO 优化中 ，100字以内</p>
					</td>
				</tr> -->
			</table>
			<h1 class="t_title heading">
				<span class="size14">店铺经营信息</span>
			</h1>
			<table width="100%" border="0" cellspacing="0" cellpadding="0" class="manage list">
				<!-- <tr>
					<td width="13%" align="right" class="black"> 经营时间： </td>
					<td width="90%" style="padding:0">
						<el-table :data="tableData" border style="width: 82%">
							<el-table-column v-for="item in week" width="60" :key="item.id" property="flag" :label="item">
								<template slot-scope="scope">
									<el-switch disabled v-model="flag" active-color="#13ce66" inactive-color="#ff4949">
									</el-switch>
								</template>
							</el-table-column>
							<el-table-column label="开始时间">
								<template slot-scope="scope">
									<span class="up_time">
										<el-time-select placeholder="00:00" v-model="start_time" :picker-options="{
	                            start: '00:00',
	                            step: '00:60',
	                            end: '23:59'
	                            }">
										</el-time-select>
									</span>
								</template>
							</el-table-column>
							<el-table-column label="结束时间">
								<template slot-scope="scope">
									<span class="up_time">
										<el-time-select placeholder="00:00" v-model="end_time" :picker-options="{
	                            start: '00:00',
	                            step: '00:60',
	                            end: '23:59'
	                            }">
										</el-time-select>
									</span>
								</template>
							</el-table-column>
						</el-table>
					</td>
				</tr> -->
				<tr>
					<td align="right" class="black">
						<b>*</b> 联系地址： </td>
					<td>
						<city-three v-on:sendcityData="getCityData" :sendParams="city_tree"></city-three>
					</td>
				</tr>
				<tr>
					<td width="13%" align="right" class="black nothing">
						<b>*</b> 详细地址：
						<p class="none_z"></p>
					</td>
					<td width="80%" id="address">
						<el-input type="textarea" :autosize="{ minRows: 2, maxRows: 5}" :rows="2" class="el-input" placeholder="请输入内容" v-model="register_address">
						</el-input>
					</td>
				</tr>
				<tr>
					<td align="right" class="black">
						<b>*</b>真实联系地址： </td>
					<td>
						<city-four v-on:sendcityData1="getCityData1" :sendParams1="city_four"></city-four>
					</td>
				</tr>
				<tr>
					<td width="13%" align="right" class="black nothing">
						<b>*</b> 真实详细地址：
						<p class="none_z"></p>
					</td>
					<td width="80%" id="address">
						<el-input type="textarea" :autosize="{ minRows: 2, maxRows: 5}" :rows="2" class="el-input" placeholder="请输入内容" v-model="actual_address">
						</el-input>
					</td>
				</tr>
				<tr>
					<td align="right">&nbsp;</td>
					<td class="submit-box">
						<el-button type="success" @click="submit">确认提交</el-button>
					</td>
					<td>&nbsp;</td>
				</tr>
			</table>
		</div>
	</div>
</template>
<script>
export default {
	name: 'shopfit',
	data() {
		return {
			startTime: '',
			endTime: '',
			flag: true,
			value: true,
			week: ['周一', '周二', '周三', '周四', '周五', '周六', '周日'],
			tableData: [{ falg: true }],
			textfield1: 'e',
			action: this.$store.state.image_api_url + "FileUpload/uploadStoreLogo/",
			// dialogImageUrl1: "",
			// dialogVisible1: false,
			// dialogImageUrl2: "",
			// dialogVisible2: false,
			// dialogImageUrl3: "",
			// dialogVisible3: false,
			dialogImageUrl: "",
			dialogVisible: false,
			textarea: '22',
			// fileList1: [],
			// fileList2: [],
			// fileList3: [],
			uploadData: {
				sessionToken: "",
				imageToken: ""
			},
			fileList: [],
			imageConf: {},
			imageToken: "",
			sToken: "", // session token
			// uploadFile1: [],
			// uploadFile2: [],
			// uploadFile3: [],
			uploadFile: [],
			classData: {}, // 一级分类
			classByTwo: [], // 二级分类数据
			classByThree: [], // 三级分类数据
			shopData: {
				address: {},
				store: {
					shop_name: ''
				}
			},
			city_tree: {},
			city_four: {},
			shop_name: '',
			company_name: '',
			code: '',
			name: '',
			enterprise_type: '',
			registered_capital: '',
			bus_name: '',
			mobile: '',
			grade_name: '',
			invoice: '',
			buy: '',
			store_state: '',
			effect_time: '',
			st_time: '',
			en_time: '',
			brand_agent: '',
			categroy: '',
			remarks: '',
			store_sales: '',
			store_collect: '',
			// store_sort: '',
			// is_own: '',
			// status: '',
			// shop_long: '',
			user_name: '',
			// description: '',
			// start_time: '',
			// end_time: '',
			register_address: '',
			prov: 0,
			dist: 0,
			city: 0,
			actual_address: '',
			prov_id: 0,
			dist_id: 0,
			city_id: 0,
			electronic_version: '',
			brand_agent_img: '',
			categroy_img: '',
			store_logo: '',
			store_address: 0
		}
	},
	created() {
		this.invoking();
	},
	mounted() {
		this.$HTTP(this.$httpConfig.storeLogoCofig, {}, 'post').then(res => {
			let data = res.data.data;
			this.imageConf = data.config;
			this.imageToken = data.token;
			this.sToken = data.s_token;
		});
	},
	methods: {
		// 店铺信息
		invoking(){
			this.$HTTP(this.$httpConfig.getStoreInfo, {}, 'post').then((res) => {
						let store = res.data.data.store;
						let address = res.data.data.address;
						this.shop_name = store.shop_name;
						this.company_name = store.company_name;
						this.code = store.code;
						this.name = store.name;
						this.enterprise_type = store.enterprise_type;
						this.registered_capital = store.registered_capital;
						this.bus_name = store.bus_name;
						this.mobile = store.mobile;
						this.grade_name = store.grade_name;
						this.invoice = store.invoice;
						this.buy = store.buy;
						this.store_state = store.store_state;
						this.brand_agent = store.brand_agent;
						this.categroy = store.categroy;
						this.remarks = store.remarks;
						this.store_sales = store.store_sales;
						this.store_collect = store.store_collect;
						// this.store_sort = store.store_sort;
						// this.is_own = store.is_own;
						// this.status = store.status;
						// this.shop_long = store.shop_long;
						this.user_name = store.user_name;
						this.print_desc = store.print_desc;
						// this.description = store.description;
						// if (store.effect_time.length == 1) {
						// 	this.effect_time = '0' + store.effect_time + ":00";
						// } else {
						// 	this.effect_time = store.effect_time + ":00";
						// }
						// if (store.start_time.length == 1) {
						// 	this.start_time = '0' + store.start_time + ":00";
						// } else {
						// 	this.start_time = store.start_time + ":00";
						// }
						// if (store.end_time.length == 1) {
						// 	this.end_time = '0' + store.end_time + ":00";
						// } else {
						// 	this.end_time = store.end_time + ":00";
						// }
						// this.effect_time = this.timeFormat(~~store.effect_time);
						// this.start_time = this.timeFormat(~~store.start_time);
						// this.end_time = this.timeFormat(~~store.end_time);
						this.effect_time = store.effect_time;
						this.store_logo = store.store_logo;
						this.electronic_version = store.electronic_version;
						this.brand_agent_img = store.brand_agent_img;
						this.categroy_img = store.categroy_img;
						this.store_address = store.store_address;
						this.register_address = address.register_address.address;
						this.actual_address = address.actual_address.address;
						this.prov = address.register_address.prov;
						this.city = address.register_address.city;
						this.dist = address.register_address.dist;
						this.prov_id = address.actual_address.prov;
						this.city_id = address.actual_address.city;
						this.dist_id = address.actual_address.dist;
						this.city_tree = {
							prov: this.prov,
							city: this.city,
							dist: this.dist
						};
						this.city_four = {
							prov: this.prov_id,
							city: this.city_id,
							dist: this.dist_id
						};
					}).catch((err) => {
						this.$message.error(err);
					});
		},
		// 时间转换锉
		timeFormat (time, temp = true) {
				let t = typeof time === 'number' && time.toString().length === 10 ? time.toString() * 1000 : time.valueOf()
				let date = new Date(t)
				let year = date.getFullYear(time)
				let month = date.getMonth(time) + 1
				let day = date.getDate(time)
				let hour = date.getHours(time) <= 9 ? '0' + date.getHours(time) : date.getHours(time)
				let minute = date.getMinutes(time) <= 9 ? '0' + date.getMinutes(time) : date.getMinutes(time)
				let seconds = date.getSeconds(time) <= 9 ? '0' + date.getSeconds(time) : date.getSeconds(time)
				return  hour + ':' + minute
  	},
			// 获取省市区数据
		getCityData(data) {
			this.prov = data.prov;
			this.city = data.city;
			this.dist = data.dist;
		},
		getCityData1(data) {
			this.prov_id = data.prov;
			this.city_id = data.city;
			this.dist_id = data.dist;
		},

		// handleRemove1(file, fileList1, index) {
		// 	this.$HTTP(this.$httpConfig.delGoodsImgCofig, {
		// 		fileName: file.response.data,
		// 		sessionToken: this.uploadData.sessionToken,
		// 		imageToken: this.uploadData.imageToken
		// 	}, 'post').then(res => {
		// 		//找到删除的图片并在数据里删除
		// 		let index = this.uploadFile1.indexOf(file.response.data);
		// 		this.uploadFile1.splice(index, 1);
		// 		this.$message.success(res.data.message);
		// 	}).catch(function (error) {
		// 		console.log(error);
		// 	});
		// },
		// // 上传之前
		// beforeUploade1(file) {
		// 	this.uploadData.sessionToken = this.sToken;
		// 	this.uploadData.imageToken = this.imageToken;
		// 	const isLt2M = file.size / 1024 / 1024 < 3;
		// 	if (!isLt2M) {
		// 		this.$message.error("上传头像图片大小不能超过 2MB!");
		// 	}
		// 	return isLt2M;
		// },
		// //显示
		// handlePictureCardPreview1(file) {
		// 	this.dialogImageUrl1 = file.url;
		// 	this.dialogVisible1 = true;
		// },
		// // 上传成功
		// success1(response, file, fileList1) {
		// 	// console.log(response)
		// 	this.$message.success(response.message);
		// 	if (response.status == 0) {
		// 		let length = fileList1.length;
		// 		let i = 0;
		// 		for (i; i < length; i++) {
		// 			if (fileList1[i].name === file.name) {
		// 				fileList1.splice(i, 1);
		// 			}
		// 		}
		// 	} else {
		// 		this.uploadFile1.push(response.data);
		// 	}
		// },
		// //超出文件个数
		// exceeding1(files, fileList1) {
		// 	if (fileList1.length == 1) {
		// 		this.$message({
		// 			duration: 1000,
		// 			type: 'error',
		// 			message: '超出最大文件个数!'
		// 		});
		// 	}
		// },

		// handleRemove2(file, fileList2, index) {
		// 	this.$HTTP(this.$httpConfig.delGoodsImgCofig, {
		// 		fileName: file.response.data,
		// 		sessionToken: this.uploadData.sessionToken,
		// 		imageToken: this.uploadData.imageToken
		// 	}, 'post').then(res => {
		// 		//找到删除的图片并在数据里删除
		// 		let index = this.uploadFile2.indexOf(file.response.data);
		// 		this.uploadFile2.splice(index, 1);
		// 		this.$message.success(res.data.message);
		// 	}).catch(function (error) {
		// 		console.log(error);
		// 	});
		// },
		// // 上传之前
		// beforeUploade2(file) {
		// 	this.uploadData.sessionToken = this.sToken;
		// 	this.uploadData.imageToken = this.imageToken;
		// 	const isLt2M = file.size / 1024 / 1024 < 3;
		// 	if (!isLt2M) {
		// 		this.$message.error("上传头像图片大小不能超过 2MB!");
		// 	}
		// 	return isLt2M;
		// },
		// //显示
		// handlePictureCardPreview2(file) {
		// 	this.dialogImageUrl2 = file.url;
		// 	this.dialogVisible2 = true;
		// },
		// // 上传成功
		// success2(response, file, fileList2) {
		// 	// console.log(response)
		// 	this.$message.success(response.message);
		// 	if (response.status == 0) {
		// 		let length = fileList2.length;
		// 		let i = 0;
		// 		for (i; i < length; i++) {
		// 			if (fileList2[i].name === file.name) {
		// 				fileList2.splice(i, 1);
		// 			}
		// 		}
		// 	} else {
		// 		this.uploadFile2.push(response.data);
		// 	}
		// },
		// //超出文件个数
		// exceeding2(files, fileList2) {
		// 	if (fileList2.length == 1) {
		// 		this.$message({
		// 			duration: 1000,
		// 			type: 'error',
		// 			message: '超出最大文件个数!'
		// 		});
		// 	}
		// },

		// handleRemove3(file, fileList3, index) {
		// 	this.$HTTP(this.$httpConfig.delGoodsImgCofig, {
		// 		fileName: file.response.data,
		// 		sessionToken: this.uploadData.sessionToken,
		// 		imageToken: this.uploadData.imageToken
		// 	}, 'post').then(res => {
		// 		//找到删除的图片并在数据里删除
		// 		let index = this.uploadFile3.indexOf(file.response.data);
		// 		this.uploadFile3.splice(index, 1);
		// 		this.$message.success(res.data.message);
		// 	}).catch(function (error) {
		// 		console.log(error);
		// 	});
		// },
		// // 上传之前
		// beforeUploade3(file) {
		// 	this.uploadData.sessionToken = this.sToken;
		// 	this.uploadData.imageToken = this.imageToken;
		// 	const isLt2M = file.size / 1024 / 1024 < 3;
		// 	if (!isLt2M) {
		// 		this.$message.error("上传头像图片大小不能超过 2MB!");
		// 	}
		// 	return isLt2M;
		// },
		// //显示
		// handlePictureCardPreview3(file) {
		// 	this.dialogImageUrl3 = file.url;
		// 	this.dialogVisible3 = true;
		// },
		// // 上传成功
		// success3(response, file, fileList3) {
		// 	// console.log(response)
		// 	this.$message.success(response.message);
		// 	if (response.status == 0) {
		// 		let length = fileList3.length;
		// 		let i = 0;
		// 		for (i; i < length; i++) {
		// 			if (fileList3[i].name === file.name) {
		// 				fileList3.splice(i, 1);
		// 			}
		// 		}
		// 	} else {
		// 		this.uploadFile3.push(response.data);
		// 	}
		// },
		// //超出文件个数
		// exceeding3(files, fileList3) {
		// 	if (fileList3.length == 1) {
		// 		this.$message({
		// 			duration: 1000,
		// 			type: 'error',
		// 			message: '超出最大文件个数!'
		// 		});
		// 	}
		// },

		// 删除回调
		handleRemove(file, fileList, index) {
			this.$HTTP(this.$httpConfig.delGoodsImgCofig, {
				fileName: file.response.data,
				sessionToken: this.uploadData.sessionToken,
				imageToken: this.uploadData.imageToken
			}, 'post').then(res => {
				//找到删除的图片并在数据里删除
				let index = this.uploadFile.indexOf(file.response.data);
				this.uploadFile.splice(index, 1);
				this.$message.success(res.data.message);
			}).catch(function (error) {
				console.log(error);
			});
		},
		// 上传之前
		beforeUploade(file) {
			this.uploadData.sessionToken = this.sToken;
			this.uploadData.imageToken = this.imageToken;
			const isLt2M = file.size / 1024 / 1024 < 3;
			if (!isLt2M) {
				this.$message.error("上传头像图片大小不能超过 2MB!");
			}
			return isLt2M;
		},
		//显示
		handlePictureCardPreview(file) {
			this.dialogImageUrl = file.url;
			this.dialogVisible = true;
		},
		// 上传成功
		success(response, file, fileList) {
			// console.log(response)
			this.$message.success(response.message);
			if (response.status == 0) {
				let length = fileList.length;
				let i = 0;
				for (i; i < length; i++) {
					if (fileList[i].name === file.name) {
						fileList.splice(i, 1);
					}
				}
			} else {
				this.uploadFile.push(response.data);
			}
		},
		//超出文件个数
		exceeding(files, fileList) {
			if (fileList.length == 1) {
				this.$message({
					duration: 1000,
					type: 'error',
					message: '超出最大文件个数!'
				});
			}
		},
		// 添加图片
		addPicture() {
			this.$HTTP(this.$httpConfig.addGoodsPic, { pic_url: this.uploadFile }, 'post').then(function (res) {
				this.$message.success(res.data.message);
			});
		},
		tolink() {
			this.$router.push({
				name: 'addGrade',
				// params: {
				//     status: 0
				// }
			});
		},
		submit() {
			// let effect_time = '';
			// let start_time = '';
			// let end_time = '';
			// effect_time = this.effect_time.substring(0, this.effect_time.indexOf(':'));
			// if (effect_time[0] == 0) {
			// 	effect_time = effect_time.substring(1);
			// }
			// start_time = this.start_time.substring(0, this.start_time.indexOf(':'));
			// if (start_time[0] == 0) {
			// 	start_time = start_time.substring(1);
			// }
			// end_time = this.end_time.substring(0, this.end_time.indexOf(':'));
			// if (end_time[0] == 0) {
			// 	end_time = end_time.substring(1);
			// }
			// if (this.uploadFile1[0]) {
			// this.electronic_version = this.uploadFile1[0];
			// }
			// else {
			// 	this.electronic_version = this.electronic_version;
			// }
			// if (this.uploadFile2[0]) {
			// this.brand_agent_img = this.uploadFile2[0];
			// }
			// else {
			// 	this.brand_agent_img = this.brand_agent_img;
			// }
			// if (this.uploadFile3[0]) {
			// this.categroy_img = this.uploadFile3[0];
			// }
			// else {
			// 	this.categroy_img = this.categroy_img;
			// }
			if (this.uploadFile[0]) {
			this.store_logo = this.uploadFile[0];
			}
			else {
				this.store_logo = this.store_logo;
			}
			var act_address = {
				prov: this.prov_id,
				city: this.city_id,
				dist: this.dist_id,
			}
			this.$HTTP(this.$httpConfig.saveStoreInfo, {
				shop_name: this.shop_name,
				company_name: this.company_name,
				code: this.code,
				name: this.name,
				enterprise_type: this.enterprise_type,
				registered_capital: this.registered_capital,
				electronic_version: this.electronic_version,
				bus_name: this.bus_name,
				mobile: this.mobile,
				invoice: this.invoice,
				buy: this.buy,
				store_state: this.store_state,
				// effect_time: effect_time,
				effect_time: this.effect_time,
				brand_agent: this.brand_agent,
				brand_agent_img: this.brand_agent_img,
				categroy: this.categroy,
				categroy_img: this.categroy_img,
				remarks: this.remarks,
				store_sales: this.store_sales,
				store_collect: this.store_collect,
				// store_sort: this.store_sort,
				// is_own: this.is_own,
				// status: this.status,
				// shop_long: this.shop_long,
				user_name: this.user_name,
				// description: this.description,
				// start_time: start_time,
				// end_time: end_time,
				register_address: this.register_address,
				prov: this.prov,
				city: this.city,
				dist: this.dist,
				address: this.actual_address,
				actual_address: act_address,
				// prov_id: this.prov_id,
				// city_id: this.city_id,
				// dist_id: this.dist_id,
				store_logo: this.store_logo,
				store_address: this.store_address,
			}, 'post').then((res) => {
				this.$message({
					duration: 1000,
					type: 'success',
					message: res.data.message
				});
				this.invoking();
			}).catch((err) => {
				this.$message.error(err);
			});
		},
	},
	filters: {
		glqe: function (value) {
			let arr = ['是', '否'];
			return typeof (value);
		}
	}
}
</script>
<style>
.classify {
  padding-bottom: 50px;
}
.submit-box {
  text-align: center;
}
.updata_image {
  margin-left: 10px;
}
.el-upload--picture-card i {
  line-height: 148px;
}
.avatar-uploader .el-upload {
  border: 1px dashed #d9d9d9;
  border-radius: 6px;
  cursor: pointer;
  position: relative;
  overflow: hidden;
}
.avatar-uploader .el-upload:hover {
  border-color: #ff920b;
}
.avatar-uploader-icon {
  font-size: 28px;
  color: #8c939d;
  width: 178px;
  height: 178px;
  line-height: 178px;
  text-align: center;
}
.avatar {
  width: 178px;
  height: 178px;
  display: block;
}
.el-upload__input {
  display: none !important;
}
</style>
<style lang="less">
body {
  overflow: inherit;
}
.g_att {
  .t_title {
    color: #333;
    border-bottom: 1px solid #dddddd;
    overflow: hidden;
    margin-bottom: 22px;
    line-height: 50px;
    span {
      float: left;
      color: #333;
    }
    .t_add {
      background: url(../../../../assets/plus2.jpg) no-repeat 15px #ff9f24;
      width: 135px;
      height: 32px;
      border: 1px solid #ff920b;
      border-radius: 4px;
      font-size: 12px;
      font-weight: normal;
      cursor: pointer;
      color: #fff;
      line-height: 32px;
      text-indent: 35px;
    }
  }
  .heading {
    border: none;
    line-height: 30px;
    margin: 10px 0 10px 10px;
  }
  .el-date-editor.el-input,
  .el-date-editor.el-input__inner {
    width: 100px;
  }
}

.el-switch {
  .el-switch__core {
    width: 35px !important;
    height: 16px;
    .el-switch__button {
      width: 11px;
      height: 11px;
    }
  }
  .el-switch__label {
    color: #a4a5a7;
  }
  .el-switch__label.is-active {
    color: #f7bc0a;
  }
  .el-switch__label span {
    line-height: 20px;
    font-size: 12px;
  }
}
</style>
<style type="text/css">
#address .el-input {
  width: 500px;
}

.el-table td,
.el-table th.is-leaf {
  text-align: center;
}
</style>
<style lang="less" scoped>
.classify {
  width: 1000px;
  .g_att {
    .info {
      .el-input {
        width: 500px;
      }
    }
    .list {
      margin-top: 15px;
      tr {
        td {
          padding: 15px 0;
          input,
          select {
            padding-left: 5px;
            width: 288px;
            height: 32px;
            border: 1px solid #cccccc;
          }
          select {
            width: 180px;
          }
          .none {
            padding: 0;
            height: 80px;
          }
          .none_z {
            height: 50px;
            padding: 0;
          }
          .none_x {
            height: 35px;
            padding: 0;
          }
          img {
            background-color: #fbfdff;
            border: 1px dashed #c0ccda;
            border-radius: 6px;
            box-sizing: border-box;
            width: 148px;
            height: 148px;
            line-height: 146px;
            vertical-align: top;
            float: left;
            margin-right: 5px;
          }
          p {
            padding: 10px 0;
          }
          b {
            color: #ff0000;
          }
          textarea {
            padding-left: 5px;
            padding-top: 5px;
            min-height: 80px;
            border: 1px solid #cccccc;
          }
          .Settled {
            height: 32px;
            line-height: 32px;
            color: #fff;
            text-align: center;
            display: block;
            border-radius: 6px;
            margin-top: 20px;
            float: left;
            margin-right: 20px;
            cursor: pointer;
          }
        }
      }
    }
    .manage {
      margin-top: 15px;
      tr {
        td {
          padding: 15px 0;
          .time {
            border-left: 1px solid #ddd;
            border-right: 1px solid #ddd;
            border-top: 1px solid #ddd;
            tr {
              td {
                border-bottom: 1px solid #ddd;
                padding: 10px 0;
                .up_time {
                  padding-left: 10px;
                }
              }
              .right-border {
                border-right: 1px solid #ddd;
              }
            }
          }
        }
      }
    }
  }
  .info-s {
    display: none;
  }
}
</style>
