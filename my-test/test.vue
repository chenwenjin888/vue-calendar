<template>
  <div class="position-relative height-100">
    <!--start 日期-->
    <calendar ref="calendar" :range="calendar.range" :zero="calendar.zero" :value="calendar.value"
              @confirm="calendar.confirm" @showCalendar="calendar.showCalendar"></calendar>
    <!--end 日期-->
  </div>
</template>
<script>
  import calendar from './calendar.vue' // 日历组件
  export default{
    data(){
      return {
        startDate: '',
        endDate: '',
        calendar: {
          range: true,// 范围模式
          zero: true,// 小于10补零
          value: [], //默认日期
          confirm: (begin, end) => { // 确定
            if (begin.length != 0 || end.length != 0) {
              this.calendar.value = [begin, end];
            }
            this.params.startTime = begin.join('-');
            this.params.endTime = end.join('-');
            this.params.pageNo = 1;

            // 取值后操作
          },
          showCalendar: () => {
            if (!this.startDate) return;
            this.calendar.value = [this.startDate.split('-'), this.endDate.split('-')];
          }
        }
      }
    },
    components: {
      calendar
    },
    methods: {
      // 显示日期
      showCalendar(){
        this.$refs.calendar.showCalendar();
      }
    }
  }
</script>
<style scoped>
</style>
