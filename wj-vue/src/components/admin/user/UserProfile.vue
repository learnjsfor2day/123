<template>
  <div>
    <el-row style="margin: 18px 0px 0px 18px ">
      <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item :to="{ path: '/admin/dashboard' }">Management Center</el-breadcrumb-item>
        <el-breadcrumb-item>User Management</el-breadcrumb-item>
        <el-breadcrumb-item>User Information</el-breadcrumb-item>
      </el-breadcrumb>
    </el-row>
    <el-card style="margin: 18px 2%;width: 95%">
      <el-table
        :data="users"
        stripe
        style="width: 100%"
        :max-height="tableHeight">
        <el-table-column
          type="selection"
          width="55">
        </el-table-column>
        <el-table-column
          prop="id"
          label="id"
          width="100">
        </el-table-column>
        <el-table-column
          prop="username"
          label="username"
          fit>
        </el-table-column>
        <el-table-column
          prop="name"
          label="name"
          fit>
        </el-table-column>
        <el-table-column
          prop="phone"
          label="phone"
          fit>
        </el-table-column>
        <el-table-column
          prop="email"
          label="email"
          show-overflow-tooltip
          fit>
        </el-table-column>
        <el-table-column
          label="status"
          width="100">
          <template slot-scope="scope">
            <el-switch
              v-model="scope.row.enabled"
              active-color="#13ce66"
              inactive-color="#ff4949"
              @change="(value) => commitChange(value, scope.row)">
            </el-switch>
          </template>
        </el-table-column>
        <el-table-column
          label="operation"
          width="120">
          <template slot-scope="scope">
            <el-button
              @click.native.prevent="editBook(scope.row)"
              type="text"
              size="small">
              edit
            </el-button>
            <el-button
              @click.native.prevent="deleteBook(scope.row.id)"
              type="text"
              size="small">
              remove
            </el-button>
          </template>
        </el-table-column>
      </el-table>
      <div style="margin: 20px 0 20px 0;float: left">
        <el-button>cancel selection</el-button>
        <el-button>remove all</el-button>
      </div>
    </el-card>
  </div>
</template>

<script>
    export default {
        name: 'UserProfile',
      data () {
          return {
            users: []
          }
      },
      mounted () {
        this.listUsers()
      },
      computed: {
        tableHeight () {
          return window.innerHeight - 320
        }
      },
      methods: {
        listUsers () {
          var _this = this
          this.$axios.get('/admin/user').then(resp => {
            if (resp && resp.status === 200) {
              _this.users = resp.data
            }
          })
        },
        commitChange (value, user) {
          if (user.username !== 'admin') {
            this.$axios.put('/admin/user', {
              enabled: value,
              username: user.username
            }).then(resp => {
              if (resp && resp.status === 200) {
                if (value) {
                  this.$message('用户 [' + user.username + '] 已启用')
                } else {
                  this.$message('用户 [' + user.username + '] 已禁用')
                }
              }
            })
          } else {
            user.enabled = true
            this.$alert('不能禁用管理员账户')
          }
        }
      }
    }
</script>

<style scoped>

</style>
