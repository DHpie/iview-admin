<template>
  <div>
    <Card>
      <tables ref="tables" editable searchable search-place="top" v-model="tableData" :columns="columns" @on-delete="handleDelete"
      />
      <Button style="margin: 10px 0;" type="primary">导出为Csv文件</Button>
    </Card>
  </div>
</template>

<script>
import Tables from '_c/tables'
import { getTableData } from '@/api/data'

export default {
  name: 'test-proj',
  components: {
    Tables
  },
  data () {
    return {
      tableData: [],
      columns: [
        // {title: 'ID', key: 'id'},
        { title: 'Name', key: 'name', sortable: true },
        { title: 'Email', key: 'email', editable: true },
        { title: 'Create-Time', key: 'createTime' },
        {
          title: 'Handle',
          key: 'handle',
          options: ['delete', 'add'],
          button: [
            (h, params, vm) => {
              return h('Poptip', {
                props: {
                  confirm: true,
                  title: '你确定要删除吗?'
                },
                on: {
                  'on-ok': () => {
                    vm.$emit('on-delete', params)
                    vm.$emit('input', params.tableData.filter((item, index) => index !== params.row.initRowIndex))
                  }
                }
              }, [
                h('Button', '自定义删除')
              ])
            }
          ]
        }
      ]
    }
  },
  methods: {
    handleDelete (params) {
      console.log(params)
    }
  },
  mounted () {
    /* 初始化加载mock数据 */
    getTableData().then(res => {
      this.tableData = res.data
    })
  }

}
</script>

<style scoped>

</style>
