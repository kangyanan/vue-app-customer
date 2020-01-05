<template>
    <briup-fulllayout title="常用地址">
    <van-list>  
        <!-- --{{address}} -->
        <!-- --{{info}} -->
        <van-cell
            v-for="item in address"
            :key="item.id"
            :title="item.province+item.city+item.area+item.address"
        />
    </van-list>
    <br/>
    <van-button block type="default"  color="#7232dd" @click="toAddressEditHandler">添加</van-button>
  
      
    </briup-fulllayout>
</template>

<script>
import {get} from '../../../http/axios'
import {mapState} from 'vuex'
export default {
    data(){
    return {
     address:[]
      
    }
  },
  computed:{//计算属性
      //将状态机中的user对象中的info对象获取到
      ...mapState("user",["info"])

  },
    created(){
        this.loadAddress();

    },
    methods:{
        loadAddress(){
            let id=this.info.id;
            let url="/address/findByCustomerId?id="+id;
            get(url).then((response)=>{
                this.address=response.data;
            })
        },
        toAddressEditHandler(){
            this.$router.push("/manager/address_edit");

        }

    }
    
}
</script>