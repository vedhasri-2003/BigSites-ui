<template>
  <div class="div-table">
    <div class="div-table-row">
      <b-message type="is-info" has-icon style="font-size: 12px; max-width: 520px">
        <h5>Welcome to Securo JOBZ!!..</h5>
        <h4>Agent Id : {{ agentEmail }}</h4>
        <h5>Click the "Profile Email" to view the details</h5>
      </b-message>
    </div>
  </div>
</template>
<script>
export default {
  props: ['agentNm', 'agentEmail'],
}
</script>
