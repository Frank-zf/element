## Ickey-Button 按钮
### 
:::demo ickey-button
```html
<el-row style="margin-bottom:20px">
  <el-button>默认按钮</el-button>
  <el-button type="primary">主要按钮</el-button>
  <el-button type="danger">危险按钮</el-button>
  <el-button type="warning">警告按钮</el-button>
</el-row>
<el-row style="margin-bottom:20px">
  <el-button plain>默认按钮</el-button>
  <el-button type="primary" plain>主要按钮</el-button>
    <el-button type="danger" plain>批量删除</el-button>
  <el-button type="warning" plain>警告按钮</el-button>
</el-row>
<script>
export default {
  data() {
    return {
      selectRow: null,
    }
  },
  created() {	
  },
  methods: {
  },
}
</script>
```
:::
### 配置说明

button按钮Json配置的数据结构字段说明

:::demo no-code
```html
<el-collapse>
  <el-collapse-item title="id" name="id">
    <div>类型为字符串，当前页面唯一即可</div>
  </el-collapse-item>
  <el-collapse-item title="element" name="element">
    <div>类型为字符串，此处应该为'button'，其他可选值：form，table，modal，button等</div>
  </el-collapse-item>
  <el-collapse-item title="getConfig" name="getConfig">
    <div>类型为函数，返回值一般为对象，对象可能包含的属性如下：（此处代码示例仅供参考数据结构，直接拷贝可能无法生效，更多案例见下方）</div>
      <el-collapse class="code-demo marginBottom">
        <el-collapse-item title="代码示例">
          <pre style="color:#666;">
getConfig() {
  return {
    name: '删除员工',
    type: 'danger',
    check() {
      return {
        max: null,
        min: 1,
      }
    },
    upload() {
      return {
        limit: 3,
        multiple: false,
        autoUpload: true,
        accept: '.js,.html,.vue,.png,.pdf',
      }
    },
    // 请求类型的action
    action() {
      return {
        tableId: 'staffTable',
        url: '/staff/delete',
        method: 'post',
        data: {}
      }
    },
    // 链接、路由类型的action
    action() {
      return {
        type: 'link',
        url: '/user/staff',
      }
    },
    // 弹窗类型的action
    action() {
      return {
        type: 'modal',
        element: 'add-page',
      }
    },
  }
},
          </pre>
        </el-collapse-item>
      </el-collapse>
  <el-table
    :data="getConfig"
    style="width: 100%"
    border
    row-key="name"
    :header-cell-style="() => 'background:#eee'"
    :tree-props="{children: 'children', hasChildren: 'hasChildren'}">
    <el-table-column
      prop="name"
      label="属性">
    </el-table-column>
    <el-table-column
      prop="desc"
      label="说明">
    </el-table-column>
    <el-table-column
      prop="type"
      label="类型/返回类型">
    </el-table-column>
    <el-table-column
      prop="value"
      label="可选值">
    </el-table-column>
    <el-table-column
      prop="default"
      label="默认值">
    </el-table-column>
  </el-table>
  </el-collapse-item>
</el-collapse>
<script>
  export default {
    data() {
      return {
        getConfig: [
          { 
            name: 'name',
            desc: '按钮名称',
            type: 'string',
            value: '',
            default: '',
          },
          { 
            name: 'type',
            desc: '按钮类型',
            type: 'string',
            value: 'primary,warning,danger',
            default: '',
          },
          { 
            name: 'icon',
            desc: '按钮icon',
            type: 'string',
            value: 'el-icon-search,el-icon-plus等，具体可查阅icon图标组件',
            default: '',
          },
          { 
            name: 'check',
            desc: '按钮校验配置，在触发action之前的校验，适合做table列表的批量删除等操作',
            type: 'object',
            value: '{}',
            default: '{}',
            children: [
              {
                name: 'max',
                desc: '最多选择多少项',
                type: 'number',
                value: '',
                default: '',
              },
              {
                name: 'min',
                desc: '最少选择多少项',
                type: 'number',
                value: '',
                default: '1',
              },
            ]
          },
          { 
            name: 'upload',
            desc: '上传按钮配置',
            type: 'object',
            value: '{}',
            default: '{}',
            children: [
              {
                name: 'limit',
                desc: '最多选择多少文件',
                type: 'number',
                value: '',
                default: '',
              },
              {
                name: 'multiple',
                desc: '是否支持多选',
                type: 'boolean',
                value: 'true,false',
                default: 'false',
              },
              {
                name: 'accept',
                desc: '可选的文件类型，文件名后缀需要加点.，以逗号隔开',
                type: 'string',
                value: '.js,.html,.vue,.png,.pdf',
                default: '',
              },
            ]
          },
          { 
            name: 'action',
            desc: '按钮具体操作',
            type: 'object',
            value: '{}',
            default: '{}',
            children: [
              {
                name: 'type',
                desc: '按钮操作类型，请求、弹窗、抽屉、链接/路由跳转',
                type: 'string',
                value: 'request,modal,drawer,link',
                default: 'request',
              },
              {
                name: 'url',
                desc: 'Api接口请求地址',
                type: 'string',
                value: '',
                default: '',
              },
              {
                name: 'method',
                desc: 'Api接口请求方法',
                type: 'string',
                value: 'post,get',
                default: '',
              },
              {
                name: 'data',
                desc: 'Api接口请求参数',
                type: 'any',
                value: '{}',
                default: '',
              },
              {
                name: 'tableId',
                desc: '关联的表格id，例如批量删除，点击删除之前校验对应表格的checkbox选项',
                type: 'string',
                value: '',
                default: '',
              },
              {
                name: 'element',
                desc: '关联的元素组件名，例如点击按钮弹出新增弹窗add-page，需要在components文件夹下新增addPage.vue，点击按钮之后就会弹出新增弹窗',
                type: 'string',
                value: '',
                default: '',
              }
            ]
          },
          { name: 'data', desc: 'api请求参数', type: 'any', value: '', default: 'null' },
        ],
        tableData: [
          { id: 10001, name: 'Test1', role: 'Develop', sex: 'Man', age: 28, address: 'test abc' },
          { id: 10002, name: 'Test2', role: 'Test', sex: 'Women', age: 22, address: 'Guangzhou' },
          { id: 10003, name: 'Test3', role: 'PM', sex: 'Man', age: 32, address: 'Shanghai' },
          { id: 10004, name: 'Test4', role: 'Designer', sex: 'Women', age: 24, address: 'Shanghai' }
        ]
      };
    },
    methods: {
      handleChange(val) {
        console.log(val);
      }
    }
  }
</script>
```
:::
### 案例说明

常用的button案例说明，对应getConfig里面的内容

:::demo no-code
```html
<el-collapse>
  <el-collapse-item title="添加员工 弹框" name="1">
      <el-collapse class="code-demo marginBottom">
        <div>这类按钮大多是放在table的左上角，且需要和table表格进行联动，所以配置要写到table下的getConfig-lowcodeProp-toolBar下面</div>
        <el-collapse-item title="代码示例">
          <pre style="color:#666;">
{
  id: 'addStaff',
  element: 'button',
  getConfig() {
    return {
      name: '添加员工',
      type: 'primary',
      action() {
        return {
          type: 'modal',
          element: 'add-page',
        }
      },
    }
  },
},
          </pre>
        </el-collapse-item>
      </el-collapse>
  <el-row style="margin-bottom:20px">
    <el-button @click="toolBarFunc" size="small" type="primary">新增</el-button>
  </el-row>
    <vxe-table
      border
      ref="xTable1"
      :data="tableData">
      <vxe-column field="name" title="姓名"></vxe-column>
      <vxe-column field="sex" title="性别"></vxe-column>
      <vxe-column field="age" title="年龄"></vxe-column>
    </vxe-table>
    <el-dialog title="新增员工" :visible.sync="dialogAddVisible">
      <el-form :model="addForm">
        <el-form-item label="姓名" :label-width="formLabelWidth">
          <el-input v-model="addForm.name" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="性别" :label-width="formLabelWidth">
          <el-select v-model="addForm.sex" placeholder="请选择员工性别">
            <el-option label="男" value="Man"></el-option>
            <el-option label="女" value="Women"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="年龄" :label-width="formLabelWidth">
          <el-input v-model="addForm.age" autocomplete="off"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogAddVisible = false">取 消</el-button>
        <el-button type="primary" @click="addStaff">确 定</el-button>
      </div>
    </el-dialog>
  </el-collapse-item>
</el-collapse>
<el-collapse>
  <el-collapse-item title="批量删除" name="1">
      <el-collapse class="code-demo marginBottom">
        <div>这类按钮大多是放在table的左上角，且需要和table表格进行联动，所以配置要写到table下的getConfig-lowcodeProp-toolBar下面</div>
        <el-collapse-item title="代码示例">
          <pre style="color:#666;">
{
  id: 'deleteStaff',
  element: 'button',
  getConfig() {
    return {
      name: '删除员工',
      type: 'danger',
      check() {
        return {
          max: 5,
          min: 1,
        }
      },
      action() {
        return {
          tableId: 'staffTable',
          url: '/staff/delete',
          method: 'post',
          params: 'ids:id',
        }
      },
    }
  },
},
          </pre>
        </el-collapse-item>
      </el-collapse>
  <el-row style="margin-bottom:20px">
    <el-button @click="deleteStaff" size="small" type="danger">删除</el-button>
  </el-row>
    <vxe-table
      border
      ref="xTableDelete"
      @checkbox-change="selectChangeEvent"
      @checkbox-all="selectAllEvent"
      :data="tableData">
      <vxe-column type="checkbox" width="60"></vxe-column>
      <vxe-column field="name" title="姓名"></vxe-column>
      <vxe-column field="sex" title="性别"></vxe-column>
      <vxe-column field="age" title="年龄"></vxe-column>
    </vxe-table>
  </el-collapse-item>
</el-collapse>
<el-collapse>
  <el-collapse-item title="链接/路由跳转" name="1">
      <el-collapse class="code-demo marginBottom">
        <div>支持http&https链接跳转，也支持路由跳转</div>
        <el-collapse-item title="代码示例">
          <pre style="color:#666;">
{
  id: 'openLink',
  element: 'button',
  getConfig() {
    return {
      name: '查看详情',
      type: 'primary',
      action() {
        return {
          type: 'link',
          url: '/staff/user',
        }
      },
    }
  },
},
          </pre>
        </el-collapse-item>
      </el-collapse>
  <el-row style="margin-bottom:20px">
    <el-button @click="viewDetail" size="small" type="primary">查看详情</el-button>
  </el-row>
  </el-collapse-item>
</el-collapse>
<el-collapse>
  <el-collapse-item title="打开抽屉/侧边栏" name="1">
      <el-collapse class="code-demo marginBottom">
        <div>抽屉里面内容需要单独写配置，支持自定义打开方向、宽度，组件文档待更新</div>
        <el-collapse-item title="代码示例">
          <pre style="color:#666;">
{
  id: 'drawer',
  element: 'button',
  getConfig() {
    return {
      name: '打开抽屉',
      type: 'primary',
      action() {
        return {
          type: 'drawer',
          element: 'add-page-drawer',
        }
      },
    }
  },
},
          </pre>
        </el-collapse-item>
      </el-collapse>
  <el-row style="margin-bottom:20px">
    <el-button @click="dialogDrawer = true" size="small" type="primary">打开抽屉</el-button>
  </el-row>
<el-drawer
  title="打开抽屉"
  :visible.sync="dialogDrawer"
  direction="rtl"
  size="40%"
  custom-class="demo-drawer"
  ref="drawer"
  >
  <div class="demo-drawer__content">
    <el-form :model="form">
      <el-form-item label="活动名称" :label-width="formLabelWidth">
        <el-input v-model="form.name" autocomplete="off"></el-input>
      </el-form-item>
      <el-form-item label="活动区域" :label-width="formLabelWidth">
        <el-select v-model="form.region" placeholder="请选择活动区域">
          <el-option label="区域一" value="shanghai"></el-option>
          <el-option label="区域二" value="beijing"></el-option>
        </el-select>
      </el-form-item>
    </el-form>
    <div class="demo-drawer__footer">
      <el-button @click="dialogDrawer = false">取 消</el-button>
      <el-button type="primary" @click="dialogDrawer = false">确定</el-button>
    </div>
  </div>
</el-drawer>
  </el-collapse-item>
</el-collapse>
<el-collapse>
  <el-collapse-item title="上传文件" name="1">
      <el-collapse class="code-demo marginBottom">
        <div>支持批量上传，上传预览功能</div>
        <el-collapse-item title="代码示例">
          <pre style="color:#666;">
  {
    id: 'upload',
    element: 'button',
    getConfig() {
      return {
        name: '上传',
        type: 'warning',
        upload() {
          return {
            limit: 3,
            multiple: true,
            autoUpload: true,
            accept: '.jpg,.png',
          }
        },
        action() {
          return {
            method: 'get',
            url: '/user/upload-user-file',
          }
        },
      }
    },
  },
          </pre>
        </el-collapse-item>
      </el-collapse>
  <!-- <el-row style="margin-bottom:20px">
    <el-button @click="viewDetail" size="small" type="warning">上传</el-button>
  </el-row> -->
<el-upload
  class="upload-demo"
  action="https://jsonplaceholder.typicode.com/posts/"
  :on-preview="handlePreview"
  :on-remove="handleRemove"
  :before-remove="beforeRemove"
  multiple
  :limit="3"
  :on-exceed="handleExceed"
  :file-list="fileList">
  <el-button size="small" type="primary">点击上传</el-button>
  <!-- <div slot="tip" class="el-upload__tip">只能上传jpg/png文件</div> -->
</el-upload>
  </el-collapse-item>
</el-collapse>

<script>
  export default {
    data() {
      return {
        input: '',
        tips: { content: '用户姓名' },
        tableData: [
          { id: 10001, name: 'Test1', role: 'Develop', sex: 'Man', age: 28, address: 'test abc',time: 1599320111520 },
          { id: 10002, name: 'Test2', role: 'Test', sex: 'Women', age: 22, address: 'Guangzhou',time: 1520820967410 },
          { id: 10003, name: 'Test3', role: 'PM', sex: 'Man', age: 32, address: 'Shanghai',time: 1609390785410 },
          { id: 10004, name: 'Test4', role: 'Designer', sex: 'Women', age: 23, address: 'test abc',time: 1611627586920 },
          { id: 10005, name: 'Test5', role: 'Develop', sex: 'Women', age: 30, address: 'Shanghai',time: 1629728569710 }
        ],
        fileList: [],
        dialogFormVisible: false,
        dialogAddVisible: false,
        dialogDrawer: false,
        form: {
          name: '',
          region: '',
          date1: '',
          date2: '',
          delivery: false,
          type: [],
          resource: '',
          desc: ''
        },
        addForm: {
          name: '',
          sex: '',
          age: '',
        },
        modalTitle: '',
        formLabelWidth: '120px',
        checkRecords: null
      };
    },
    methods: {
      handleClick(msg) {
        this.dialogFormVisible = true
      },
      toolBarFunc() {
        this.dialogAddVisible = true
      },
      addStaff() {
        const obj = this.addForm
        obj['id'] = Math.floor(Math.random() * 100000)
        obj['address'] = '上海'
        obj['time'] = +new Date()
        this.tableData.unshift(obj)
        this.addForm = {
          name: '',
          sex: '',
          age: '',
        }
        this.$message({
          message: '添加成功',
          type: 'success'
        });
        this.dialogAddVisible = false
      },
      selectChangeEvent ({ checked }) {
        const records = this.$refs.xTableDelete.getCheckboxRecords()
        this.checkRecords = records
        console.log(checked ? '勾选事件' : '取消事件', records)
      },
      selectAllEvent ({ checked }) {
        const records = this.$refs.xTableDelete.getCheckboxRecords()
        this.checkRecords = records
        console.log(checked ? '所有勾选事件' : '所有取消事件', records)
      },
      deleteStaff() {
        if (this.checkRecords.length < 1) {
          this.$message.error('请至少选择一项');
        } else if (this.checkRecords.length > 5) {
          this.$message.error('最多选择5项');
        } else {
          const ids = this.checkRecords.map(item => item.id)
          this.tableData = this.tableData.filter(item => !ids.includes(item.id))
          this.$message({
            message: '删除成功',
            type: 'success'
          });
        }
      },
      viewDetail() {
        window.location.href = '/#/zh-CN/component/ickey-form'
      },
      handleRemove(file, fileList) {
        console.log(file, fileList);
      },
      handlePreview(file) {
        console.log(file);
      },
      handleExceed(files, fileList) {
        this.$message.warning(`当前限制选择 3 个文件，本次选择了 ${files.length} 个文件，共选择了 ${files.length + fileList.length} 个文件`);
      },
      beforeRemove(file, fileList) {
        return this.$confirm(`确定移除 ${ file.name }？`);
      }
    }
  }
</script>
```