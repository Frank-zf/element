## Ickey-Table 复杂表格
### 
:::demo ickey-table，直接拷贝mockdata部分即可生成整个表格
```html
<el-row style="margin-bottom:20px">
  <el-button @click="toolBarFunc('新增')" size="small">新增</el-button>
  <el-button @click="toolBarFunc('删除')" size="small" type="primary">删除</el-button>
  <el-button @click="toolBarFunc('禁用')" size="small" type="disabled">禁用</el-button>
</el-row>
  <vxe-table
    ref="xTable1"
    border
    resizable
    show-overflow
    keep-source
    max-height="400"
    row-id="id"
    size="medium"
    :loading="loading2"
    :data="tableData2"
  >
    <vxe-column
      type="checkbox"
      width="60"
    />
    <vxe-column
      type="seq"
      title="id"
      width="60"
      sortable
    />
    <vxe-column
      field="name"
      title="客户名称"
      sortable
    />
    <vxe-column
      field="sex"
      title="客户性别"
      formatter="formatSex"
    />
    <vxe-column
      field="age"
      title="年龄"
      sortable
    />
    <vxe-column
      field="address"
      title="地址"
    />
    <vxe-column
      field="date"
      title="日期"
      formatter="formatDate"
      sortable
    />
    <vxe-column
      title="操作"
      width="100"
    >
	<el-button type="text">查看</el-button>
	<el-button type="text">编辑</el-button>
	<el-button type="text">删除</el-button>
    </vxe-column>
  </vxe-table>
  <vxe-modal
	v-if="showEdit"
    v-model="showEdit"
    :title="selectRow ? '编辑&保存' : '新增&保存'"
    width="800"
    min-width="600"
    min-height="300"
    resize
    destroy-on-close
  >
    <template #default>
      <vxe-form
        :data="formData"
        :rules="formRules"
        title-align="right"
        title-width="100"
        @submit="submitEvent"
      >
        <vxe-form-item
          title="Basic information"
          title-align="left"
          :title-width="200"
          :span="24"
          :title-prefix="{ icon: 'fa fa-address-card-o' }"
        />
        <vxe-form-item
          field="name"
          title="Name"
          :span="12"
          :item-render="{}"
        >
          <template #default="{ data }">
            <vxe-input
              v-model="data.name"
              placeholder="请输入名称"
            />
          </template>
        </vxe-form-item>
        <vxe-form-item
          field="nickname"
          title="Nickname"
          :span="12"
          :item-render="{}"
        >
          <template #default="{ data }">
            <vxe-input
              v-model="data.name"
              placeholder="请输入名称"
            />
          </template>
        </vxe-form-item>
        <vxe-form-item
          field="role"
          title="Role"
          :span="12"
          :item-render="{}"
        >
          <template #default="{ data }">
            <vxe-input
              v-model="data.name"
              placeholder="请输入角色"
            />
          </template>
        </vxe-form-item>
        <vxe-form-item
          field="sex"
          title="Sex"
          :span="12"
          :item-render="{}"
        >
          <template #default="{ data }">
            <vxe-select
              v-model="data.sex"
              transfer
            >
              <vxe-option
                v-for="item in sexList"
                :key="item.value"
                :value="item.value"
                :label="item.label"
              />
            </vxe-select>
          </template>
        </vxe-form-item>
        <vxe-form-item
          field="age"
          title="Age"
          :span="12"
          :item-render="{}"
        >
          <template #default="{ data }">
            <vxe-input
              v-model="data.age"
              type="number"
              placeholder="请输入年龄"
            />
          </template>
        </vxe-form-item>
        <vxe-form-item
          field="flag1"
          title="是否单身"
          :span="12"
          :item-render="{}"
        >
          <template #default="{ data }">
            <vxe-radio-group v-model="data.flag1">
              <vxe-radio
                label="Y"
                content="是"
              />
              <vxe-radio
                label="N"
                content="否"
              />
            </vxe-radio-group>
          </template>
        </vxe-form-item>
        <vxe-form-item
          field="checkedList"
          title="可选信息"
          :span="24"
          :item-render="{}"
        >
          <template #default="{ data }">
            <vxe-checkbox-group v-model="data.checkedList">
              <vxe-checkbox
                label="1"
                content="运动、跑步"
              />
              <vxe-checkbox
                label="2"
                content="听音乐"
              />
              <vxe-checkbox
                label="3"
                content="爬山"
              />
              <vxe-checkbox
                label="4"
                content="吃美食"
              />
            </vxe-checkbox-group>
          </template>
        </vxe-form-item>
        <vxe-form-item
          title="Other information"
          title-align="left"
          :title-width="200"
          :span="24"
          :title-prefix="{ message: '请填写必填项', icon: 'fa fa-info-circle' }"
        />
        <vxe-form-item
          field="num"
          title="Number"
          :span="12"
          :item-render="{}"
        >
          <template #default="{ data }">
            <vxe-input
              v-model="data.num"
              type="number"
              placeholder="请输入数值"
            />
          </template>
        </vxe-form-item>
        <vxe-form-item
          field="date3"
          title="Date"
          :span="12"
          :item-render="{}"
        >
          <template #default="{ data }">
            <vxe-input
              v-model="data.date3"
              type="date"
              placeholder="请选择日期"
              transfer
            />
          </template>
        </vxe-form-item>
        <vxe-form-item
          field="address"
          title="Date"
          :span="24"
          :item-render="{}"
          :title-suffix="{
            message: '提示信息！！',
            icon: 'fa fa-question-circle',
          }"
        >
          <template #default="{ data }">
            <vxe-textarea
              v-model="data.address"
              :autosize="{ minRows: 2, maxRows: 4 }"
            />
          </template>
        </vxe-form-item>
        <vxe-form-item
          align="center"
          title-align="left"
          :span="24"
        >
          <template #default>
            <vxe-button type="submit">提交</vxe-button>
            <vxe-button type="reset">重置</vxe-button>
          </template>
        </vxe-form-item>
      </vxe-form>
    </template>
  </vxe-modal>
  <vxe-pager
    border
    size="medium"
    :loading="loading2"
    :current-page="tablePage2.currentPage"
    :page-size="tablePage2.pageSize"
    :total="tablePage2.totalResult"
    :layouts="[
      'PrevPage',
      'JumpNumber',
      'NextPage',
      'FullJump',
      'Sizes',
      'Total',
    ]"
    @page-change="handlePageChange2"
  />
<script>
export default {
  data() {
    return {
      selectRow: null,
      formData: null,
      showEdit: false,
      tableData2: [],
      tablePage2: {
        currentPage: 1,
        pageSize: 10,
        totalResult: 0,
      },
      formRules: {
        name: [
          { required: true, message: '请输入名称' },
          { min: 3, max: 5, message: '长度在 3 到 5 个字符' },
        ],
        nickname: [{ required: true, message: '请输入昵称' }],
        sex: [{ required: true, message: '请选择性别' }],
      },
    }
  },
  created() {	
    this.findList2()
  },
  methods: {
    findList2() {
      this.loading2 = true
      setTimeout(() => {
        const list = [
          {
            id: 10001,
            name: 'Test1',
            nickname: 'T1',
            role: 'Develop',
            sex: '1',
            age: 28,
            address: 'Shenzhen',
            date: 165994468,
          },
          {
            id: 10002,
            name: 'Test2',
            nickname: 'T2',
            role: 'Test',
            sex: '0',
            age: 22,
            address: 'Guangzhou',
            date: 161994468,
          },
          {
            id: 10003,
            name: 'Test3',
            nickname: 'T3',
            role: 'PM',
            sex: '1',
            age: 32,
            address: 'Shanghai',
            date: 161294468,
          },
          {
            id: 10004,
            name: 'Test4',
            nickname: 'T4',
            role: 'Designer',
            sex: '0',
            age: 23,
            address: 'Shenzhen',
            date: 161294468,
          },
          {
            id: 10005,
            name: 'Test5',
            nickname: 'T5',
            role: 'Develop',
            sex: '0',
            age: 30,
            address: 'Shanghai',
            date: 161294268,
          },
          {
            id: 10006,
            name: 'Test6',
            nickname: 'T6',
            role: 'Develop',
            sex: '0',
            age: 27,
            address: 'Shanghai',
            date: 165994168,
          },
          {
            id: 10007,
            name: 'Test7',
            nickname: 'T1',
            role: 'Develop',
            sex: '1',
            age: 28,
            address: 'Shenzhen',
            date: 165894168,
          },
          {
            id: 10008,
            name: 'Test8',
            nickname: 'T2',
            role: 'Test',
            sex: '0',
            age: 22,
            address: 'Guangzhou',
            date: 165864168,
          },
          {
            id: 10009,
            name: 'Test9',
            nickname: 'T3',
            role: 'PM',
            sex: '1',
            age: 32,
            address: 'Shanghai',
            date: 165894168,
          },
          {
            id: 100010,
            name: 'Test10',
            nickname: 'T4',
            role: 'Designer',
            sex: '0',
            age: 23,
            address: 'Shenzhen',
            date: 163894168,
          },
          {
            id: 100011,
            name: 'Test11',
            nickname: 'T5',
            role: 'PM',
            sex: '0',
            age: 35,
            address: 'Shenzhen',
            date: 162894168,
          },
          {
            id: 100012,
            name: 'Test12',
            nickname: 'T6',
            role: 'Designer',
            sex: '1',
            age: 25,
            address: 'Shanghai',
            date: 164897168,
          },
          {
            id: 100013,
            name: 'Test13',
            nickname: 'T9',
            role: 'Develop',
            sex: '1',
            age: 33,
            address: 'Shenzhen',
            date: 162897168,
          },
          {
            id: 100014,
            name: 'Test14',
            nickname: 'T6',
            role: 'Develop',
            sex: '0',
            age: 21,
            address: 'Shanghai',
            date: 162897168,
          },
          {
            id: 100015,
            name: 'Test15',
            nickname: 'T6',
            role: 'Develop',
            sex: '0',
            age: 19,
            address: 'Shanghai',
            date: 165897968,
          },
          {
            id: 100016,
            name: 'Test16',
            nickname: 'T8',
            role: 'Develop',
            sex: '1',
            age: 29,
            address: 'Shenzhen',
            date: 160897168,
          },
        ]
        this.loading2 = false
        this.tablePage2.totalResult = list.length
        this.tableData2 = list.slice(
          (this.tablePage2.currentPage - 1) * this.tablePage2.pageSize,
          this.tablePage2.currentPage * this.tablePage2.pageSize,
        )
      }, 300)
    },
    handlePageChange2({ currentPage, pageSize }) {
      this.tablePage2.currentPage = currentPage
      this.tablePage2.pageSize = pageSize
      this.findList2()
    },
    toolBarFunc(type) {
      this.$message(type)
    }
  },
}
</script>
```
:::
### 配置说明

table表格Json配置的数据结构字段说明

:::demo no-code
```html
<el-collapse>
  <el-collapse-item title="id" name="id">
    <div>类型为字符串，当前页面唯一即可</div>
  </el-collapse-item>
  <el-collapse-item title="element" name="element">
    <div>类型为字符串，此处应该为'table'，其他可选值：form，table，modal，button等</div>
  </el-collapse-item>
  <el-collapse-item title="getData" name="getData">
    <div>类型为函数，返回值一般为对象，对象可能包含的属性如下：（也可以自定义返回值）</div>
      <el-collapse class="code-demo marginBottom">
        <el-collapse-item title="代码示例">
          <pre style="color:#666;">
getData: () => {
  return {
    url: '/staff/list',
    method: 'post',
    data: {
      ...
    }
  }
}
          </pre>
        </el-collapse-item>
      </el-collapse>
    <vxe-table
      :data="getData">
      <vxe-column field="name" title="属性"></vxe-column>
      <vxe-column field="desc" title="说明"></vxe-column>
      <vxe-column field="type" title="类型/返回类型"></vxe-column>
      <vxe-column field="value" title="可选值"></vxe-column>
      <vxe-column field="default" title="默认值"></vxe-column>
    </vxe-table>
  </el-collapse-item>
  <el-collapse-item title="getConfig" name="getConfig">
    <div>类型为函数，返回值一般为对象，对象可能包含的属性如下：</div>
      <el-collapse class="code-demo marginBottom">
        <el-collapse-item title="代码示例">
          <pre style="color:#666;">
getConfig: () => {
  return {
    elementProp: {},
    lowcodeProp: {
      filterFieldsByAuth: () => {
        return {
          url: '/auth/xxxx',
          method: 'post',
        }
      },
      tableTitle: '关联公司',
      toolBar: [
        {},
        ...
      ],
      getFields: () => {
        return [
          {},
          ...
        ]
      },
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
        getData: [
          { name: 'url', desc: 'api请求地址', type: 'string', value: '', default: '' },
          { name: 'method', desc: 'api请求方式', type: 'sting', value: 'post,get', default: '' },
          { name: 'data', desc: 'api请求参数', type: 'any', value: '', default: 'null' },
        ],
        queryData: [
          { name: 'url', desc: 'api请求地址', type: 'string', value: '', default: '' },
          { name: 'method', desc: 'api请求方式', type: 'sting', value: 'post,get', default: '' },
          { name: 'data', desc: 'api请求参数', type: 'any', value: '', default: 'null' },
        ],
        getConfig: [
          { 
            name: 'elementProp',
            desc: 'element-ui参数，table这里不需要做自定义，直接定义为空对象{}即可',
            type: 'object',
            value: '{}',
            default: '{}',
            // children: [
            //   {
            //     name: 'label-width',
            //     desc: '标签宽度',
            //     type: 'string',
            //     value: 'auto或具体多少px，例如100px',
            //     default: 'auto',
            //   },
            //   {
            //     name: 'span',
            //     desc: '每行几个元素',
            //     type: 'number',
            //     value: '',
            //     default: '',
            //   }
            // ]
          },
          { 
            name: 'lowcodeProp',
            desc: '低代码参数',
            type: 'object',
            value: '{}',
            default: '{}',
            children: [
              {
                name: 'filterFieldsByAuth',
                desc: '权限接口控制：类型为函数，返回值为对象，包含的属性如下：',
                type: '',
                value: '',
                default: '',
                children: [
                  {
                    name: 'url',
                    desc: '权限Api接口请求地址',
                    type: 'string',
                    value: '',
                    default: '',
                  },
                  {
                    name: 'method',
                    desc: '权限Api接口请求地址',
                    type: 'string',
                    value: 'post,get',
                    default: '',
                  }
                ]
              },
              {
                name: 'tableTitle',
                desc: '类型为字符串，定义表格的标题',
                type: 'string',
                value: '',
                default: '',
              },
              {
                name: 'toolBar',
                desc: '类型为数组，定义表格的工具按钮，新增、删除等，具体按钮配置可见按钮说明文档',
                type: 'Array',
                value: '[]',
                default: '[]',
              },
              {
                name: 'getFields',
                desc: '类型为函数，返回值为数组，具体元素类型见下方元素说明',
                type: '',
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
### 元素说明

table表格里单元格的字段说明，对应getConfig-lowcodeProp-getFields里面的内容

:::demo no-code
```html
<el-collapse>
  <el-collapse-item title="checkbox 复选框" name="1">
      <el-collapse class="code-demo marginBottom">
        <div>checkbox配置一般放在getFields数组的第一项，这样默认会放到最左边。如果其他列设置了fixed属性，那么这里同样也要设置。</div>
        <el-collapse-item title="代码示例">
          <pre style="color:#666;">
{
  width: 100, //复选框单元格宽度
  fixed: '',// 固定在最左或最右，left|right
  type: 'checkbox',
},
{
  field: 'name',
  title: '姓名',
},
{
  field: 'sex',
  title: '性别',
},
{
  field: 'age',
  title: '年龄',
},
          </pre>
        </el-collapse-item>
      </el-collapse>
    <vxe-table
      border
      ref="xTable1"
      :data="tableData">
      <vxe-column type="checkbox" width="60"></vxe-column>
      <vxe-column field="name" title="姓名"></vxe-column>
      <vxe-column field="sex" title="性别"></vxe-column>
      <vxe-column field="age" title="年龄"></vxe-column>
    </vxe-table>
  </el-collapse-item>
</el-collapse>
<el-collapse>
  <el-collapse-item title="sortable 排序" name="1">
      <el-collapse class="code-demo marginBottom">
        <el-collapse-item title="代码示例">
          <pre style="color:#666;">
{
  field: 'name',
  title: '姓名',
  // 当前列不支持排序
},
{
  field: 'sex',
  title: '性别',
  sortable: true,// 当前列支持排序
},
{
  field: 'age',
  title: '年龄',
  sortable: true,// 当前列支持排序
},
          </pre>
        </el-collapse-item>
      </el-collapse>
    <vxe-table
      border
      ref="xTable1"
      :data="tableData">
      <vxe-column field="name" title="姓名"></vxe-column>
      <vxe-column field="sex" title="性别" sortable></vxe-column>
      <vxe-column field="age" title="年龄" sortable></vxe-column>
    </vxe-table>
  </el-collapse-item>
</el-collapse>
<el-collapse>
  <el-collapse-item title="fixed 固定列" name="1">
      <el-collapse class="code-demo marginBottom">
        <el-collapse-item title="代码示例">
          <pre style="color:#666;">
{
  field: 'name',
  title: '姓名',
  // 当前列不支持排序
},
{
  field: 'sex',
  title: '性别',
  sortable: true,// 当前列支持排序
},
{
  field: 'age',
  title: '年龄',
  sortable: true,// 当前列支持排序
},
          </pre>
        </el-collapse-item>
      </el-collapse>
    <vxe-table
      border
      ref="xTable1"
      :data="tableData">
      <vxe-column field="id" title="ID" fixed="left" width="300"></vxe-column>
      <vxe-column field="name" title="姓名" width="300"></vxe-column>
      <vxe-column field="sex" title="性别" width="300" sortable></vxe-column>
      <vxe-column field="age" title="年龄" width="300" sortable></vxe-column>
      <vxe-column field="address" title="地址" fixed="right" width="300"></vxe-column>
    </vxe-table>
  </el-collapse-item>
</el-collapse>
<el-collapse>
  <el-collapse-item title="formatter 数据格式化" name="1">
      <el-collapse class="code-demo marginBottom">
        <div>此处create_time的返回值可能是时间戳，需要转成 yyyy-MM-dd HH:mm:ss 的格式。可选值：TimeToDate、NumToString，后续待更新</div>
        <el-collapse-item title="代码示例">
          <pre style="color:#666;">
{
  field: 'create_time',
  title: '添加时间',
  formatter: 'TimeToDate',// 格式化方法
  sortable: true,
}
          </pre>
        </el-collapse-item>
      </el-collapse>
    <vxe-table
      border
      ref="xTable1"
      :data="tableData">
      <vxe-column field="id" title="ID" width="100"></vxe-column>
      <!-- <vxe-column field="name" title="姓名"></vxe-column>
      <vxe-column field="sex" title="性别"></vxe-column>
      <vxe-column field="age" title="年龄"></vxe-column> -->
      <vxe-column field="time" title="时间戳"></vxe-column>
      <vxe-column field="time" title="普通日期" formatter="formatDate"></vxe-column>
    </vxe-table>
  </el-collapse-item>
</el-collapse>
<el-collapse>
  <el-collapse-item title="titlePrefix 列标题说明" name="1">
      <el-collapse class="code-demo marginBottom">
        <div></div>
        <el-collapse-item title="代码示例">
          <pre style="color:#666;">
{
  field: 'name',
  title: '姓名',
  titlePrefix: { content: '用户姓名' }
}
          </pre>
        </el-collapse-item>
      </el-collapse>
    <vxe-table
      border
      ref="xTable1"
      :data="tableData">
      <vxe-column field="name" title="姓名" :title-prefix="tips"></vxe-column>
      <vxe-column field="sex" title="性别"></vxe-column>
      <vxe-column field="age" title="年龄"></vxe-column>
    </vxe-table>
  </el-collapse-item>
</el-collapse>
<el-collapse>
  <el-collapse-item title="input 单元格输入框" name="1">
      <el-collapse class="code-demo marginBottom">
        <div></div>
        <el-collapse-item title="代码示例">
          <pre style="color:#666;">
{
  field: 'name',
  title: '姓名',
  editRender: 'MyInput',
},
          </pre>
        </el-collapse-item>
      </el-collapse>
    <vxe-table
      border
      ref="xTable1"
      show-overflow
      :data="tableData">
      <vxe-column field="name" title="姓名" :edit-render="{}">
        <template slot-scope="row">
          <vxe-input v-model="row.name" type="text"></vxe-input>
        </template>
        <el-input v-model="input" placeholder="请输入内容"></el-input>
      </vxe-column>
      <vxe-column field="sex" title="性别"></vxe-column>
      <vxe-column field="age" title="年龄"></vxe-column>
    </vxe-table>
  </el-collapse-item>
</el-collapse>
<el-collapse>
  <el-collapse-item title="getCellRenderAtrrs 操作按钮" name="1">
      <el-collapse class="code-demo marginBottom">
        <div></div>
        <el-collapse-item title="代码示例">
          <pre style="color:#666;">
{
  field: 'oprate',
  title: '操作',
  width: 160,
  fixed: 'right',
  cellRender: 'OprateButton',
  getCellRenderAtrrs: () => {
    return [
      {
        name: '编辑',
        action: function() {
          return {
            type: 'modal',
            element: 'add-page',
          }
        },
        position: 'left',// 当前按钮固定在左边，剩下放到更多操作里
      },
      {
        name: '删除',
        action: function() {
          // 删除弹窗
        },
      },
    ]
  }
}
          </pre>
        </el-collapse-item>
      </el-collapse>
    <vxe-table
      border
      ref="xTable1"
      :data="tableData">
      <!-- <vxe-column field="name" title="姓名" :title-prefix="tips"></vxe-column> -->
      <vxe-column field="name" title="姓名"></vxe-column>
      <vxe-column field="sex" title="性别"></vxe-column>
      <vxe-column field="age" title="年龄"></vxe-column>
      <vxe-column title="操作" width="180" show-overflow>
        <template slot-scope="scope">
          <el-button type="text" @click="handleClick('编辑')">编辑</el-button>
          <el-divider direction="vertical"></el-divider>
          <el-dropdown>
            <el-button type="text">
              更多操作<i class="el-icon-arrow-down el-icon--right"></i>
            </el-button>
            <el-dropdown-menu slot="dropdown">
              <el-dropdown-item>查看</el-dropdown-item>
              <el-dropdown-item>删除</el-dropdown-item>
              <el-dropdown-item>禁用</el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown>
        </template>
      </vxe-column>
    </vxe-table>
    <el-dialog :title="modalTitle" :visible.sync="dialogFormVisible">
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
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="dialogFormVisible = false">确 定</el-button>
      </div>
    </el-dialog>
  </el-collapse-item>
</el-collapse>

<script>
  let id = 0;
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
        dialogFormVisible: false,
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
        modalTitle: '',
        formLabelWidth: '120px'
      };
    },
    methods: {
      handleClick(msg) {
        this.dialogFormVisible = true
        this.modalTitle = msg
      }
    }
  }
</script>
```