<template>
  <div class="app-container">
    <el-row :gutter="20">
      <el-button @click="add" class="el-icon-plus" type="primary" round> 添加</el-button>
      <el-button @click="edit" class="el-icon-edit" type="primary" round> 修改</el-button>
      <el-button @click="deleted" class="el-icon-close" type="primary" round> 删除</el-button>
    </el-row>

    <el-table :data="list" v-loading.body="listLoading" element-loading-text="Loading" border fit highlight-current-row>
      <el-table-column align="center" label='ID' width="95">
        <template slot-scope="scope">
          {{scope.$index+1}}
        </template>
      </el-table-column>
      <el-table-column label="登陆账号">
        <template slot-scope="scope">
          {{scope.row.username}}
        </template>
      </el-table-column>
      <el-table-column label="昵称"  align="center">
        <template slot-scope="scope">
          <span>{{scope.row.realname}}</span>
        </template>
      </el-table-column>
      <el-table-column label="Email" align="center">
        <template slot-scope="scope">
          {{scope.row.email}}
        </template>
      </el-table-column>
      <el-table-column class-name="status-col" label="状态"  align="center">
        <template slot-scope="scope">
          <el-tag :type="scope.row.status | statusFilter">{{scope.row.status}}</el-tag>
        </template>
      </el-table-column>
      <el-table-column align="center" prop="createTime" label="创建时间" >
        <template slot-scope="scope">
          <i class="el-icon-time"></i>
          <span>{{scope.row.createTime}}</span>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
import { getList } from '@/api/user'

export default {
  data() {
    return {
      list: null,
      listLoading: true
    }
  },
  filters: {
    statusFilter(status) {
      const statusMap = {
        published: 'success',
        draft: 'gray',
        deleted: 'danger'
      }
      return statusMap[status]
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    add: function() {
      alert('Hello !')
    },
    edit: function() {
      alert('Hello !')
    },
    deleted: function() {
      alert('Hello !')
    },
    fetchData() {
      debugger
      this.listLoading = true
      getList(this.listQuery).then(response => {
        debugger
        this.list = response.data
        this.listLoading = false
      })
    }
  }
}
</script>
