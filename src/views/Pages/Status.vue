<template>
  <div>

      <b-modal id="bv-modal-example" hide-footer v-bind="insertform.emp_id">
    <template #modal-title>
      บันทึกข้อมูล 
    </template>
    <div class="d-block text-center">

   ID พนักงาน: {{ insertform.emp_id }} <br />
                  ชื่อ-นามสกุล :{{ insertform.emp_fullname }} <br />
                  วันเริ่มงาน: {{ insertform.emp_start }} <br />
                  วันเกิด: {{ insertform.emp_bithday }}<br />
               
    </div>
    <b-button class="mt-3" block @click="$bvModal.hide('bv-modal-example')">ปิด</b-button>
  </b-modal>
  </div>
</template>

<script>
export default {

}
</script>

<style>

</style>