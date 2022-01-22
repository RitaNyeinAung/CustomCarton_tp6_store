<template>
	<div class="logistics fl">
		<!-- 客服-添加客服管理 -->
		<div class="t_tab">
			<h1 class="t_title">
            <span v-if="!status" class="size16">客服管理 - 添加</span>
            <span v-else class="size16">客服管理 - 修改</span>
            <div class="t_m fr" @click="to">返回客服列表</div>
        </h1>
			<table width="100%" border="0" cellspacing="0" cellpadding="0" class="logistics_x">
				<tr>
					<td align="right" class="black"><b>*</b>客服帐号：</td>
					<td>
						<el-select style="width: 400px;" v-model="params.user_id" placeholder="请选择">
							<el-option v-for="(item, key) in options" :key="key" :label="item.seller_name"
                         :value="item.user_id">
              </el-option>
						</el-select>
					</td>
				</tr>
				<tr>
					<td align="right" class="black">是否启用：</td>
					<td>
						<el-switch v-model="params.status" inactive-text="否" active-text="是" active-color="#f7bc0a">
						</el-switch>
					</td>
				</tr>
				<tr>
					<td align="right" class="black"><b>*</b>排序：</td>
					<td>
						<el-input style="width: 400px;" v-model="params.sort" clearable></el-input>
						<span class="notes">数字范围 0~255 ，数字越小越靠前</span>
					</td>
				</tr>
				<tr>
					<td align="right">&nbsp;</td>
					<td colspan="2">
						<el-button v-if="!status" type="success" @click="submit">确认添加</el-button>
						<el-button v-else type="success" @click="saveData">确认修改</el-button>
					</td>
				</tr>
			</table>
		</div>
	</div>
</template>
<script>
	export default {
		name: 'addservicemanage',
		data() {
			return {
				status: 0, //0代表是新增，1代表是修改
				classData: {}, // 一级分类
				params: {
					status: 0,
					// tool: '',
					sort: 0,
					user_id:''
				},
				options: '',
				id: 0
			}
		},
		created() {
			this.$HTTP(this.$httpConfig.addServiceConver, {

			}).then((res) => {
				console.log(res);
				this.options = res.data.data;
				console.log(this.options);
			}).catch((err) => {
				console.log(err);
			})
		},
		mounted() {
			this.status = this.$route.params.status;
			if(this.status) {
				/*修改*/
				this.id = this.$route.params.id;
				this.queryData();
			}

			//this.getClass();
		},
		methods: {
			fn() {
        console.log(this.params.user_name)
				this.options.forEach((item,index)=>{
					// if(item.seller_name = this.params.seller_name){
					// 	this.params.user_id = item.user_id
					// }
          console.log(item);
						this.params.user_id = item.user_id
				})
			},
			setCode(event){
				// console.log(event)
				return event.keyCode>=48&&event.keyCode<=57
			},
			to() {
				this.$router.back();
			},
			toAdd(){
				/*跳转到添加客服类型页面*/
				this.$router.push('/addservicetype');
			},
			queryData() {

				this.$HTTP(this.$httpConfig.getServiceDetail,{service_id : this.id}).then((res)=>{
					console.log(res);
					this.params = res.data.data;
					this.params.status = res.data.data.status==1?true:false;
					this.$message.success(res.data.message);
				}).catch((err)=>{
					this.$message.error(err.data.message);
				});
			},
			// getClass() {
			// 	// //获取客服类型
            // 	// this.$HTTP(this.$httpConfig.getServiceTypeList,{}).then((res) => {
			// 	// 	if(!res.data.data) {
			// 	// 		this.$layer.msg('暂无数据:(');
			// 	// 		return;
			// 	// 	}
			// 	// 	this.classData = res.data.data;
			// 	// }).catch((err) => {
			// 	// 	console.log(err)
			// 	// });
			// },
			submit() {
				this.params.status = Number(this.params.status);
				if(this.status) {
					this.params.service_id = this.id;
				} else {
					delete this.params.service_id;
				}
				this.$HTTP(this.$httpConfig.addService,this.params).then((res) => {
					this.$router.go(-1)
					this.$message.success(res.data.message);
				}).catch((err) => {
					this.$message.error(err.data.message);
				})
			},
      saveData() {
        this.params.status = Number(this.params.status);
        if(this.status) {
          this.params.service_id = this.id;
        } else {
          delete this.params.service_id;
        }
        this.$HTTP(this.$httpConfig.saveService,this.params).then((res) => {
          this.$router.go(-1)
          this.$message.success(res.data.message);
        }).catch((err) => {
          this.$message.error(err.data.message);
        })
      }
		}
	}
</script>
<style lang="less">
	.t_tab {
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
		}
	}

	.el-switch {
		height: 20px;
		.el-switch__core {
			width: 35px!important;
			height: 20px;
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

<style lang="less" scoped>
	.logistics {
		width: 1000px;
		padding-bottom:80px;
		.t_m {
			background: url(../../../../assets/return.jpg) no-repeat 20px #ff9f24;
			width: 135px;
			height: 32px;
			border: 1px solid #ff920b;
			border-radius: 4px;
			font-size: 12px;
			font-weight: normal;
			cursor: pointer;
			color: #FFF;
			line-height: 32px;
			text-indent: 40px;
		}
		.Commodity-management {
			background-color: #f6f6f6;
			border: 1px solid #dddddd;
			margin-top: 15px;
			line-height: 50px;
			margin-bottom: 20px;
			input {
				width: 140px;
				border: 1px solid #ddd;
				line-height: 29px;
				height: 29px;
				color: #999;
				text-indent: 5px;
			}
		}
		.bold {
			font-weight: bold;
		}
		.black {
			color: #333;
		}
		.logistics_x {
			tr {
				td {
					padding: 10px 0;
					.ss {
						margin: 0;
					}
					b {
						color: #ff0000;
					}
					.notes {
						padding-left: 15px;
						i {
							cursor: pointer;
							color: #87e1ff;
						}
					}
					input,
					select {
						text-indent: 5px;
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
					.abstract {
						min-height: 70px;
					}
					.Settled {
						height: 32px;
						line-height: 32px;
						color: #FFF;
						text-align: center;
						display: block;
						border-radius: 6px;
						margin-top: 30px;
						float: left;
						margin-right: 20px;
						cursor: pointer;
					}
				}
			}
		}
	}
</style>
