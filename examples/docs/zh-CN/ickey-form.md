## Ickey-Form-Table

Form + Table


:::demo ickey-form: 如果希望某个表单项或某个表单组件的尺寸不同于 Form 上的`size`属性，直接为这个表单项或表单组件设置自己的`size`即可。
```html
  <el-form ref="form" :model="sizeForm" style="overflow:hidden" label-width="80px" size="mini">
    <el-col :span="8">
      <el-form-item label="会员账号">
        <el-input v-model="sizeForm.account" disabled placeholder="请输入会员账号" />
      </el-form-item>
    </el-col>
    <el-col :span="8">
      <el-form-item label="会员ID">
        <el-input v-model="sizeForm.ID" placeholder="请输入会员ID" />
      </el-form-item>
    </el-col>
    <el-col :span="8">
      <el-form-item label="用户名">
        <el-input v-model="sizeForm.name" placeholder="请输入用户名" />
      </el-form-item>
    </el-col>
    <el-col :span="8">
      <el-form-item label="公司名称">
        <el-input v-model="sizeForm.company_name" placeholder="请输入公司名称" />
      </el-form-item>
    </el-col>
    <el-col :span="8">
      <el-form-item label="会员等级">
        <el-input v-model="sizeForm.account_level" placeholder="请输入会员等级" />
      </el-form-item>
    </el-col>
    <el-col :span="8">
      <el-form-item label="客户类型">
        <el-select v-model="sizeForm.client_type" placeholder="请选择客户类型">
          <el-option label="大客户" value="1" />
          <el-option label="一般客户" value="2" />
        </el-select>
      </el-form-item>
    </el-col>
    <el-col :span="8">
      <el-form-item label="产品类型">
        <el-cascader :props="props" placeholder="请选择产品类型" filterable />
      </el-form-item>
    </el-col>
    <el-col :span="8">
      <el-form-item label="注册时间">
        <el-date-picker
          v-model="sizeForm.register_time"
          type="date"
          placeholder="选择注册时间"
        />
      </el-form-item>
    </el-col>
    <el-col :span="12">
      <el-form-item label="最后下单时间">
        <el-date-picker
          v-model="sizeForm.order_time"
          type="daterange"
          start-placeholder="开始日期"
          end-placeholder="结束日期"
        />
      </el-form-item>
    </el-col>

    <el-col :span="8">
      <el-form-item size="large">
        <el-button type="primary" size="mini" @click="onSubmit">查询</el-button>
        <el-button size="mini" @click="resetForm('form')">重置</el-button>
      </el-form-item>
    </el-col>
  </el-form>

  <!-- table -->
  <vxe-table
    ref="xTable"
    border
    show-overflow
    keep-source
    max-height="400"
    row-id="id"
    size="medium"
    :loading="loading2"
    :data="tableData2"
  >
    <vxe-column type="checkbox" width="60" />
    <vxe-column type="seq" title="id" width="60" sortable />
    <vxe-column field="name" title="客户名称" sortable />
    <vxe-column field="sex" title="客户性别" formatter="formatSex" />
    <vxe-column field="age" title="年龄" sortable />
    <vxe-column field="address" title="地址" />
    <vxe-column field="date" title="日期" formatter="formatDate" fixed="right" sortable />
  </vxe-table>
  <vxe-pager
    border
    size="medium"
    :loading="loading2"
    :current-page="tablePage2.currentPage"
    :page-size="tablePage2.pageSize"
    :total="tablePage2.totalResult"
    :layouts="['PrevPage', 'JumpNumber', 'NextPage', 'FullJump', 'Sizes', 'Total']"
    @page-change="handlePageChange2"
  />
<script>
let id = 0
const cascaderArr = ['测试', '生产', '预发', '模拟', '开发', '用户']
export default {
  data() {
    return {
      props: {
        lazy: true,
        multiple: true,
        lazyLoad(node, resolve) {
          const { level } = node
          setTimeout(() => {
            const nodes = Array.from({ length: level + 1 }).map((item) => ({
              value: ++id,
              label:
                cascaderArr[Math.floor(Math.random() * 10)] || cascaderArr[0],
              leaf: level >= 2,
            }))
            // 通过调用resolve将子节点数据返回，通知组件数据加载完成
            resolve(nodes)
          }, 1000)
        },
      },
      sizeForm: {
        name: '',
        region: '',
        date1: '',
        date2: '',
        delivery: false,
        type: [],
        resource: '',
        desc: '',
        account: '',
        account_level: '',
        company_name: '',
        ID: '',
      },
      loading2: false,
      tableData2: [],
      tablePage2: {
        currentPage: 1,
        pageSize: 10,
        totalResult: 0,
      },
    }
  },
  created() {
    this.findList2()
  },
  methods: {
    onSubmit() {
      alert('查询表单')
    },
    resetForm(formName) {
      this.$refs[formName].resetFields()
    },
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
            date: 165994468
          },
          {
            id: 10002,
            name: 'Test2',
            nickname: 'T2',
            role: 'Test',
            sex: '0',
            age: 22,
            address: 'Guangzhou',
            date: 161994468
          },
          {
            id: 10003,
            name: 'Test3',
            nickname: 'T3',
            role: 'PM',
            sex: '1',
            age: 32,
            address: 'Shanghai',
            date: 161294468
          },
          {
            id: 10004,
            name: 'Test4',
            nickname: 'T4',
            role: 'Designer',
            sex: '0',
            age: 23,
            address: 'Shenzhen',
            date: 161294468
          },
          {
            id: 10005,
            name: 'Test5',
            nickname: 'T5',
            role: 'Develop',
            sex: '0',
            age: 30,
            address: 'Shanghai',
            date: 161294268
          },
          {
            id: 10006,
            name: 'Test6',
            nickname: 'T6',
            role: 'Develop',
            sex: '0',
            age: 27,
            address: 'Shanghai',
            date: 165994168
          },
          {
            id: 10007,
            name: 'Test7',
            nickname: 'T1',
            role: 'Develop',
            sex: '1',
            age: 28,
            address: 'Shenzhen',
            date: 165894168
          },
          {
            id: 10008,
            name: 'Test8',
            nickname: 'T2',
            role: 'Test',
            sex: '0',
            age: 22,
            address: 'Guangzhou',
            date: 165864168
          },
          {
            id: 10009,
            name: 'Test9',
            nickname: 'T3',
            role: 'PM',
            sex: '1',
            age: 32,
            address: 'Shanghai',
            date: 165894168
          },
          {
            id: 100010,
            name: 'Test10',
            nickname: 'T4',
            role: 'Designer',
            sex: '0',
            age: 23,
            address: 'Shenzhen',
            date: 163894168
          },
          {
            id: 100011,
            name: 'Test11',
            nickname: 'T5',
            role: 'PM',
            sex: '0',
            age: 35,
            address: 'Shenzhen',
            date: 162894168
          },
          {
            id: 100012,
            name: 'Test12',
            nickname: 'T6',
            role: 'Designer',
            sex: '1',
            age: 25,
            address: 'Shanghai',
            date: 164897168
          },
          {
            id: 100013,
            name: 'Test13',
            nickname: 'T9',
            role: 'Develop',
            sex: '1',
            age: 33,
            address: 'Shenzhen',
            date: 162897168
          },
          {
            id: 100014,
            name: 'Test14',
            nickname: 'T6',
            role: 'Develop',
            sex: '0',
            age: 21,
            address: 'Shanghai',
            date: 162897168
          },
          {
            id: 100015,
            name: 'Test15',
            nickname: 'T6',
            role: 'Develop',
            sex: '0',
            age: 19,
            address: 'Shanghai',
            date: 165897968
          },
          {
            id: 100016,
            name: 'Test16',
            nickname: 'T8',
            role: 'Develop',
            sex: '1',
            age: 29,
            address: 'Shenzhen',
            date: 160897168
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
  },
}
</script>
```
:::

### ickey-table 复杂表格

:::demo ickey-table
```html
<el-row>
  <el-button>默认按钮</el-button>
  <el-button type="primary">主要按钮</el-button>
  <el-button type="success">成功按钮</el-button>
  <el-button type="info">信息按钮</el-button>
  <el-button type="warning">警告按钮</el-button>
  <el-button type="danger">危险按钮</el-button>
</el-row>
<vxe-button type="submit" @click="insertEvent">新增</vxe-button>
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
      show-overflow
    >
      <template #default="{ row }">
        <vxe-button
          type="text"
          icon="fa fa-edit"
          @click="editEvent(row)"
        />
        <vxe-button
          type="text"
          icon="fa fa-trash-o"
        />
      </template>
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
    insertEvent() {
      this.formData = {
        name: '',
        nickname: '',
        role: '',
        sex: '',
        age: '',
        num: '',
        checkedList: [],
        flag1: '',
        date3: '',
        address: '',
      }
      this.selectRow = null
      this.showEdit = true
    },
    editEvent(row) {
      this.formData = {
        name: row.name,
        nickname: row.nickname,
        role: row.role,
        sex: row.sex,
        age: row.age,
        num: row.num,
        checkedList: row.checkedList,
        flag1: row.flag1,
        date3: row.date3,
        address: row.address,
      }
      this.selectRow = row
      this.showEdit = true
    },
    async removeEvent(row) {
      const type = await VXETable.modal.confirm('您确定要删除该数据?')
      const $table = this.$refs.xTable
      if (type === 'confirm') {
        $table.remove(row)
      }
    },
    submitEvent() {
      this.submitLoading = true
      setTimeout(() => {
        const $table = this.$refs.xTable
        this.submitLoading = false
        this.showEdit = false
        if (this.selectRow) {
          VXETable.modal.message({ content: '保存成功', status: 'success' })
          Object.assign(this.selectRow, this.formData)
        } else {
          VXETable.modal.message({ content: '新增成功', status: 'success' })
          $table.insert(this.formData)
        }
      }, 500)
    },
  },
}
</script>
```
:::

### Form Attributes

| 参数      | 说明          | 类型      | 可选值                           | 默认值  |
|---------- |-------------- |---------- |--------------------------------  |-------- |
| model   | 表单数据对象 | object      |                  —                |  — |
| rules    | 表单验证规则 | object | — | — |
| inline    | 行内表单模式 | boolean | — | false |
| label-position | 表单域标签的位置，如果值为 left 或者 right 时，则需要设置 `label-width` | string |  right/left/top            | right |
| label-width | 表单域标签的宽度，例如 '50px'。作为 Form 直接子元素的 form-item 会继承该值。支持 `auto`。 | string | — | — |
| label-suffix | 表单域标签的后缀 | string | — | — |
| hide-required-asterisk | 是否隐藏必填字段的标签旁边的红色星号 | boolean | — | false |
| show-message  | 是否显示校验错误信息 | boolean | — | true |
| inline-message  | 是否以行内形式展示校验信息 | boolean | — | false |
| status-icon  | 是否在输入框中显示校验结果反馈图标 | boolean | — | false |
| validate-on-rule-change  | 是否在 `rules` 属性改变后立即触发一次验证 | boolean | — | true |
| size  | 用于控制该表单内组件的尺寸 | string | medium / small / mini | — |
|  | 是否禁用该表单内的所有组件。若设置为 true，则表单内组件上的  属性不再生效 | boolean | — | false |

### Form Methods

| 方法名      | 说明          | 参数
|---------- |-------------- | --------------
| validate | 对整个表单进行校验的方法，参数为一个回调函数。该回调函数会在校验结束后被调用，并传入两个参数：是否校验成功和未通过校验的字段。若不传入回调函数，则会返回一个 promise | Function(callback: Function(boolean, object))
| validateField | 对部分表单字段进行校验的方法 | Function(props: array \| string, callback: Function(errorMessage: string))
| resetFields | 对整个表单进行重置，将所有字段值重置为初始值并移除校验结果 | —
| clearValidate | 移除表单项的校验结果。传入待移除的表单项的 prop 属性或者 prop 组成的数组，如不传则移除整个表单的校验结果 | Function(props: array \| string)

### Form Events
| 事件名称 | 说明    | 回调参数  |
|--------- |-------- |---------- |
| validate | 任一表单项被校验后触发 | 被校验的表单项 prop 值，校验是否通过，错误消息（如果存在） |

### Form-Item Attributes

| 参数      | 说明          | 类型      | 可选值                           | 默认值  |
|---------- |-------------- |---------- |--------------------------------  |-------- |
| prop    | 表单域 model 字段，在使用 validate、resetFields 方法的情况下，该属性是必填的 | string    | 传入 Form 组件的 `model` 中的字段 | — |
| label | 标签文本 | string | — | — |
| label-width | 表单域标签的的宽度，例如 '50px'。支持 `auto`。 | string |       —       | — |
| required | 是否必填，如不设置，则会根据校验规则自动生成 | boolean | — | false |
| rules    | 表单验证规则 | object | — | — |
| error    | 表单域验证错误信息, 设置该值会使表单验证状态变为`error`，并显示该错误信息 | string | — | — |
| show-message  | 是否显示校验错误信息 | boolean | — | true |
| inline-message  | 以行内形式展示校验信息 | boolean | — | false |
| size  | 用于控制该表单域下组件的尺寸 | string | medium / small / mini | - |

### Form-Item Slot
| name | 说明 |
|------|--------|
| — | Form Item 的内容 |
| label | 标签文本的内容 |

### Form-Item Scoped Slot
|  name  |   说明  |
|--------|--------|
|  error | 自定义表单校验信息的显示方式，参数为 { error } |

### Form-Item Methods

| 方法名      | 说明          | 参数
|---------- |-------------- | --------------
| resetField | 对该表单项进行重置，将其值重置为初始值并移除校验结果 | -
| clearValidate | 移除该表单项的校验结果 | -
