## Ickey-Form 复杂表单
###

:::demo ickey-form，直接拷贝mockdata部分即可生成整个表单。
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
      <el-form-item label="邮箱">
        <el-input v-model="sizeForm.email" placeholder="请输入邮箱" />
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
    <!-- <el-col :span="8">
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
    </el-col> -->

    <el-col :span="8">
      <el-form-item size="large">
        <el-button type="primary" size="mini" @click="onSubmit">查询</el-button>
        <el-button size="mini" @click="resetForm('form')">重置</el-button>
      </el-form-item>
    </el-col>
  </el-form>
<style>
  .el-select .el-input {
    width: 100%!important;
  }
</style>
<script>
let id = 0
const cascaderArr = ['测试', '生产', '预发', '模拟', '开发', '用户']
const mockdata = [
  {
    id: 'staffform',
    element: 'form',
    getData: () => {
      return {
        login_name: '张三用户名',
        name: '张三',
        work_code: '40056',
        department: '1',
        sitting_number: '3333356',
        test_radio: '2',
      }
    },
    queryData: (form) => {
      console.log('---querydata dd---:', form.data)
    },
    getConfig: () => {
      return {
        elementProp: {
          'label-width': 'auto',
          span: 6,
        },
        lowcodeProp: {
          getFields: () => {
            return [
              {
                type: 'checkbox'
              },
              {
                prop: 'login_name',
                element: 'input',
                label: '用户名',
              },
              {
                prop: 'sitting_number',
                element: 'input',
                label: '400电话',
                type: 'text',
                valueType: 'number',
              },
              {
                prop: 'name',
                element: 'input',
                label: '姓名',
              },
              {
                prop: 'work_code',
                element: 'input',
                label: 'OA工号',
              },
              {
                prop: 'test_radio',
                element: 'radio',
                label: 'OA工号',
                getData: () => {
                  return [
                    {
                      value: '1',
                      label: '部门一',
                    },
                    {
                      value: '2',
                      label: '部门二',
                    },
                  ]
                },
              },
              {
                prop: 'department',
                element: 'select',
                label: '部门',
                getData: () => {
                  return [
                    {
                      value: '1',
                      label: '部门一',
                    },
                    {
                      value: '2',
                      label: '部门二',
                    },
                  ]
                },
              },
              {
                prop: 'station',
                element: 'select',
                label: '岗位',
                getData: () => {
                  return [
                    {
                      value: '1',
                      label: '岗位一',
                    },
                    {
                      value: '2',
                      label: '岗位二',
                    },
                  ]
                },
              },
            ]
          },
          header: [],
          footer: [
            // {
            //   element: 'button',
            //   getConfig: () => {
            //     return [
            //       {
            //         name: '查询',
            //         action: function () {
            //           return {}
            //         },
            //         // position: 'left',
            //       },
            //       {
            //         name: '重置',
            //         action: function () {
            //           alert('我是一个自定义按钮')
            //         },
            //       },
            //     ]
            //   },
            // },
          ],
        },
      }
    },
  },
  {
    id: 'staffTable',
    element: 'table',
    getData() {
      // alert('此处可以为表单提供数据，也可以进行refresh')
      return {
        url: '/staff/list',
        method: 'post',
      }
      // return new Promise((resolve, reject) => {
      //   setTimeout(() => {
      //     const res = [
      //       {
      //         id: 1,
      //         name: '啊啊啊',
      //         test: 'test',
      //         login_name: '小张',
      //         sitting_number: '',
      //         qq: '3333',
      //       },
      //       {
      //         id: 2,
      //         name: 'bbbb',
      //         test: '34test',
      //         login_name: '小李',
      //         sitting_number: '',
      //         qq: '4444',
      //       },
      //     ]
      //     resolve(res)
      //   }, 500)
      // })
    },
    getConfig: () => {
      return {
        elementProp: {},
        lowcodeProp: {
          getFields: () => {
            return [
              { field: '', title: '', type: 'checkbox', width: 100 },
              { field: 'id', title: 'id', width: 100 },
              {
                field: 'login_name',
                title: '用户名',
                width: 100,
                editRender: 'MyInput',
                sortable: true,
                titlePrefix: { content: '用户名' },
                copy: false,
              },
              {
                field: 'sitting_number',
                title: '400工号',
                width: 160,
                sortable: true,
                formatter: 'NumToString',
              },
              {
                field: 'qq',
                title: 'QQ绑定号码',
                width: 30,
                editRender: 'MyInput',
                titlePrefix: { content: 'QQ绑定号码' },
              },
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
                      action: function () {
                        return {
                          type: 'modal',
                          element: 'add-page',
                        }
                      },
                      position: 'left',
                    },
                    {
                      name: '我是一个自定义按钮',
                      action: function () {
                        alert('我是一个自定义按钮')
                      },
                    },
                    {
                      name: '400关闭',
                      fields: 'sitting_number',
                      condition: 'notEmpty',
                      action: function () {
                        alert('调用400关闭的接口服务')
                      },
                    },
                    {
                      name: '400开启',
                      fields: 'sitting_number',
                      condition: 'empty',
                      action: function () {
                        alert('调用400开启的接口服务')
                      },
                    },
                    { name: '禁用' },
                    { name: '开启' },
                  ]
                },
              },
            ]
          },
          // header: [],
          // footer: [],
        },
      }
    },
  },
  {
    id: 'getSatff',
    element: 'button',
    getConfig() {
      return {
        name: '获取人员列表',
        type: 'primary',
        size: 'small',
        disabled() {
          return {
          }
        },
        action() {
          return {
            url: '/staff/list',
            data: {},
            method: 'post',
          }
        }
      }
    }
  },
  {
    id: 'submitForm',
    element: 'button',
    getConfig() {
      return {
        name: '查询',
        type: 'primary',
        icon: 'el-icon-search',
        action() {
          return {
            formId: 'staffform',
            tableId: 'staffTable',
            url: '/staff/list',
            method: 'post'
          }
        }
      }
    }
  },
  {
    id: 'resetForm',
    element: 'button',
    getConfig() {
      return {
        name: '重置',
        action() {
          return {
            formId: 'staffform',
            tableId: 'staffTable',
            formRef: 'staffform',
            url: '/staff/list',
            method: 'post',
            type: 'reset'
          }
        }
      }
    }
  },
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
            element: 'add-page'
          }
        },
      }
    }
  },
  {
    id: 'deleteStaff',
    element: 'button',
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
        action() {
          return {
            tableId: 'staffTable',
            url: '/staff/delete',
            method: 'post',
            params: 'ids:id'
          }
        }
      }
    }
  },
  {
    id: 'openLink',
    element: 'button',
    getConfig() {
      return {
        name: '打开新标签页',
        type: 'primary',
        action() {
          return {
            type: 'link',
            url: 'https://www.baidu.com/'
          }
        },
      }
    }
  },
  {
    id: 'routerLink',
    element: 'button',
    getConfig() {
      return {
        name: '路由跳转',
        type: 'primary',
        action() {
          return {
            type: 'link',
            url: '/user/staff'
          }
        },
      }
    }
  },
  {
    id: 'export',
    element: 'button',
    getConfig() {
      return {
        name: '导出',
        type: 'warning',
        action() {
          return {
            formId: 'staffform',
            url: '/user/export',
            method: 'post',
            params: 'department:department',
          }
        },
      }
    }
  },
  {
    id: 'drawer',
    element: 'button',
    getConfig() {
      return {
        name: 'form抽屉',
        type: 'primary',
        action() {
          return {
            type: 'drawer',
            element: 'add-page-drawer'
          }
        },
      }
    }
  },
  {
    id: 'upload',
    element: 'button',
    getConfig() {
      return {
        name: '上传',
        type: 'success',
        upload() {
          return {
            limit: 3,
            multiple: false,
            autoUpload: true,
            accept: '.js,.html,.vue,.png,.pdf',
          }
        },
        action() {
          return {
            method: 'get',
            url: '/user/upload-user-file'
          }
        },
      }
    }
  }
]
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
    }
  },
  methods: {
    onSubmit() {
      alert('查询表单')
    },
    resetForm(formName) {
      this.$refs[formName].resetFields()
    }
  },
}
</script>
```
:::
### 配置说明

form表单Json配置的数据结构字段说明

:::demo no-code
```html
<el-collapse>
  <el-collapse-item title="id" name="id">
    <div>类型为字符串，当前页面唯一即可</div>
  </el-collapse-item>
  <el-collapse-item title="element" name="element">
    <div>类型为字符串，此处应该为'form'，其他可选值：form，table，modal，button等</div>
  </el-collapse-item>
  <el-collapse-item title="getData" name="getData">
    <div>类型为函数，此处定义的对象为提交表单时请求api接口的body参数，需自定义，每个属性对应表单中的各个input、select元素绑定值</div>
      <el-collapse class="code-demo marginBottom">
        <el-collapse-item title="代码示例">
          <pre style="color:#666;">
getData: () => {
  return {
    login_name: '张三用户名',
    name: '张三',
    work_code: '40056',
    department: '1',
    sitting_number: '3333356',
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
  <el-collapse-item title="queryData" name="queryData">
    <div>类型为函数，一般不需要修改</div>
      <el-collapse class="code-demo marginBottom">
        <el-collapse-item title="代码示例">
          <pre style="color:#666;">
queryData: (form) => {},
          </pre>
        </el-collapse-item>
      </el-collapse>
    <!-- <vxe-table
      :data="queryData">
      <vxe-column field="name" title="属性"></vxe-column>
      <vxe-column field="desc" title="说明"></vxe-column>
      <vxe-column field="type" title="类型/返回类型"></vxe-column>
      <vxe-column field="value" title="可选值"></vxe-column>
      <vxe-column field="default" title="默认值"></vxe-column>
    </vxe-table> -->
  </el-collapse-item>
  <!-- <el-collapse-item title="getConfig" name="getConfig">
    <div>类型为函数，返回值一般为对象，对象可能包含的属性如下：（也可以自定义返回值）</div>
    <vxe-table
      :data="getConfig">
      <vxe-column field="name" title="属性"></vxe-column>
      <vxe-column field="desc" title="说明"></vxe-column>
      <vxe-column field="type" title="类型/返回类型"></vxe-column>
      <vxe-column field="value" title="可选值"></vxe-column>
      <vxe-column field="default" title="默认值"></vxe-column>
    </vxe-table>
  </el-collapse-item> -->
  <el-collapse-item title="getConfig" name="getConfig">
    <div>类型为函数，返回值一般为对象，对象可能包含的属性如下：</div>
      <el-collapse class="code-demo marginBottom">
        <el-collapse-item title="代码示例">
          <pre style="color:#666;">
getConfig: () => {
  return {
    elementProp: {
      'label-width': 'auto',
      span: 24,
    },
    lowcodeProp: {
      filterFieldsByAuth: () => {
        return {
          url: '/auth/xxxx',
          method: 'post',
        }
      },
      getFields: () => {
        return [
          {
            prop: 'company_name',
            element: 'input',
            label: '公司名称',
          }
        ]
      }
    }
  }
}
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
          { name: 'login_name', desc: '登录名称', type: 'string', value: '', default: '' },
          { name: 'name', desc: '用户名', type: 'sting', value: '', default: '' },
          { name: 'work_code', desc: '工号', type: 'string', value: '', default: '' },
          { name: '....', desc: '', type: '', value: '', default: '' },
        ],
        // queryData: [
        //   { name: 'url', desc: 'api请求地址', type: 'string', value: '', default: '' },
        //   { name: 'method', desc: 'api请求方式', type: 'sting', value: 'post,get', default: '' },
        //   { name: 'data', desc: 'api请求参数', type: 'any', value: '', default: 'null' },
        // ],
        getConfig: [
          { 
            name: 'elementProp',
            desc: 'element-ui参数',
            type: 'object',
            value: '{}',
            default: '{}',
            children: [
              {
                name: 'label-width',
                desc: '标签宽度',
                type: 'string',
                value: 'auto或具体多少px，例如100px',
                default: 'auto',
              },
              {
                name: 'span',
                desc: '每行几个元素',
                type: 'number',
                value: '',
                default: '',
              }
            ]
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

form表单里的各个元素的字段说明，对应getConfig-lowcodeProp-getFields里面的内容

:::demo no-code
```html
<el-collapse>
  <el-collapse-item title="input 输入框" name="1">
    <div style="color:#222;font-weight:700;">示例：</div>
    <el-form ref="form" :model="inputForm" style="overflow:hidden;margin-top:20px" label-width="80px" size="mini">
      <el-col :span="24">
        <el-form-item label="基础用法">
          <el-input v-model="inputForm.ID" placeholder="请输入名称" />
          <el-collapse class="code-demo">
            <el-collapse-item title="代码示例">
              <pre style="color:#666;">
{
  prop: 'work_code',
  element: 'input',
  label: 'OA工号'
}
              </pre>
            </el-collapse-item>
          </el-collapse>
        </el-form-item>
      </el-col>
      <el-col :span="24">
        <el-form-item label="禁用">
          <el-input v-model="inputForm.name" placeholder="请输入用户名" disabled />
          <el-collapse class="code-demo">
            <el-collapse-item title="代码示例">
              <pre style="color:#666;">
{
  prop: 'user_name',
  element: 'input',
  label: '用户名',
  disabled: true
}
              </pre>
            </el-collapse-item>
          </el-collapse>
        </el-form-item>
      </el-col>
      <el-col :span="24">
        <el-form-item label="密码">
          <el-input placeholder="请输入密码" v-model="inputForm.password" show-password></el-input>
          <el-collapse class="code-demo">
            <el-collapse-item title="代码示例">
              <pre style="color:#666;">
{
  prop: 'password',
  element: 'input',
  label: '密码',
  showPassword: true
}
              </pre>
            </el-collapse-item>
          </el-collapse>
        </el-form-item>
      </el-col>
      <el-col :span="24">
        <el-form-item label="参数格式化">
          <el-input placeholder="输入值为string，传参会格式化成number" v-model="inputForm.text"></el-input>
          <el-collapse class="code-demo">
            <el-collapse-item title="代码示例">
              <pre style="color:#666;">
{
  prop: 'sitting_number',
  element: 'input',
  label: '400电话',
  type: 'text',
  valueType: 'number',
}
              </pre>
            </el-collapse-item>
          </el-collapse>
        </el-form-item>
      </el-col>
      <el-col :span="24">
        <el-form-item label="可清空">
          <el-input
            placeholder="请输入内容"
            v-model="inputForm.input"
            clearable>
          </el-input>
          <el-collapse class="code-demo">
            <el-collapse-item title="代码示例">
              <pre style="color:#666;">
{
  prop: 'department',
  element: 'input',
  label: '部门',
  clearable: true
}
              </pre>
            </el-collapse-item>
          </el-collapse>
        </el-form-item>
      </el-col>
      <el-col :span="24">
        <el-form-item label="带icon(后)">
          <el-input
            placeholder="请输入日期"
            suffix-icon="el-icon-date"
            v-model="inputForm.input1">
          </el-input>
          <el-collapse class="code-demo">
            <el-collapse-item title="代码示例">
              <pre style="color:#666;">
{
  prop: 'department',
  element: 'input',
  label: '部门',
  'suffix-icon': 'el-icon-date'
}
              </pre>
            </el-collapse-item>
          </el-collapse>
        </el-form-item>
      </el-col>
      <el-col :span="24">
        <el-form-item label="带icon(前)">
          <el-input
            placeholder="请输入内容搜索"
            prefix-icon="el-icon-search"
            v-model="inputForm.input2">
          </el-input>
          <el-collapse class="code-demo">
            <el-collapse-item title="代码示例">
              <pre style="color:#666;">
{
  prop: 'department',
  element: 'input',
  label: '部门',
  'suffix-icon': 'el-icon-search'
}
              </pre>
            </el-collapse-item>
          </el-collapse>
        </el-form-item>
      </el-col>
      <el-col :span="24">
        <el-form-item label="文本域">
          <el-input
            type="textarea"
            :rows="2"
            placeholder="请输入内容"
            v-model="inputForm.textarea">
          </el-input>
          <el-collapse class="code-demo">
            <el-collapse-item title="代码示例">
              <pre style="color:#666;">
{
  prop: 'department',
  element: 'input',
  label: '部门',
  type: 'textarea'
}
              </pre>
            </el-collapse-item>
          </el-collapse>
        </el-form-item>
      </el-col>
    </el-form>
    <div class="attr">属性说明：</div>
    <vxe-table
      :data="inputData">
      <vxe-column field="name" title="属性"></vxe-column>
      <vxe-column field="desc" title="说明"></vxe-column>
      <vxe-column field="type" title="类型/返回类型"></vxe-column>
      <vxe-column field="value" title="可选值"></vxe-column>
      <vxe-column field="default" title="默认值"></vxe-column>
      <vxe-column field="required" title="是否必须"></vxe-column>
    </vxe-table>
  </el-collapse-item>
  <el-collapse-item title="select 下拉选择" name="select">
    <div style="color:#222;font-weight:700;">示例：</div>
      <el-form ref="form" :model="selectForm" style="overflow:hidden;margin-top:20px" label-width="80px" size="mini">
        <el-col :span="24">
          <el-form-item label="基础用法">
            <el-select v-model="selectForm.value" placeholder="请选择">
              <el-option
                v-for="item in selectForm.options"
                :key="item.value"
                :label="item.label"
                :value="item.value">
              </el-option>
            </el-select>
            <el-collapse class="code-demo">
              <el-collapse-item title="代码示例，枚举型">
                <pre style="color:#666;">
{
  prop: 'station',
  element: 'select',
  label: '岗位',
  getData: () => {
    return [
      {
        value: '1',
        label: '岗位一'
      },
      {
        value: '2',
        label: '岗位二'
      }
    ]
  }
}
                </pre>
              </el-collapse-item>
            </el-collapse>
          </el-form-item>
        </el-col>
        <el-col :span="24">
          <el-form-item label="多选">
            <el-select v-model="selectForm.value1" multiple placeholder="请选择">
              <el-option
                v-for="item in selectForm.options1"
                :key="item.value"
                :label="item.label"
                :value="item.value">
              </el-option>
            </el-select>
            <el-collapse class="code-demo">
              <el-collapse-item title="代码示例，后台获取">
                <pre style="color:#666;">
{
  prop: 'department',
  element: 'select',
  label: '部门',
  multiple: true,// 多选
  getData: () => {
    return {
      method: 'post',
      url: '/staff/department-list'
    }
  }
}
                </pre>
              </el-collapse-item>
            </el-collapse>
          </el-form-item>
        </el-col>
        <el-col :span="24">
          <el-form-item label="可搜索">
            <el-select v-model="selectForm.value2" filterable placeholder="输入关键字，搜索结果">
              <el-option
                v-for="item in selectForm.options2"
                :key="item.value"
                :label="item.label"
                :value="item.value">
              </el-option>
            </el-select>
            <el-collapse class="code-demo">
              <el-collapse-item title="代码示例，后台获取">
                <pre style="color:#666;">
{
  prop: 'menu',
  element: 'select',
  label: '菜单',
  filterable: true,// 搜索
  getData: () => {
    return {
      method: 'post',
      url: '/staff/menu-list'
    }
  }
}
                </pre>
              </el-collapse-item>
            </el-collapse>
          </el-form-item>
        </el-col>
      </el-form>
    <div class="attr">属性说明：</div>
    <vxe-table
      :data="selectData">
      <vxe-column field="name" title="属性"></vxe-column>
      <vxe-column field="desc" title="说明"></vxe-column>
      <vxe-column field="type" title="类型/返回类型"></vxe-column>
      <vxe-column field="value" title="可选值"></vxe-column>
      <vxe-column field="default" title="默认值"></vxe-column>
      <vxe-column field="required" title="是否必须"></vxe-column>
    </vxe-table>
  </el-collapse-item>
  <el-collapse-item title="date 日期时间选择" name="date">
    <el-form ref="form" :model="dateForm" style="overflow:hidden;margin-top:20px" label-width="80px" size="mini">
      <el-col :span="24">
        <el-form-item label="日期">
        <el-date-picker
          v-model="dateForm.value"
          type="date"
          placeholder="选择日期">
        </el-date-picker>
          <el-collapse class="code-demo">
            <el-collapse-item title="代码示例">
              <pre style="color:#666;">
{
  prop: 'registerDate',
  element: 'datepicker',
  label: '注册日期'
}
              </pre>
            </el-collapse-item>
          </el-collapse>
        </el-form-item>
      </el-col>
      <el-col :span="24">
        <el-form-item label="日期时间">
        <el-date-picker
          v-model="dateForm.value1"
          type="datetime"
          placeholder="选择日期和时间">
        </el-date-picker>
          <el-collapse class="code-demo">
            <el-collapse-item title="代码示例">
              <pre style="color:#666;">
{
  prop: 'registerTime',
  element: 'datepicker',
  label: '注册时间',
  type: 'datetime'
}
              </pre>
            </el-collapse-item>
          </el-collapse>
        </el-form-item>
      </el-col>
      <el-col :span="24">
        <el-form-item label="日期时间范围">
        <el-date-picker
          v-model="dateForm.value2"
          type="datetimerange"
          placeholder="选择日期">
        </el-date-picker>
          <el-collapse class="code-demo">
            <el-collapse-item title="代码示例">
              <pre style="color:#666;">
{
  prop: 'registerTimeRange',
  element: 'datepicker',
  label: '注册时间范围',
  type: 'datetimerange'
}
              </pre>
            </el-collapse-item>
          </el-collapse>
        </el-form-item>
      </el-col>
    </el-form>
    <div class="attr">属性说明：</div>
    <vxe-table
      :data="dateData">
      <vxe-column field="name" title="属性"></vxe-column>
      <vxe-column field="desc" title="说明"></vxe-column>
      <vxe-column field="type" title="类型/返回类型"></vxe-column>
      <vxe-column field="value" title="可选值"></vxe-column>
      <vxe-column field="default" title="默认值"></vxe-column>
      <vxe-column field="required" title="是否必须"></vxe-column>
    </vxe-table>
  </el-collapse-item>
  <el-collapse-item title="cascade 级联选择" name="cascader">
    <el-form ref="form" :model="cascaderForm" style="overflow:hidden;margin-top:20px" label-width="80px" size="mini">
      <el-col :span="24">
        <el-form-item label="基本用法">
          <el-cascader
            v-model="cascaderForm.value"
            :options="cascaderForm.options"
            @change="handleChange">
          </el-cascader>
          <el-collapse class="code-demo">
            <el-collapse-item title="代码示例">
              <pre style="color:#666;">
{
  prop: 'cascader',
  element: 'cascader',
  label: '选择类型',
  getData: () => {
    return [
      {
        value: 'zhinan',
        label: '指南',
        children: [{
          value: 'shejiyuanze',
          label: '设计原则',
          children: [{
            value: 'yizhi',
            label: '一致'
          }, {
            value: 'kekong',
            label: '可控'
          }]
        }]
      },
      {
        value: 'zujian',
        label: '组件',
      }
    ]
  }
}
              </pre>
            </el-collapse-item>
          </el-collapse>
        </el-form-item>
      </el-col>
      <el-col :span="24">
        <el-form-item label="多选">
        <el-cascader
          :options="cascaderForm.options"
          :props="{ multiple: true }"
          clearable></el-cascader>
          <el-collapse class="code-demo">
            <el-collapse-item title="代码示例">
              <pre style="color:#666;">
{
  props: 'cascader',
  element: 'cascader',
  multiple: true,// 多选
  label: '产品类型',
  getData: () => {
    return [
      {
        value: 'zhinan',
        label: '指南',
        children: [{
          value: 'shejiyuanze',
          label: '设计原则',
          children: [{
            value: 'yizhi',
            label: '一致'
          }, {
            value: 'kekong',
            label: '可控'
          }]
        }]
      },
      {
        value: 'zujian',
        label: '组件',
      }
    ]
  }
}
              </pre>
            </el-collapse-item>
          </el-collapse>
        </el-form-item>
      </el-col>
      <el-col :span="24">
        <el-form-item label="动态加载">
        <el-cascader :props="props"></el-cascader>
          <el-collapse class="code-demo">
            <el-collapse-item title="代码示例">
              <pre style="color:#666;">
{
  props: 'cascader',
  element: 'cascader',
  level: 3,
  multiple: true,
  label: '产品类型',
  getData: () => {
    return {
      method: 'post',
      url: '/staff/station-list',
      handleSelectChange: (data) => {
        const { value, label, level } = data || {}
        return {
          url: '/getson/id',
          data: data,
          method: 'post',
        }
      },
    }
  },
}
              </pre>
            </el-collapse-item>
          </el-collapse>
        </el-form-item>
      </el-col>
    </el-form>
    <div class="attr">属性说明：</div>
    <vxe-table
      :data="cascaderData">
      <vxe-column field="name" title="属性"></vxe-column>
      <vxe-column field="desc" title="说明"></vxe-column>
      <vxe-column field="type" title="类型/返回类型"></vxe-column>
      <vxe-column field="value" title="可选值"></vxe-column>
      <vxe-column field="default" title="默认值"></vxe-column>
      <vxe-column field="required" title="是否必须"></vxe-column>
    </vxe-table>
  </el-collapse-item>
</el-collapse>
<script>
  let id = 0;
  export default {
    data() {
      return {
        props: {
          lazy: true,
          lazyLoad (node, resolve) {
            const { level } = node;
            setTimeout(() => {
              const nodes = Array.from({ length: level + 1 })
                .map(item => ({
                  value: ++id,
                  label: `选项${id}`,
                  leaf: level >= 2
                }));
              // 通过调用resolve将子节点数据返回，通知组件数据加载完成
              resolve(nodes);
            }, 1000);
          }
        },
        inputForm: {},
        dateForm: {},
        cascaderForm: {
          value: '',
          options: [
            {
              value: 'zhinan',
              label: '指南',
              children: [{
                value: 'shejiyuanze',
                label: '设计原则',
                children: [{
                  value: 'yizhi',
                  label: '一致'
                }, {
                  value: 'kekong',
                  label: '可控'
                }]
              }]
            },
            {
              value: 'zujian',
              label: '组件',
            }
          ]
        },
        selectForm: {
          options: [{
            value: '1',
            label: '岗位一'
          }, {
            value: '2',
            label: '岗位二'
          }],
          value: '',
          value1: '',
          options1: [{
            value: '1',
            label: '部门一'
          }, {
            value: '2',
            label: '部门二'
          }, {
            value: '3',
            label: '部门二'
          }],
          value2: '',
          options2: [{
            value: '1',
            label: '人员列表'
          }, {
            value: '2',
            label: '权限列表'
          }, {
            value: '3',
            label: '仓储信息'
          }, {
            value: '4',
            label: '物流信息'
          }, {
            value: '5',
            label: '菜单管理'
          }],
        },
        inputData: [
          { name: 'prop', desc: '当前元素对应的接口字段', type: 'string', value: '', default: '', required: 'true' },
          { name: 'element', desc: '元素类型', type: 'sting', value: 'input', default: '',required: 'true' },
          { name: 'label', desc: '标签名称', type: 'string', value: '', default: '', required: 'true' },
          { name: 'type', desc: '输入值类型', type: 'string', value: '', default: '' },
          { name: 'valueType', desc: 'prop传值的类型，和type属性配合使用', type: 'string', value: '', default: '' },
          { name: 'disabled', desc: '是否禁用', type: 'boolean', value: 'true,false', default: 'false' },
          { name: 'showPassword', desc: '密码输入框', type: 'boolean', value: 'true,false', default: 'false' },
        ],
        selectData: [
          { name: 'prop', desc: '当前元素对应的接口字段', type: 'string', value: '', default: '',required: 'true' },
          { name: 'element', desc: '元素类型', type: 'sting', value: 'select', default: '',required: 'true' },
          { name: 'label', desc: '标签名称', type: 'string', value: '', default: '',required: 'true' },
          { name: 'disabled', desc: '是否禁用', type: 'boolean', value: 'true,false', default: 'false' },
          { name: 'getData', desc: '当前元素的数据从接口获取,具体用法参考配置说明-getData', type: 'function', value: '', default: '' },
        ],
        dateData: [
          { name: 'prop', desc: '当前元素对应的接口字段', type: 'string', value: '', default: '',required: 'true' },
          { name: 'element', desc: '元素类型', type: 'sting', value: 'datepicker', default: '',required: 'true' },
          { name: 'label', desc: '标签名称', type: 'string', value: '', default: '',required: 'true' },
          { name: 'type', desc: '类型', type: 'string', value: 'year,month,date,week,datetime,datetimerange,daterange', default: 'date' },
          { name: 'getData', desc: '当前元素的数据从接口获取,具体用法参考配置说明-getData', type: 'function', value: '', default: '' },
        ],
        cascaderData: [
          { name: 'prop', desc: '当前元素对应的接口字段', type: 'string', value: '', default: '',required: 'true' },
          { name: 'element', desc: '元素类型', type: 'sting', value: 'cascader', default: '',required: 'true' },
          { name: 'label', desc: '标签名称', type: 'string', value: '', default: '',required: 'true' },
          { name: 'multiple', desc: '支持多选', type: 'boolean', value: 'true,false', default: 'false' },
          { name: 'level', desc: '级联层级', type: 'number', value: '', default: '' },
          { name: 'getData', desc: '当前元素的数据从接口获取，具体用法参考配置说明-getData，handleSelectChange的用法和getData类似', type: 'function', value: '', default: '' },
        ]
      };
    },
    methods: {
      handleChange(val) {
        console.log(val);
      },
      remoteMethod(query) {
        if (query !== '') {
          this.loading = true;
          setTimeout(() => {
            this.loading = false;
            this.options = this.list.filter(item => {
              return item.label.toLowerCase()
                .indexOf(query.toLowerCase()) > -1;
            });
          }, 200);
        } else {
          this.options = [];
        }
      }
    }
  }
</script>
```
<!-- ::: -->
<!-- ### Form Attributes

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
| clearValidate | 移除该表单项的校验结果 | - -->
