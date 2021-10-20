<template>
  <div class="admin">
    <div>
      <el-form ref="lists">
        <el-row>
          <el-col :xs="18" :sm="9" :md="7" :lg="7" :xl="5" class="el-col" style="margin: 20px">
            <span class="demo-input-label">Product name</span>
            <el-input
              placeholder="Please input"
              v-model="lists.product_name"
              :rules="lists.product_nameRueles"
            ></el-input>
            <i class="erors">{{this.erors.name}}</i>
            
          </el-col>
          <el-col :xs="18" :sm="9" :md="7" :lg="7" :xl="5" style="margin: 20px">
            <span class="demo-input-label">Product title</span>
            <el-input
              placeholder="Please input"
              v-model="lists.product_title"
            ></el-input>
            <i class="erors">{{this.erors.title}}</i>
          </el-col>
          <el-col :xs="18" :sm="9" :md="7" :lg="7" :xl="5" style="margin: 20px">
            <span class="demo-input-label">Product type</span>
            <el-input
              placeholder="Please input"
              v-model="lists.product_type"
            ></el-input>
            <i class="erors">{{this.erors.type}}</i>
          </el-col>
          <el-col :xs="18" :sm="9" :md="7" :lg="7" :xl="5" style="margin: 20px">
            <span class="demo-input-label">Product price</span>
            <el-input
              placeholder="Please input"
              v-model="lists.product_price"
            ></el-input>
            <i class="erors">{{this.erors.price}}</i>
          </el-col>
          <el-col :xs="18" :sm="9" :md="7" :lg="7" :xl="5" style="margin: 20px">
            <span class="demo-input-label">Product author</span>
            <el-input
              placeholder="Please input"
              v-model="lists.author"
            ></el-input>
            <i class="erors">{{this.erors.author}}</i>
          </el-col>
          <el-col
            :xs="24"
            :sm="24"
            :md="24"
            :lg="24"
            :xl="24"
            class="btn-group"
          >
            <el-button @click="cancel()">Cansel</el-button>
            <el-button @click="onSubmit()">Create Product</el-button>
          </el-col>
        </el-row>
      </el-form>
    </div>
    <div>
      <el-table :data="tableData" style="width: 100%">
        <el-table-column label="product name" prop="product_name" width="180">
        </el-table-column>
        <el-table-column label="product title" prop="product_title" width="180">
        </el-table-column>
        <el-table-column label="product type" prop="product_type" width="180">
        </el-table-column>
        <el-table-column label="product price" prop="product_price" width="180">
        </el-table-column>
        <el-table-column label="author" prop="author" width="180">
        </el-table-column>
        <el-table-column label="Buttons" width="180">
          <template slot-scope="scope">
            <el-button @click="editItem(scope.$index, scope.row)"
              >Edit</el-button
            >
            <el-button @click="deleted()">Delete</el-button>
          </template>
        </el-table-column>
      </el-table>
    </div>
    <el-dialog
      title="Edit product"
      :visible.sync="dialogVisible"
      width="30%"
      :before-close="handleClose"
    >
      <el-form ref="editList">
        <el-row>
          <el-col :xs="5" :sm="5" :md="7" :lg="7" :xl="10" style="margin: 10px">
            <span class="demo-input-label">Product name</span>
            <el-input
              placeholder="Please input"
              v-model="editList.product_name"
            ></el-input>
          </el-col>
          <el-col :xs="5" :sm="5" :md="7" :lg="7" :xl="10" style="margin: 10px">
            <span class="demo-input-label">Product title</span>
            <el-input
              placeholder="Please input"
              v-model="editList.product_title"
            ></el-input>
          </el-col>
          <el-col :xs="5" :sm="5" :md="7" :lg="7" :xl="10" style="margin: 10px">
            <span class="demo-input-label">Product type</span>
            <el-input
              placeholder="Please input"
              v-model="editList.product_type"
            ></el-input>
          </el-col>
          <el-col :xs="5" :sm="5" :md="7" :lg="7" :xl="10" style="margin: 10px">
            <span class="demo-input-label">Product price</span>
            <el-input
              placeholder="Please input"
              v-model="editList.product_price"
            ></el-input>
          </el-col>
          <el-col :xs="5" :sm="5" :md="7" :lg="7" :xl="10" style="margin: 10px">
            <span class="demo-input-label">Product author</span>
            <el-input
              placeholder="Please input"
              v-model="editList.author"
            ></el-input>
          </el-col>
        </el-row>
      </el-form>
      <span slot="footer" class="dialog-footer">
        <el-button @click="dialogVisible = false">Cancel</el-button>
        <el-button type="primary" @click="save()">Save</el-button>
      </span>
    </el-dialog>
    <el-dialog
  :visible.sync="centerDialogVisible"
  width="30%"
  center>
  <span>Rostan ham o'chirmoqchimisan</span>
  <span slot="footer" class="dialog-footer">
    <el-button @click="centerDialogVisible = false">Cancel</el-button>
    <el-button type="primary" @click="deleteItem(item)">Delete</el-button>
  </span>
</el-dialog>
  </div>
</template>

<script>
import Vue from "vue";
import axios from "axios";
import VueAxios from "vue-axios";
Vue.use(VueAxios, axios);
export default {
  data() {
    return {
      lists: {
        product_name: null,
        product_title: null,
        author: null,
        id: null,
        create_time: null,
        product_type: null,
        product_price: null,
      },
      tableData: [],
      item: null,
      dialogVisible: false,
      editList: {
        product_name: null,
        product_title: null,
        author: null,
        id: null,
        create_time: null,
        product_type: null,
        product_price: null,
      },
      erors: {
        name:null,
        title: null,
        type: null,
        price: null,
        author: null,
      },
      centerDialogVisible: false
    };
  },
  mounted() {
    this.getList();
  },

  methods: {
    getList() {
      Vue.axios
        .get(`https://616e5323a83a850017caa91c.mockapi.io/api/shop//users`)
        .then((res) => {
          this.tableData = res.data;
          for(let i in this.tableData){
            this.item = this.tableData[i].id
          }
        });
    },
    onSubmit() {
      if((this.lists.product_name === null)){
        this.erors.name="Iltimos mahsulot nomini kiriting"
      }else if(this.lists.product_title === null){
        this.erors.title="Iltimos mahsulot haqida ma'lumot kiriting"
      }
      else if(this.lists.product_type === null){
        this.erors.type="mahsulot qaysi type ga bog'liq?"
      }
      else if((this.lists.product_price === null)){
        this.erors.price="mahsulotga narx belgilang"
        console.log(typeof(this.lists.product_price));
        
      }
      else if(this.lists.author === null){
        this.erors.author="mahsulot kim tomonidan kiritildi?"
      }
      else{
        Vue.axios
        .post(
          `https://616e5323a83a850017caa91c.mockapi.io/api/shop//users`,
          this.lists
        )
        .then(() => {
          this.getList();
          this.lists.product_name = null;
          this.lists.product_title = null;
          this.lists.product_price = null;
          this.lists.id = null;
          this.lists.author = null;
          this.lists.product_type = null;
          this.erors.name=null;
          this.erors.title=null;
          this.erors.price=null;
          this.erors.type=null;
          this.erors.author=null;
        })
        .catch((error) => {
          console.log(error);
        })
        .finally(() => {});
      this.dialogVisible = false;
      }
      
      
    },
    cancel() {
      this.lists.product_name = null;
      this.lists.product_title = null;
      this.lists.product_price = null;
      this.lists.author = null;
      this.lists.id = null;
      this.lists.product_type = null;
      this.lists.create_time = null;
    },
    deleted() {
      this.centerDialogVisible = true
    },
    deleteItem(item) {
      Vue.axios
        .delete(
          "https://616e5323a83a850017caa91c.mockapi.io/api/shop//users/" +  item
        )
        .then(() => {
          this.getList();
        });
        this.centerDialogVisible = false
    },
    handleClose(done) {
      this.$confirm("Are you sure to close this dialog?")
        .then(() => {
          done();
        })
        .catch(() => {});
    },
    editItem(index, row) {
      this.dialogVisible = true;
      console.log("row.id", row.id);
      this.editList.id = row.id;
      Vue.axios
        .get(
          "https://616e5323a83a850017caa91c.mockapi.io/api/shop//users/" +
            row.id
        )
        .then((res) => {
          this.editList.product_name = res.data.product_name;
          this.editList.product_title = res.data.product_title;
          this.editList.product_price = res.data.product_price;
          this.editList.product_type = res.data.product_type;
          this.editList.author = res.data.author;
        });
      console.log(index);
    },
    save(item) {
      console.log(item);
      Vue.axios
        .put(
          "https://616e5323a83a850017caa91c.mockapi.io/api/shop//users/" +
            this.editList.id,
          this.editList
        )
        .then((res) => {
          console.log(res.data);
          this.getList();
        });
        this.dialogVisible = false;
    },
  },
};
</script>

<style>
.admin {
  padding: 30px;
}
.demo-input-label {
  text-transform: lowercase;
  color: #666;
  margin: 10px 0px;
  font-size: 13px;
  text-align: start;
  display: block;
  position: relative;
}
.demo-input-label:after {
  content: "*";
  color: red;
  font-size: 16px;
  position: absolute;
  top: 0;
  right: 0;
}
.el-date-editor {
  width: 100% !important;
}
.btn-group {
  display: flex;
  justify-content: end;
}
/* Dialog */
.el-dialog {
  width: 50% !important;
}
.el-col{
  position: relative;
}
.erors{
  display: block;
  position: absolute;
  bottom: -15px;
  left: 0;
  color: red;
  font-size: 11px;
}
</style>