<template>
    <div class="z_index" v-loading="loading" style="width: 100%;height:100%;">
        <div v-title data-title="订单管理-订单列表">订单管理-订单列表</div>
        <!-- 头部 -->
         <header-Top></header-Top>
         <!-- 内容 -->
         <div class="content">
             <!-- 左边 -->
             <left :list="$store.state.leftNav"></left>
            <!-- 右边 -->
            <iframe-Label></iframe-Label>
         </div>
         <!-- 脚部 -->
         <Merchant-Foot></Merchant-Foot>
    </div>
</template>
<script>
import headerTop from '@/components/header/top';
import MerchantFoot from '@/components/foot/foot';
import left from '../../page/left' //左边
import iframeLabel from '../../page/iframe' //iframe 
    export default {
        name : 'trade',
        data(){
            return {
                loading: true,
                // list:[{url:'tradeManage',title:'订单管理'},{url:'invoice',title:'发货单管理'},{url:'refund',title:'退款/退货管理'},{url:'evaluate',title:'评价管理'},]
            }
        },
        created(){
            setTimeout(() => {
                this.loading = false;
                }, 500);
        },
          mounted() {

            this.$store.state.link = this.$store.state.leftNav[0].url;
            if(this.$route.query.type  == 'invoice'){
              this.$store.state.link = 'invoice?a=1576483743320'
            }else if(this.$route.query.type  == 'evaluate'){
              this.$store.state.link = 'evaluate?a=1576483743320'
            }else if(this.$route.query.type  == 'refund'){
              this.$store.state.link = 'refund?a=1576483743320'
            }
        },
        methods: {

        },
        components: {
            headerTop,
            MerchantFoot,
            left,
            iframeLabel
        },
    }
</script>
<style lang="less" scoped>
body{
        overflow: inherit;
    }
    .z_index{
        .content{
            width: 1266px;
            color: #a4a5a7;
            margin: 0 auto;
            overflow: hidden;
        }
    }
        
</style>