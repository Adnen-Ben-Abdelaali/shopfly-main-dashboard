<template>
  <div>
    <en-table-layout
      :toolbar="false"
      :pagination="false"
      :tableData="tableData.data"
      :loading="loading"
      border
    >
      <template slot="table-columns">
        <el-table-column prop="order_num" label="Purchase frequency"/>
        <el-table-column prop="member_num" label="Number of single members"/>
        <el-table-column prop="percent" label="The number of"/>
      </template>
    </en-table-layout>
  </div>
</template>

<script>
  import * as API_Statistics from '@/api/customerPriceDistribution'

  export default {
    name: 'customerPriceDistributionFrequency',
    props: ['params', 'curTab'],
    data() {
      return {
        loading: false,
        /** The list of data*/
        tableData: ''
      }
    },
    watch: {
      curTab: 'GET_CustomerPriceDistributionFrequency',
      params: {
        handler: 'GET_CustomerPriceDistributionFrequency',
        deep: true
      }
    },
    methods: {
      GET_CustomerPriceDistributionFrequency() {
        if (this.curTab !== 'frequency' || this.loading) return
        this.loading = true
        API_Statistics.getBuyFrequency(this.params).then(response => {
          this.loading = false
          this.tableData = response
        }).catch(() => { this.loading = false })
      }
    }
  }
</script>
