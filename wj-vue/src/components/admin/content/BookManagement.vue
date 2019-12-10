<template>
  <div>
    <el-row style="margin: 18px 0px 0px 18px ">
      <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item :to="{ path: '/admin/dashboard' }">Management System</el-breadcrumb-item>
        <el-breadcrumb-item>Content Management</el-breadcrumb-item>
        <el-breadcrumb-item>Book Management</el-breadcrumb-item>
      </el-breadcrumb>
    </el-row>
    <edit-form @onSubmit="loadBooks()" ref="edit"></edit-form>
    <el-card style="margin: 18px 2%;width: 95%">
      <el-table
        :data="books"
        stripe
        style="width: 100%"
        :max-height="tableHeight">
        <el-table-column
          type="selection"
          width="55">
        </el-table-column>
        <el-table-column type="expand">
          <template slot-scope="props">
            <el-form label-position="left" inline>
              <el-form-item>
                <span>{{ props.row.abs }}</span>
              </el-form-item>
            </el-form>
          </template>
        </el-table-column>
        <el-table-column
          prop="title"
          label="Title"
          fit>
        </el-table-column>
        <el-table-column
          prop="category.name"
          label="Category"
          width="100">
        </el-table-column>
        <el-table-column
          prop="author"
          label="Author"
          fit>
        </el-table-column>
        <el-table-column
          prop="date"
          label="Press Date"
          width="120">
        </el-table-column>
        <el-table-column
          prop="press"
          label="Press"
          fit>
        </el-table-column>
        <!--<el-table-column-->
          <!--prop="abs"-->
          <!--label="摘要"-->
          <!--show-overflow-tooltip-->
          <!--fit>-->
        <!--</el-table-column>-->
        <el-table-column
          fixed="right"
          label="Operation"
          width="120">
          <template slot-scope="scope">
            <el-button
              @click.native.prevent="editBook(scope.row)"
              type="text"
              size="small">
              Edit
            </el-button>
            <el-button
              @click.native.prevent="deleteBook(scope.row.id)"
              type="text"
              size="small">
              Remove
            </el-button>
          </template>
        </el-table-column>
      </el-table>
      <div style="margin: 20px 0 20px 0;float: left">
        <el-button>Cancel Selection</el-button>
        <el-button>Remove All</el-button>
      </div>
    </el-card>
  </div>
</template>

<script>
  import EditForm from './EditForm'
  export default {
    name: 'BookManagement',
    components: {EditForm},
    data () {
      return {
        books: []
      }
    },
    mounted () {
      this.loadBooks()
    },
    computed: {
      tableHeight () {
        return window.innerHeight - 320
      }
    },
    methods: {
      deleteBook (id) {
        this.$confirm('Continue?', 'Tip', {
          confirmButtonText: 'Yes',
          cancelButtonText: 'No',
          type: 'warning'
        }).then(() => {
            this.$axios
              .post('/delete', {id: id}).then(resp => {
              if (resp && resp.status === 200) {
                this.loadBooks()
              }
            })
          }
        ).catch(() => {
          this.$message({
            type: 'info',
            message: 'Cancel'
          })
        })
        // alert(id)
      },
      editBook (item) {
        this.$refs.edit.dialogFormVisible = true
        this.$refs.edit.form = {
          id: item.id,
          cover: item.cover,
          title: item.title,
          author: item.author,
          date: item.date,
          press: item.press,
          abs: item.abs,
          category: {
            id: item.category.id.toString(),
            name: item.category.name
          }
        }
        // this.$refs.edit.category = {
        //   id: item.category.id.toString()
        // }
      },
      loadBooks () {
        var _this = this
        this.$axios.get('/books').then(resp => {
          if (resp && resp.status === 200) {
            _this.books = resp.data
          }
        })
      }
    }
  }
</script>

<style scoped>
</style>
