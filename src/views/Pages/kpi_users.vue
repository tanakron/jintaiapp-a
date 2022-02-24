<template>
<div>   

   <b-card class="bg-gradient-danger">
        <b-row align-v="center" >
          <b-col cols="8">
            <h3 class="mt-4  text-white">ข้อมูลพนักงานทั้งหมด</h3>
          </b-col>
  
        </b-row>
        
      </b-card>
        
 
        
        <b-button variant="danger" class="mt-4 ml-4 mb-3"   href="#/kpi_form">เพิ่มข้อมูล </b-button>
 <b-table :items ="(items)" :fields="fields" striped responsive="sm">
   
   <template #cell(show_details)="row">
        <b-button size="sm" @click="row.toggleDetails" class="mr-2">
          {{ row.detailsShowing ? 'Hide' : 'Show'}} Details
        </b-button>

        <!-- As `row.showDetails` is one-way, we call the toggleDetails function on @change -->
      
      </template>
            <template #row-details="row">
        <b-card>
          
          <b-row class="mb-2">
            <b-col sm="3" class="text-sm-right"><b>เลขอ้างอิง:</b></b-col>
            <b-col>
              <span>
                {{row.item.kpi_documentnumber}}
              </span>
            </b-col>
          </b-row>

          <b-row class="mb-2">
            <b-col sm="3" class="text-sm-right"><b>ชื่อ พนักงาน:    </b></b-col>
            <b-col>  {{row.item.kpi_name}}</b-col>
          </b-row>

 <b-row class="mb-2">
            <b-col sm="3" class="text-sm-right"><b>ตำแหน่งงาน: </b></b-col>
            <b-col> {{row.item.kpi_department }}</b-col>
          </b-row>

           <b-row class="mb-2">
            <b-col sm="3" class="text-sm-right"><b>วันที่แจ้ง: {{row.item.kpi_datenow }}</b></b-col>
            <b-col> </b-col>
          </b-row>
          <b-row class="mb-2">
            <b-col sm="3" class="text-sm-right"><b>เรื่อง KPI: </b></b-col>
            <b-col> {{row.item.kpi_subject }} </b-col>
          </b-row>
          <b-button size="sm" @click="row.toggleDetails">Hide Details</b-button>
           <b-button size="sm" >แก้ไขข้อมูล</b-button>
                   <b-button size="sm" >ลบ</b-button>

        </b-card>
      </template>
    </b-table>


  
     </div>
</template>
<script>

import axios from "axios";  


  export default {

    async mounted(){
let items = await axios.get("http://localhost:3000/admin/kpi_empuser")
this.items = items.data;
    },
    data() {
      
      return {
      fields: ['emp_id', 'emp_fullname', 'emp_start','show_details'],
  items: 
   {
     emp_url:"http://localhost:3000/backend/img_users/",
   },
  
      };
    },
    computed: {
      rows() {
        return this.items.length
      }
      
    },
 components:{

 },
    mainProps: { blank: true, blankColor: '#777', width: 75, height: 75, class: 'm1'}
    
  }
  
</script>
<style>
.btadd{
  margin-top: 2%;
  margin-bottom: 3%;
}
</style>