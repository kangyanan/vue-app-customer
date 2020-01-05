<template>
    <briup-fulllayout title="新增地址">
    
    <div>
        {{form}}
        <van-cell-group>
            <van-field v-model="from.telephone" placeholder="请输入手机号" />
        </van-cell-group>
         <van-cell-group>
            <van-field v-model="from.province" placeholder="省" />
        </van-cell-group>
         <van-cell-group>
            <van-field v-model="from.city" placeholder="市" />
        </van-cell-group>
         <van-cell-group>
            <van-field v-model="from.area" placeholder="区" />
        </van-cell-group>
         <van-cell-group>
            <van-field v-model="from.address" placeholder="请输入详细地址" />
        </van-cell-group>
        <van-button block type="primary" @click="submitHandler">保存</van-button>
    </div>
    </briup-fulllayout>
</template>
<script>
import {mapState} from 'vuex';
import { post } from '../../../http/axios';

export default {
    data(){
        return {
            from:{}
        }

    },
    computed:{
        ...mapState('user',['info'])

    },
    methods:{
        submitHandler(){
            let url="/address/saveOrUpdate"
            //提交前，将当前登陆者id作为顾客id
            this.from.customerId=this.info.id;
            post(url,this.from).then((response)=>{
                //返回上一级
                this.$router.go(-1);
                //轻提示
                this.$toast.success(response.message);


            })
        }
    }
    
}
</script>