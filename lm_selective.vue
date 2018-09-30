<template >

    <!-- :model="filters" v-model="filters.title" v-on:click="getUsers" @click="handleAdd"-->
  <section>
        <!-- 左侧子导航 -->
      <div id="subNav"  class="lanmu-subNav"  >
        <comp-tree ref="child" :callback="getTreeInfo"></comp-tree>        
      
      </div>
          <!-- 右侧主内容区 -->
      <div class="lanmu-content">
         <div class="lanmu-top-content">  
            <!-- 第一行 -->
            <div class="lanmu-top-content1">         
              <div class="lanmu-top11"> 查询条件</div>   
            <div class="lanmu-clearfloat"></div> 
            </div>

          <!-- 第二行  具体的查询条件-->
            <div class="lanmu-top2">
                <div class="lanmu-top2-name"> 
                <span class="lanmu-com">栏目名称:</span> <el-input></el-input>
                </div>
                
                <div class="lanmu-top2-state"> 
                  <span class="lanmu-com">栏目状态</span>
                  <el-select placeholder="请选择">
                      <el-option>全部</el-option>   
                      <el-option>禁用</el-option>   
                      <el-option>启用</el-option>   
                  </el-select>             
                </div>

                <div class="lanmu-top2-checked"> 
                <span class="lanmu-com">是否需要审核</span>
                  <el-select placeholder="请选择">
                      <el-option>全部</el-option>   
                      <el-option>是</el-option>   
                      <el-option>否</el-option>   
                  </el-select>
                </div>
              <div class="lanmu-clearfloat"></div>
            </div>
          <!-- 底部第三行 三个按钮 -->
            <div class="lanmu-top3">
                  <el-form :inline="true" >                 
                    <el-form-item>
                      <el-button type="primary" >查询</el-button>
                    </el-form-item>
                    <el-form-item>
                      <el-button type="primary">重置</el-button>
                    </el-form-item>
                  
                  </el-form> 
          </div>        
      </div>
       <!-- 增加同级或子级栏目的按钮 -->
      <div class="lanmu-mid-content">       
        <div class="lanmu-midBtn3"><el-button type="warning"> 删除</el-button></div>
        <div class="lanmu-midBtn2"><el-button type="warning"> 新增子级栏目</el-button></div>
        <div class="lanmu-midBtn1">
          <el-button type="warning" @click="addDialogVisible = true"> 新增同级栏目</el-button></div>
        <div class="lanmu-clearfloat"></div>
      </div>

      <!-- 对话框——新增栏目 -->
         <el-dialog class="add-dialog"   title="新增同级栏目"   :visible.sync="addDialogVisible"     :before-close="handleClose">
           <div class="add-content">
                  <el-form    ref="addForm">
                    <!-- 1、父级栏目 -->
                  <el-form-item label="父级栏目" prop="fuji" style="add-titleFont">
                    <el-input  auto-complete="off"></el-input>
                  </el-form-item>
                    <!-- 2、栏目名称和序号  -->
                      <el-form-item label="栏目名称" prop="lmname" style="add-titleFont">
                    <el-input  auto-complete="off"></el-input>
                    </el-form-item>
                      <el-form-item label="序号" prop="xuhao" style="add-titleFont">
                    <el-input  auto-complete="off"></el-input>
                    </el-form-item>
                    <!-- 3、链接地址 -->
                    <el-form-item label="链接地址" prop="dizhi" style="add-titleFont">
                    <el-input  auto-complete="off"></el-input>
                    </el-form-item>
                    <!-- 4、预览图 -->
                    <el-form-item label="预览图" prop="yulan" style="add-titleFont">
                          <el-upload  class="upload-demo">
                            <el-button size="small" type="primary">点击上传</el-button>
                          </el-upload>
                    </el-form-item>					 
                    <!-- 5、是否需要审批 -->
                    <el-form-item label="是否需要审批" prop="shenpi" style="add-titleFont">
                        <el-radio v-model="radio" label="1">备选项</el-radio>
                          <el-radio v-model="radio" label="2">备选项</el-radio>
                    </el-form-item>			
                    <!-- 6、说明 -->
                    <el-form-item label="说明" prop="shuoming" style="add-titleFont">
                        富文本缺少
                    </el-form-item>
                    <!-- 7、栏目允许互动 -->
                    <el-form-item label="栏目允许互动" prop="lmhudong" style="add-titleFont">
                          <el-checkbox-group v-model="checkList">
                            <el-checkbox label="评论"></el-checkbox>
                            <el-checkbox label="收藏"></el-checkbox>
                            <el-checkbox label="点赞"></el-checkbox>
                            <el-checkbox label="分享" ></el-checkbox>
                            <el-checkbox label="缓存" ></el-checkbox>
                          </el-checkbox-group>
                    </el-form-item>
                    <!-- 8、图文允许互动 -->
                    <el-form-item label="图文允许互动" prop="tuwenhudong" style="add-titleFont">
                          <el-checkbox-group v-model="checkList">
                            <el-checkbox label="评论"></el-checkbox>
                            <el-checkbox label="收藏"></el-checkbox>
                            <el-checkbox label="点赞"></el-checkbox>
                            <el-checkbox label="分享" ></el-checkbox>
                            <el-checkbox label="缓存" ></el-checkbox>
                          </el-checkbox-group>
                    </el-form-item>
                    <!-- 9、栏目类型 -->
                    <el-form-item label="栏目类型" prop="lmleixnig" style="add-titleFont">
                        空
                    </el-form-item>
                    <!-- 10、所属地区 -->
                      <el-form-item label="所属地区" prop="diqu" style="add-titleFont">
                          <el-radio v-model="radio" label="1">基层</el-radio>
                          <el-radio v-model="radio" label="2">市内</el-radio>
                          <el-radio v-model="radio" label="2">市外</el-radio>
                          <el-radio v-model="radio" label="2">国外</el-radio>
                    </el-form-item>
                    <!-- 提交和取消按钮 -->
                    <el-form-item>
                        <el-button type="success"  @click="addDialogVisible = false">立即创建</el-button>
                        <el-button @click="addDialogVisible">取消</el-button>
                      </el-form-item>
                  </el-form>
			      </div>                
        </el-dialog>



      <!-- 表格数据部分 table-->
      <el-table :data="tableData" highlight-current-row   >
        <el-table-column type="selection" width="55">	</el-table-column>
        <!-- <el-table-column type="index" width="55" label="序号"></el-table-column> -->     
      <el-table-column  label="预览图" prop="" >    </el-table-column>
      <el-table-column  label="栏目名称" prop="name">    </el-table-column>
      <el-table-column  label="父级栏目" prop="parentName" >  </el-table-column>
      <el-table-column   label="是否审核" prop="isReview" >     </el-table-column>
      <el-table-column   label="评论量" prop="countColumnComment" >     </el-table-column>
      <el-table-column   label="关注量" prop="countColumnAttention" >     </el-table-column>
      <el-table-column   label="收藏量" prop="countColumnCollection" >     </el-table-column>
      <el-table-column   label="点赞量" prop="countColumnLiked" >     </el-table-column>
      <el-table-column   label="分享量" prop="countColumnShare" >     </el-table-column>

      <el-table-column   label="评论量" prop="countArticleComment" >     </el-table-column>
       <el-table-column   label="收藏量" prop="countArticleCollection" >     </el-table-column>
      <el-table-column   label="点赞量" prop="countArticleLiked" >     </el-table-column>
      <el-table-column   label="分享量" prop="countArticleShare" >     </el-table-column>
      <el-table-column   label="缓存量" prop="countArticleCache" >     </el-table-column>
              <!-- 最后一列有编辑和删除按钮 -->
      <el-table-column   label="状态"  >     </el-table-column>
      <el-table-column label="操作" >
          <template slot-scope="scope">
            <el-button size="small" @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
            <el-button type="danger" size="small" @click="handleDel(scope.$index, scope.row)">删除</el-button>
          </template>
        </el-table-column>
      </el-table> 
  </div>
    </section>




</template>
<script>
import CompTree from   './CompTree.vue';

export default {
  components:{
    CompTree,    
    },
  data() {
    return {
      filters: { title: "" },
      search: "",      
      tableData: [],          //存储表格数据
      addDialogVisible:false, //新增栏目的对话框是否显示
       //选中节点的信息
       selectNode:{
         nodeID:'',
         nodeName:''
       },
      //编辑对话框界面数据
      editForm: {
        index: 0,
        title: "",
        content: -1,
        author: "",
        submitTime: "",
        approver: ""
      }
      // editFormRules: {title: [{ required: true, messauthor: '请输入标题', trigger: 'blur' }]},
    };
  },
  created() {
    this.getGoodsList();
  },
  computed: {
    tables() {
      const search = this.search;
      if (search) {
        return this.tableData.filter(data => {
          return Object.keys(data).some(key => {
            return (
              String(data[key])
                .toLowerCase()
                .indexOf(search) > -1
            );
          });
        });
      }
      return this.tableData;
    }
  },

  methods: {    
    //内容显示转换
    formatcontent: function(row, column) {
      return row.content == 1 ? "男" : row.content == 0 ? "女" : "未知";
    },
    //利用父组件调用子组件的方法，来获取子组件tree当前被点击的节点信息。
     getTreeInfo(q){
      //  console.log('i am f',qq.id); 
       this.selectNode.nodeID=q.id;
       this.selectNode.nodeName=q.name;
       console.log('i am f',this.selectNode); 
     },
      

    //打开新增界面--未用
    handleAdd: function() {
      this.$router.push({ path: '/lanmuManage/lm_selective_add' });
     
    },

    //点编辑按钮，显示编辑界面
    handleEdit: function(index, row) {
      // this.editFormVisible = true;
      this.editForm = Object.assign({}, row);
      this.$router.push({
        path: "/lanmuManage/lm_selective_edit",
        query: this.editForm
      });
    },

    // 点删除按钮后显示的界面
    handleDel: function(index, row) {
      this.$confirm("确认删除该记录吗?", "提示", { type: "warning" })
        .then(() => {
          this.listLoading = true;
          //NProgress.start();
          let para = { id: row.id };
          removeUser(para).then(res => {
            this.listLoading = false;
            //NProgress.done();
            this.$messauthor({ messauthor: "删除成功", type: "success" });
            this.getUsers();
          });
        })
        .catch(() => {});
    },
    //自己编写的本地json文件数据
    getGoodsList() {
       let url='http://192.168.1.4:8080/column/getList/v1?pageNum=1&pageSize=5&isReview=1';
      this.$http.get(url).then(
        response => {
          // 响应成功回调
          // console.log('res取数成功', response.data.data.list)
          this.tableData = response.data.data.list;
          console.log('table取数成功', this.tableData)
        },
        response => {
          // 响应错误回调
          alert("table服务器请求失败");
        }
      );
    },

    svae() {},
    subbmit() {}
  }
};
</script>
<style scope>
/* 中间的三个栏目按钮 */
.lanmu-mid-content{
  background-color: #f2f2f2;
  margin-bottom: 20px;
}
.lanmu-midBtn1, .lanmu-midBtn2, .lanmu-midBtn3{
  float: right;
  width: 200px;
  margin-left: 0;
}

.lanmu-mid-content .el-button--primary:hover{
  background-color: #ffffff;
}
/* 主内容区 */
.lanmu-top11 {
  float: left;
  font-weight: 800;
  margin-left: 15px;
  margin-top: 15px;
  font-size: 20px;
}
.lanmu-top-content1 .el-button {
  position: relative;
  float: right;
  margin-right: 25px;
  background-color: #378283;
  color: white;
}
.lanmu-clearfloat {
  clear: both;
}
/* top第二行 */
.lanmu-top2 {
  margin-top: 20px;
  margin-bottom: 20px;
  margin-left: 40px;
  margin: 20px 0px 20px 20px;
}
.lanmu-top2-name,
.lanmu-top2-state,
.lanmu-top2-checked {
  float: left;
  margin: 0px 20px;
}
.lanmu-com {
  background-color: #cbebda;
  display: inline-block;
  width: 120px;
  height: 40px;
  line-height: 40px;
  vertical-align: top;
}

.lanmu-top2 .el-input,
.lanmu-top2 .el-select {
  width: 200px; 
  float: none;
}
 /* 第三行2个按钮 top3  */
.lanmu-top3 .el-button{
  width: 150px;
}
.lanmu-top3 .el-form{
  width:500px;
  margin-left: 20%;
}

/* 子导航区的设置 */
.rate1,
.el-submenu__title,
.el-menu-item {
  font-size: 20px;
  font-weight: 200;
}
.rate1 {
  display: block;
  width: 100%;
  margin-right: 20px;
}
.lanmu-subNav {
  width: 15%;
  background: #e7ecee;
  float: left;
  height: 1000px;
}
.el-menu {
  background: #e7ecee;
}
.lanmu-content {
  width: 85%;
  background-color: #fff;
  float: right;
}

.el-table .cell,
.el-table th div {
  text-align: center;
  text-overflow: ellipsis;
  white-space: nowrap;
  overflow: hidden;
}
.el-main {
  margin: 0;
  padding: 0;
}
.el-col-15 {
  padding-top: 20px;
}

/* 新增-对话框 样式 */
.add-dialog .el-form {
 background-color: white;
   /* width: 80%;  */
}
.add-dialog .el-dialog__body{
  width: 1100px;
  padding: 0;
 
}
.add-dialog .el-dialog__header{
  width: 1100px;
   background-color: yellow;

}
 .add-dialog .el-dialog__header{
    padding: 20px 65px 10px;
}

.el-form-item__label{
  width:150px;
}
.el-input{
  width:30%;
}
</style>

