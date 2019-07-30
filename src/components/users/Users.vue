<template>
  <div>
    <el-table
      :data="tableData"
      style="width: 100%"
    >
      <el-table-column
        prop="username"
        label="用户名"
        width="180"
      >
      </el-table-column>
      <el-table-column
        prop="mobile"
        label="手机号"
        width="180"
      >
      </el-table-column>
      <el-table-column
        prop="email"
        label="邮箱"
      >
      </el-table-column>
      <el-table-column
        prop="hah"
        label="状态"
      >
      </el-table-column>
      <el-table-column
        prop="ha"
        label="操作"
      >
      </el-table-column>
    </el-table>
    <!-- 分页 -->
    <el-pagination
      background
      layout="prev, pager, next"
      :total="total"
      :page-size='2'
      :current-page='pagenum'
      @current-change='currentChanged'
    >
    </el-pagination>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      tableData: [{
        mobile: '14293837341',
        username: 'nangerer',
        email: '4347832@qq.com'
      }
      ],
      total: 0,
      pagenum: 1

    }
  },
  created () {
    this.renderTable()
  },
  methods: {
    renderTable (pagenum = 1) {
      axios.get('http://localhost:8888/api/private/v1/users', {
        params: {
          query: '',
          pagenum,
          pagesize: 2
        },
        headers: {
          Authorization: localStorage.getItem('token')
        }
      }).then(res => {
        // console.log(res.data.data)
        console.log(res)
        this.total = res.data.data.total
        this.pagenum = res.data.data.pagenum
        this.tableData = res.data.data.users
      })
    },
    currentChanged (curPage) {
      this.renderTable(curPage)
    }
  }
}
</script>

<style>
</style>
