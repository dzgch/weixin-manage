<template>
    <div>
        <i-table border  :columns="columns7" :data="data6">
            <template slot-scope="{ row, index }" slot="action">
            <Button type="primary" size="small" style="margin-right: 5px" @click="show(row)">发货</Button>
            <!-- <Button type="primary" size="small" style="margin-right: 5px" @click="removeShow(row)">取消发货</Button> -->
            <!-- <Button type="error" size="small" @click="remove(row)">取消订单</Button> -->
            </template>
        </i-table>
    </div>
</template>
<script>
import { mapActions } from 'vuex'
import {getHour24} from '@/libs/util'
export default {
    name:"yeshandle_order",
    data () {
        return {
            columns7: [
                {
                    title: '商品名称',
                    key: 'rentCommodityName'
                },
                {
                    title: '日期',
                    key: 'makeOrdertime',
                    render(h,params){
                        return h('div',getHour24(params.row.makeOrdertime))
                    }
                },
                {
                    title: '购买人',
                    key: 'ownerName'
                },
                 {
                    title: '地址',
                    key: 'addr'
                },
                 {
                    title: '订单状态',
                    key: 'status'
                },
                  {
                    title: '取消原因',
                    key: 'reason'
                },
                {
                    title: '经销商ID',
                    key: 'distributorID'
                },
                {
                    title: '经销商',
                    key: 'distributorName'
                },
                {
                    title: '支付状态',
                    key: 'status',
                    render (h,params) {
                        let sta=Number(params.row.status)>=1?"已支付":"未支付"
                        return h('div',sta);
                    }
                },
                {
                    title: '订单数量',
                    key: 'count'
                }
            ],
            data6: []
        }
    },
    mounted(){
        this.getNoOrder()
    },
    methods: {
        ...mapActions([
            'getrentorderdo'
        ]),
        getNoOrder(){
            this.getrentorderdo().then(res=>{
                this.data6=res.data||[]
            })
        },
        show (index) {
            this.$Modal.info({
                title: 'User Info',
                content: `Name：${this.data6[index].name}<br>Age：${this.data6[index].age}<br>Address：${this.data6[index].address}`
            })
        },
        remove (index) {
            this.data6.splice(index, 1);
        }
    }
}
</script>

<style lang="less" scoped>

</style>
