<template>
<div>
	<el-form :model="formData" ref="formData" :rules="rules">
		<el-form-item prop="age">
	        <el-input v-model="formData.age" placeholder="age"></el-input>
	     </el-form-item>
	     <tables :formData="formData" :rules="rules"></tables>
	    <!-- <el-table :data="formData.tableData" border stripe style="width: 100%;">
	      <el-table-column prop="name" label="姓名">
	        <template slot-scope="scope">
	          <el-form-item v-if="scope.row.edit" :prop="'tableData.' + scope.$index + '.name'" :rules='rules.name'>
	            <el-input v-model="scope.row.name" placeholder="姓名"></el-input>
	          </el-form-item>
	          <span v-else>{{scope.row.name}}</span>
	        </template>
	      </el-table-column>
	      <el-table-column prop="sex" label="性别">
	        <template slot-scope="scope">
	          <el-form-item v-if="scope.row.edit" :prop="'tableData.' + scope.$index + '.sex'" :rules='rules.sex'>
	            <el-select v-model="scope.row.sex" placeholder="请选择">
	              <el-option label="男" value="1">男</el-option>
	              <el-option label="女" value="2">女</el-option>
	            </el-select>
	          </el-form-item>
	          <span v-else>
	            <p v-if="scope.row.sex==1">男</p>
	            <p v-if="scope.row.sex==2">女</p>
	          </span>
	        </template>
	      </el-table-column>
	      <el-table-column label="操作">
	        <template slot-scope="scope">
	          <el-button v-if="scope.row.edit" type="text" size="medium" @click="confirmAdd(scope.row,'formData')">
	            <i class="el-icon-check" aria-hidden="true"></i>
	          </el-button>
	          <div v-else>
	            <el-button type="text" size="medium" @click="editData(scope.row)">
	              <i class="el-icon-edit" aria-hidden="true"></i>
	            </el-button>
	            <el-button type="text" size="medium" @click="deleteData(scope.row,scope.$index)">
	              <i class="el-icon-delete" aria-hidden="true"></i>
	            </el-button>
	          </div>
	        </template>
	      </el-table-column>
	    </el-table> -->
	</el-form>
  <el-button type="text" @click="addData">添加数据</el-button>
  <!-- <el-divider></el-divider> -->
  <el-button @click="submitData('formData')">提交 </el-button>

</div>
</template>
<script>
	import tables from './tables'
  export default {
    name: "demo",
    components:{
    	tables
    },
    data() {
      return {
        formData: {
          age:null,
          tableData: [],
        },
        rules: {
	        age:{
	        	required: true,
	            message: '请输入age',
	        },
	          name: {
	            required: true,
	            message: '请输入名字',
	          },
	          sex: {
	            required: true,
	            message: '请选择性别',
	          },
        },
      }
    },
    computed:{
    	// rules:{
    	// 	age:{
	    //     	required: true,
	    //         message: '请输入age',
	    //     },
	    //      name: {
	    //         required: true,
	    //         message: '请输入名字',
	    //     },
	    //     sex: {
	    //         required: true,
	    //         message: '请选择性别',
	    //       },
	    // }
    },
    methods: {
      //添加
      addData() {
        this.formData.tableData.push({
          edit: true,
        });
      },
      //确认添加
      confirmAdd(row, formName) {
        this.$refs[formName].validate((valid) => {
          if (valid) {
            row.edit = false;
          }
        })
      },
      //修改
      editData(row) {
        row.edit = true;
      },
      //删除
      deleteData(row, index) {
        this.formData.tableData.splice(index, 1);
      },
      submitData(formName) {

        this.$refs[formName].validate((valid) => {
          if (valid) {
            let data = this.formData.tableData
            alert(JSON.stringify(data))
          }
        })
      }
    }
  }

</script>