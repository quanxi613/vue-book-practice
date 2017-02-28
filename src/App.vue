<template>
  <section>
    <!-- <img src="./assets/logo.png"> -->
    <el-row>
      <el-col :span="24">
        <h3 class="title">书籍管理demo</h3>
      </el-col>
    </el-row>
    <el-table :data="books" style="width: 100%;margin-bottom: 20px;" :row-class-name="tableRowClassName">
      <el-table-column prop="num" label="序号" width="180"></el-table-column>
      <el-table-column prop="name" label="书名" width="180"></el-table-column>
      <el-table-column prop="author" label="作者"></el-table-column>
      <el-table-column prop="price" label="价格"></el-table-column>
      <el-table-column label="操作">
        <template scope="scope">
          <el-button  type="text" size="small" @click="editBook(scope.$index, scope.row)">编辑</el-button>
          <el-button type="text" size="small" @click="delBook(scope.$index, scope.row)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
    <el-button @click="addBook">点击新增</el-button>
    <el-dialog title="新增书籍" v-model="dialogFormVisible">
      <el-form :model="book">
        <el-form-item label="书籍名称" :label-width="formLabelWidth">
          <el-input v-model="book.name" auto-complete="off"></el-input>
        </el-form-item>
        <el-form-item label="作者" :label-width="formLabelWidth">
          <el-input v-model="book.author" auto-complete="off"></el-input>
        </el-form-item>
        <el-form-item label="价格" :label-width="formLabelWidth">
          <el-input v-model="book.price" auto-complete="off"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="addSubmit">确 定</el-button>
      </div>
    </el-dialog>
    <el-dialog title="编辑书籍" v-model="editFormVisible">
      <el-form :model="bookEdit">
        <input type="hidden" v-model="bookEdit.num">
        <el-form-item label="书籍名称" :label-width="formLabelWidth">
          <el-input v-model="bookEdit.name" auto-complete="off"></el-input>
        </el-form-item>
        <el-form-item label="作者" :label-width="formLabelWidth">
          <el-input v-model="bookEdit.author" auto-complete="off"></el-input>
        </el-form-item>
        <el-form-item label="价格" :label-width="formLabelWidth">
          <el-input v-model="bookEdit.price" auto-complete="off"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="editFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="editSubmit">确 定</el-button>
      </div>
    </el-dialog>
  </section>
</template>

<script>
export default {
  data () {
    return {
      msg: 'Use Today!',
      books: [{
        num: '1',
        name: '红楼梦',
        author: '曹雪芹',
        price: '20'
      }, {
        num: '2',
        name: '西游记',
        author: '吴承恩',
        price: '20'
      }, {
        num: '3',
        name: '三国演义',
        author: '罗贯中',
        price: '20'
      }, {
        num: '4',
        name: '水浒传',
        author: '施耐庵',
        price: '20'
      }],
      formLabelWidth: '80px',
      dialogFormVisible: false,
      book: {
        num: 0,
        author: '',
        name: '',
        price: ''
      },
      editFormVisible: false,
      bookEdit: {
        num: 0,
        author: '',
        name: '',
        price: ''
      }
    }   
  },

  methods: {
    startHacking () {
      this.$notify({
        title: 'It Works',
        message: 'We have laid the groundwork for you. Now it\'s your time to build something epic!',
        duration: 6000
      })
    },
    tableRowClassName(row, index) {
      if (index === 1) {
        return 'info-row';
      } else if (index === 3) {
        return 'positive-row';
      }
      return '';
    },
    addBook () {
      this.dialogFormVisible = true;
      this.book = {
        num: 0,
        name: '',
        author: '',
        price: ''
      }
    },
    addSubmit () {
      this.book.num = this.books.length + 1;
      this.books.push(this.book);
      this.book = {
        num: 0,
        author: '',
        name: '',
        price: ''
      };
      this.dialogFormVisible = false;
    },
    delBook (index, row) {
      this.books.splice(index, 1);
    },
    editBook (index, row) {
      this.editFormVisible = true;
      this.bookEdit = {
        num: index,
        author: row.author,
        name: row.name,
        price: row.price
      }
    },
    editSubmit () {
      var num = this.bookEdit.num;
      var newBook = this.bookEdit;
      newBook.num = num+1;
      this.books.splice(num, 1, newBook);
      this.editFormVisible = false;
    }
  }
}
</script>

<style>
body {
  font-family: Helvetica, sans-serif;
}
.title {
  text-align: center;
}
.el-table .info-row {
  background: #c9e5f5;
}
.el-table .positive-row {
  background: #e2f0e4;
}
</style>
