<template>
  <div>
 
    <base-header class="pb-6 pb-8 pt-5 pt-md-8 bg-gradient-danger">
      <!-- Card stats -->
      <b-row>
        <b-col xl="3" md="6">
        
          <stats-card title="พนักงานทั้งหมด"
                      type="gradient-red"
                      icon="ni ni-active-40"
                      class="mb-4"
                      >
                       <h3>พนักงานทั้งหมด</h3>
          <span   class="type" > {{sumuser}} </span>
          
            <template slot="footer">
           
              <span class="text-success mr-2">  {{sumuser}} </span>
              <span class="text-nowrap"> พนักงานทั้งหมด </span>
            </template>
          </stats-card>
        </b-col>
        <b-col xl="3" md="6">
          <stats-card title="รายงาน KPI"
                      type="gradient-orange"
                 
                      icon="ni ni-chart-pie-35"
                      class="mb-4">
                      <h3>รายงาน KPI</h3>
 <span   class="type" > {{sumdata}} </span>
            <template slot="footer">
              <span class="text-success mr-2"> {{sumdata}} </span>
              <span class="text-nowrap"> KPIทั้งหมด</span>
            </template>
          </stats-card>
        </b-col>
        <b-col xl="3" md="6">
          <stats-card title="ตำแหน่งงาน"
                      type="gradient-green"
                    
                      icon="ni ni-money-coins"
                      class="mb-4">
                         <h3>รายงาน การลา</h3>
 <span  v-for="usercount in usercount " :key="usercount" class="type" > {{usercount}} </span>
            <template slot="footer">
              <span class="text-danger mr-2">5.72%</span>
              <span class="text-nowrap">Since last month</span>
            </template>
          </stats-card>
    
        </b-col>
        <b-col xl="3" md="6">
          <stats-card title="Performance"
                      type="gradient-info"
                      sub-title="49,65%"
                      icon="ni ni-chart-bar-32"
                      class="mb-4">
                      <h3>รายงาน การสาย</h3>
 <span  v-for="usercount in usercount " :key="usercount" class="type" > {{usercount}} </span>
            <template slot="footer">
              <span class="text-success mr-2">54.8%</span>
              <span class="text-nowrap">Since last month</span>
            </template>
          </stats-card>
        </b-col>
      </b-row>
    </base-header>

    <!--Charts-->
    <b-container fluid class="mt--7">
      <b-row>
        <b-col xl="8" class="mb-5 mb-xl-0">
          <card type="default" header-classes="bg-transparent">
            <b-row align-v="center" slot="header">
              <b-col>
                <h6 class="text-light text-uppercase ls-1 mb-1">Overview</h6>
                <h5 class="h3 text-white mb-0">จำนวน kpi</h5>
              </b-col>
              <b-col>
                <b-nav class="nav-pills justify-content-end">
                  <b-nav-item
                       class="mr-2 mr-md-0"
                       :active="bigLineChart.activeIndex === 0"
                       link-classes="py-2 px-3"
                       @click.prevent="initBigChart(0)">
                      <span class="d-none d-md-block">Month</span>
                      <span class="d-md-none">M</span>
                  </b-nav-item>
                  <b-nav-item
                    link-classes="py-2 px-3"
                    :active="bigLineChart.activeIndex === 1"
                    @click.prevent="initBigChart(1)"
                  >
                    <span class="d-none d-md-block">Week</span>
                    <span class="d-md-none">W</span>
                  </b-nav-item>
                </b-nav>
              </b-col>
            </b-row>
            <line-chart
              :height="350"
              ref="bigChart"
              :chart-data="bigLineChart.chartData"
              :extra-options="bigLineChart.extraOptions"
            >
            </line-chart>
          </card>
        </b-col>

        <b-col xl="4" class="mb-5 mb-xl-0">
          <card header-classes="bg-transparent">
            <b-row align-v="center" slot="header">
              <b-col>
                <h6 class="text-uppercase text-muted ls-1 mb-1">Performance</h6>
                <h5 class="h3 mb-0">Total User</h5>
              </b-col>
            </b-row>

            <bar-chart
              :height="350"
              ref="barChart"
              :chart-data="redBarChart.chartData"
            >
            </bar-chart>
          </card>
        </b-col>
      </b-row>
      <!-- End charts-->

      <!--Tables-->
      <b-row class="mt-5">
        <b-col xl="8" class="mb-5 mb-xl-0">
          <page-visits-table></page-visits-table>
        </b-col>
     
      </b-row>
      <!--End tables-->
    </b-container>

  </div>
</template>
<script>
import axios from "axios";
  // Charts
  import * as chartConfigs from '@/components/Charts/config';
  import LineChart from '@/components/Charts/LineChart';
  import BarChart from '@/components/Charts/BarChart';

  // Components
  import BaseProgress from '@/components/BaseProgress';
  import StatsCard from '@/components/Cards/StatsCard';

  // Tables
  import SocialTrafficTable from './Dashboard/SocialTrafficTable';
  import PageVisitsTable from './Dashboard/PageVisitsTable';

  export default {
    
    components: {
      LineChart,
      BarChart,
      BaseProgress,
      StatsCard,
      PageVisitsTable,
      SocialTrafficTable
    },
        async  created() {
  
    await axios.get("http://localhost:3000/admin/emp_alluserscconut").then((res) => {
      this.usercount= res.data;
     
    });
      await  axios.get("http://localhost:3000/admin/kpi_count").then((res) => {
      this.kpi_counts= res.data;
     
    });
  },
    data() {
      return {
        kpi_counts:[],
       usercount:[],
        bigLineChart: {
          kpi_counts: [
         
          ],
          activeIndex: 0,
          chartData: {
            datasets: [
              {
                label: 'Performance',
                data: [0,700, 800],
              }
            ],
            labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug','Sep','Oct','Nov','Dec'],
          },
          extraOptions: chartConfigs.blueChartOptions,
        },
        redBarChart: {
          chartData: {
            labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug','Sep','Oct','Nov','Dec'],
            datasets: [{
              label: 'user',
              data: [100, 800]
            }]
          },
          extraOptions: chartConfigs.blueChartOptions
        }
      };
    },
    methods: {
      initBigChart(index) {
        let chartData = {
          datasets: [
            {
              label: 'Performance',
              data: this.bigLineChart.allData[index]
            }
          ],
          labels: ['May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
        };
        this.bigLineChart.chartData = chartData;
        this.bigLineChart.activeIndex = index;
      }
    },
    mounted() {
      this.initBigChart(0);
    },

    matDatacout:{

    },
     computed: {
 sumdata:function(){
   return this.kpi_counts
 },
 sumuser:function(){
   return this.usercount
 }
  },
  };

</script>
<style>
.type{
  font-weight: bold;
  font-size: 3em;
}
.el-table .cell{
  padding-left: 0px;
  padding-right: 0px;
}
</style>
