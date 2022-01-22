<template>
  <div class="offerManage">
    <div class="g_att">
      <h1 class="t_title">
        <span class="size16">已报价- 列表</span>
      </h1>
    </div>
    <div class="order_seek">
      <div class="crux clearfix">
        <div class="seek_l">
            <div>
                项目编号 ：
                <el-input
                    v-model="item"
                    clearable
                    style="width: 150px;height: 30px;"
                >
                </el-input>
            </div>
        </div>
        <div class="seek_l">
            <div>
                项目名称 ：
                <el-input
                    v-model="item1"
                    clearable
                    style="width: 150px;height: 30px;"
                >
                </el-input>
            </div>
        </div>
        <!-- <div class="seek_l">
            <div>
                采购组织 ：
                <el-input
                    v-model="item2"
                    clearable
                    style="width: 150px;height: 30px;"
                >
                </el-input>
            </div>
        </div> -->
        <div class="seek_l">
           <el-button
            @click="getList"
            style="float: right;"
            type="success"
            icon="el-icon-search"
            class="search_button"
          >搜索</el-button>
        </div>
      </div>
    </div>
    <div class="listWrapper">
      <h6>
        已报价列表
        <span>( 共 0 条记录 )</span>
      </h6>
      <el-table
        ref="multipleTable"
        :data="projectList"
        style="width: 100%"
        @selection-change="handleSelectionChange">
        <el-table-column
          type="selection"
          width="55">
        </el-table-column>
        <el-table-column
          property="id"
          label="项目编号"
          width="120">
          <template slot-scope="scope">{{ scope.row.id }}</template>
        </el-table-column>
        <el-table-column
          property="title"
          label="项目名称"
          width="200">
        </el-table-column>
        <el-table-column
          property="shop_name"
          label="报价方"
          width="170">
        </el-table-column>
        <el-table-column
          property="create_time"
          label="发布日期"
          width="150">
        </el-table-column>
        <!-- <el-table-column
          property="deadline_time"
          label="报价截止时间"
          width="170">
        </el-table-column> -->
        <el-table-column label="报价截止时间" width="160">
					<template slot-scope="scope">
							<time-Plunge :timePlunge="scope.row.deadline_time"></time-Plunge>
          </template>
				</el-table-column>
        <el-table-column
          label="操作"
          width="143">
          <template slot-scope="scope">
            <!-- <el-button
                size="mini"
                >编辑
            </el-button> -->
            <el-button
                size="mini"
                @click="goToOtherPage(scope.row.id)"
                >查看
            </el-button>
          </template>
        </el-table-column>
      </el-table>
      <div class="Paging">
        <div class="Paging_checkbox">
            <el-checkbox v-model="checked"></el-checkbox>
        </div>
        <div class="fl pil">删除</div>
        <div class="Paging_r">
            <el-pagination
                background
                layout="total,prev, pager, next,jumper"
                :page-size="page_size"
                @current-change="handleCurrentChange"
                :total="page"
            >
            </el-pagination>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import timePlunge from '@/components/page/time';
export default {
  name: "offerManage",
  data() {
    return {
      item: '',
      item1: '',
      // item2: '',
      multipleSelection: [],
      page: 0,
      currentPage: 1,
      page_size: 0,
      checked: false,
      projectList: []
    };
  },
  created() {
    this.getProjiectList();
  },
  methods: {
    getList() {
      this.$HTTP(this.$httpConfig.offerList, {
        id: this.item,
        project_name: this.item1,
        // group_name: this.item2,
      })
      .then(res => {
        this.projectList = res.data.data.data;
        this.page_size = parseInt(res.data.data.page_size);
        this.page = parseInt(res.data.data.page);
      })
      .catch(err => {
        console.log(err);
      });
    },
    handleSelectionChange(val) {
      this.multipleSelection = val;
    },
    handleCurrentChange: function(currentPage) {
      this.currentPage = currentPage;
      this.getProjiectList();
    },
    getProjiectList() {
      this.$HTTP(this.$httpConfig.offerList+ '/page/' + this.currentPage, {
      })
      .then(res => {
        this.projectList = res.data.data.data;
        this.page_size = parseInt(res.data.data.page_size);
        this.page = parseInt(res.data.data.page);
      })
      .catch(err => {
        console.log(err);
      });
    },
    goToOtherPage(id) {
       this.$router.push({
        name: "quotationDetails",
        params: {
          id: id
        }
      });
    },
  },
  components: {
		timePlunge
	},
}
</script>

<style lang="less">
.el-table th > .cell {
    display: inline-block;
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
    position: relative;
    vertical-align: middle;
    padding-left: 14px;
    padding-right: 14px;
    width: 100%;
}
.el-table thead {
    color: #333;
    font-weight: 500;
}
.el-table th, .el-table tr {
    background-color: #F9FAFA;
}
.el-table__row {
    background-color: #fff !important;
    height: 80px;
}
.el-table th > .cell {
    display: inline-block;
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
    position: relative;
    vertical-align: middle;
    padding-left: 14px;
    padding-right: 14px;
    width: 100%;
    color: #333;
}
.el-table_11_column_106 {
    color: #E9573E !important;
}
</style>

<style lang="less" scoped>
.el-table--fit {
    border-right: 1px solid #EBEEF5;
    border-left: 1px solid #EBEEF5;
}
.has-gutter {
  background-color: #F9FAFA;
  color: #333;
}
.offerManage .listWrapper .Paging .Paging_checkbox[data-v-5b591b3e] {
    width: 5%;
    float: left;
    height: 50px;
    padding-top: 13px;
    padding-left: 14px;
}
.offerManage {
  width: 1000px;
  padding-bottom: 80px;
  .g_att {
    .t_title {
      color: #333;
      border-bottom: 1px solid #dddddd;
      overflow: hidden;
      margin-bottom: 15px;
      line-height: 50px;
      span {
        float: left;
        color: #333;
      }
    }
  }
  .order_seek {
    background-color: #f6f6f6;
    border: 1px solid #dddddd;
    margin-top: 15px;
    overflow: hidden;
    line-height: 70px;
    .crux {
      .seek_l {
        overflow: hidden;
        float: left;
        margin-left: 40px;
      }
      div:nth-child(1) {
        margin-left: 7px;
      }
     .search_button {
       margin-top: 17px;
       margin-left: 30px;
       height: 40px;
     }
    }
  }
  .listWrapper {
    h6 {
      border-bottom: 1px solid #e8e8e8;
      padding: 25px 0 10px 0;
      font-size: 16px;
      color: #333;
      span {
        font-size: 12px;
        color: #a4a5a7;
        margin-left: 6px;
      }
    }
    .Paging {
        // width: 100%;
        height: 50px;
        border-left: 1px solid #ddd;
        border-right: 1px solid #ddd;
        border-bottom: 1px solid #ddd;

        .Paging_checkbox {
            width: 5%;
            float: left;
            height: 50px;
            margin: 14px 0 0 14px;

            input {
                display: block;
                margin: auto;
                margin-top: 20px;
            }
        }

        .pil {
            border: 1px solid #e9573e;
            color: #fff;
            text-align: center;
            display: block;
            border-radius: 4px;
            background-color: #e9573e;
            float: left;
            margin-top: 9px;
            cursor: pointer;
            width: 58px;
            height: 32px;
            line-height: 32px;
        }

        .Paging_r {
            float: right;
            // padding: 10px;
            .el-pagination {
              margin-left: 0% !important;
              margin-top: 10px;
          }
        }
    }
  }
}
</style>