<template>
  <div style="padding:30px;">
    <el-calendar>
      <template slot="dateCell" slot-scope="{date, data}">
        <div class="cal-container">
          <div v-if="data.isSelected" style="float: right;color: #67C23A"><i class="el-icon-circle-plus"></i></div>
          <div class="cal-svg">
            <lcd-number :number="date.getDate()" :color="getColor(data,date)"></lcd-number>
          </div>
          <div class="svg-right">
              <div class="svg-right-div">左侧上部分</div>
              <div class="svg-right-div">下部分</div>
          </div>
          <div class="svg-bottom">
            <div>底部文本厂服</div>
          </div>
        </div>
      </template>
    </el-calendar>


  </div>
</template>
<script>
import LcdNumber from '@/components/LcdNumber'
export default {
  components: {
    LcdNumber
  },
  data() {
    return {
      value: new Date(),
      color:{
        noCurrentMonth:"#F2F6FC",
        currentMonth:"#DCDFE6",
        today:"#409EFF"
      }

    }
  },
  methods:{
    getColor(data,date){
      return data.type === 'current-month'?(
        data.isSelected||(date.getDate() === new Date().getDate() && date.getFullYear() === new Date().getFullYear() && date.getMonth() === new Date().getMonth())?this.color.today:this.color.currentMonth
      ):this.color.noCurrentMonth
    }
  }
}
</script>
<style scoped lang="scss">
.cal-container{
  position: relative;
  .cal-svg{
    text-align: center;position: absolute;z-index: 0;margin-top: 16px;
  }
  .svg-right{
    position: absolute;z-index: 99999;margin-left: 40px;margin-top: 10px;
    .svg-right-div{
      line-height: 16px;height: 16px;margin-top: 5px
    }
  }
  .svg-bottom{
    position: absolute;z-index: 99999;margin-top: 55px;
  }
}
@media screen and (max-width: 600px) {
  .svg-right {
    display: none;
  }
}
</style>
