<template>
  <div class="about">
    <h1>This is an stepTable page</h1>
    <Button type="primary"
            v-on:click='handleAddGongxuObj'>+点击添加工序</Button>
    <ul v-if='datas && datas.length>0'>
      <li v-for='(item,index) in datas'
          :key='item.id'>
        <Button class='i_btn'
                type="warning"
                @click='item.modal=true'>
          {{item.title}}
        </Button>
        <Modal v-model="item.modal"
               title="选择要添加的工部"
               @on-ok="ok(index)"
               @on-cancel="cancel">
          <div style="border-bottom: 1px solid #e9e9e9;padding-bottom:6px;margin-bottom:6px;">
            <Checkbox :indeterminate="indeterminate"
                      :value="checkAll"
                      @click.prevent.native="handleCheckAll">全选</Checkbox>
          </div>
          <CheckboxGroup v-model="checkAllGroup"
                         @on-change="checkAllGroupChange">
            <Checkbox label="工步一"></Checkbox>
            <Checkbox label="工步二"></Checkbox>
            <Checkbox label="工步三"></Checkbox>
            <Checkbox label="工步四"></Checkbox>
            <Checkbox label="工步五"></Checkbox>
          </CheckboxGroup>
        </Modal>
        <Table style="margin-top:6px;"
               border
               :columns="columns1"
               :data="item.gongbu"
               v-if='item.gongbu.length>0 && item.tableShow'></Table>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  components: {
  },
  data () {
    return {
      border: ['香蕉'],
      tableShow: false,
      indeterminate: true,
      checkAll: false,
      checkAllGroup: ['工步一', '工步二', '工步三', '工步四', '工步五'],
      checkAllGroup2: ['工步一', '工步二', '工步三', '工步四', '工步五'],
      modal1: false,
      datas: [
        /* { title: '+关联工步', modal: false, tableShow: true, gongbu: [] },
        { title: '+关联工步', modal: false, tableShow: true, gongbu: [] },
        { title: '+关联工步', modal: false, tableShow: true, gongbu: [] }, */
      ],
      columns1: [
        {
          title: '编号',
          key: 'number'
        },
        {
          title: '工步名称',
          key: 'Name_of_work_step'
        },
        {
          title: '工步描述',
          key: 'Job_description'
        },
        {
          title: '单位',
          key: 'unit'
        },
        {
          title: '工步工时',
          key: 'Working_hour',
          render: (h, params) => {
            const { Working_hour } = params.row
            const inp = h('input', {
              style: {
                width: '95%',
                padding: '4px 2px',
                borderRadius: '4px',
                border: '1px solid #e9eaec',
                textAlign: 'center'
              },
              attrs: {
                maxlength: 116
              },
              domProps: {
                value: Working_hour
              },
              on: {
                input: (event) => {
                  /* this.currentScore = event.target.value */
                }
              }
            })
            return inp
          }
        },
        {
          title: '工步数量',
          key: 'Working_number',
          render: (h, params) => {
            const { Working_number } = params.row
            const inp = h('input', {
              style: {
                width: '95%',
                padding: '4px 2px',
                borderRadius: '4px',
                border: '1px solid #e9eaec',
                textAlign: 'center'
              },
              attrs: {
                maxlength: 116
              },
              domProps: {
                value: Working_number
              },
              on: {
                input: (event) => {
                  /* this.currentScore = event.target.value */
                }
              }
            })
            return inp
          }
        },
        {
          title: '生产工时',
          key: 'Production_hours',
          render: (h, params) => {
            const { Production_hours } = params.row
            const inp = h('input', {
              style: {
                width: '95%',
                padding: '4px 2px',
                borderRadius: '4px',
                border: '1px solid #e9eaec',
                textAlign: 'center'
              },
              attrs: {
                maxlength: 116
              },
              domProps: {
                value: Production_hours
              },
              on: {
                input: (event) => {
                  /* this.currentScore = event.target.value */
                }
              }
            })
            return inp
          }
        },
        {
          title: '辅助时间',
          key: 'Auxiliary_time',
          render: (h, params) => {
            const { Auxiliary_time } = params.row
            const inp = h('input', {
              style: {
                width: '95%',
                padding: '4px 2px',
                borderRadius: '4px',
                border: '1px solid #e9eaec',
                textAlign: 'center'
              },
              attrs: {
                maxlength: 116
              },
              domProps: {
                value: Auxiliary_time
              },
              on: {
                input: (event) => {
                  /* this.currentScore = event.target.value */
                }
              }
            })
            return inp
          }
        },
        {
          title: '操作',
          key: 'operation',
          render: (h, params) => {
            console.log('h:', h, 'params:', params);

            return h('div', [
              h('Button', {
                props: {
                  type: 'primary',
                  size: 'small'
                },
                style: {
                  marginRight: '18px'
                },
                on: {
                  click: () => {
                    this.show(params.index)
                  }
                }
              }, 'View'),
              h('Button', {
                props: {
                  type: 'error',
                  size: 'small'
                },
                on: {
                  click: (key) => {
                    this.remove(params.index)
                    window.console.log('xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx', key)
                  }
                }
              }, 'Delete')
            ]);
          }
        }
      ],
      data1: [],
      arr: [],
      data2: [
        {
          idIndex: 0,
          Working_name: '工步一',
          number: 'BJ0265981',
          Name_of_work_step: 'John Brown1',
          Job_description: 'John Brown1',
          unit: '根1',
          Working_hour: 181,
          Working_number: 141,
          Production_hours: '自动计算',
          Auxiliary_time: '自动计算',
          operation: '删除'
        },
        {
          idIndex: 1,
          Working_name: '工步二',
          number: 'BK0288552',
          Name_of_work_step: 'John Brown2',
          Job_description: 'John Brown2',
          unit: '根2',
          Working_hour: 182,
          Working_number: 142,
          Production_hours: '自动计算',
          Auxiliary_time: '自动计算',
          operation: '删除'
        },
        {
          idIndex: 2,
          Working_name: '工步三',
          number: 'BK0288553',
          Name_of_work_step: 'John Brown3',
          Job_description: 'John Brown3',
          unit: '根3',
          Working_hour: 183,
          Working_number: 143,
          Production_hours: '自动计算',
          Auxiliary_time: '自动计算',
          operation: '删除'
        },
        {
          idIndex: 3,
          Working_name: '工步四',
          number: 'BK0288554',
          Name_of_work_step: 'John Brown4',
          Job_description: 'John Brown4',
          unit: '根4',
          Working_hour: 184,
          Working_number: 144,
          Production_hours: '自动计算',
          Auxiliary_time: '自动计算',
          operation: '删除'
        },
        {
          idIndex: 4,
          Working_name: '工步五',
          number: 'BK028855',
          Name_of_work_step: 'John Brown5',
          Job_description: 'John Brown5',
          unit: '根5',
          Working_hour: 185,
          Working_number: 145,
          Production_hours: '自动计算',
          Auxiliary_time: '自动计算',
          operation: '删除'
        },
      ]
    }
  },
  methods: {
    handleAddGongxuObj: function () {
      this.datas.push({ title: '+关联工步', modal: false, tableShow: true, gongbu: [] })
    },
    handleAddGongbuObj: function () {
      window.console.log(1)
    },
    ok (btnIndex) {
      this.$Message.info('Clicked ok');
      window.console.log('您勾选的数组集合为： ', this.checkAllGroup)
      /* this.data1 = [] */
      this.checkAllGroup.forEach((item) => {
        /*  window.console.log(item) */
        for (let index = 0; index < this.checkAllGroup2.length; index++) {
          if (this.checkAllGroup2[index] === item) {
            /* window.console.log('tian la lu index~~', index) */
            /* this.arr.push(index)
            window.console.log('tian la lu arr ~~', this.arr) */
            /* window.console.log('tian la lu datas ~~~~~~', this.datas) */
            /* window.console.log('tian la lu btnIndex ~~~~~~', btnIndex) */
            this.datas[btnIndex].gongbu.push(this.data2[index])
            this.datas[btnIndex].tableShow = true
            /* this.datas[index][0].push(this.data2[index]) */

          }
        }
      })
      /* this.data1.push(data2[index]) */
      /* this.tableShow = true */

    },
    cancel () {
      this.$Message.info('Clicked cancel');
    },
    handleCheckAll () {
      /* window.console.log(this.checkAllGroup) */
      if (this.indeterminate) {
        this.checkAll = false;
      } else {
        this.checkAll = !this.checkAll;
      }
      this.indeterminate = false;

      if (this.checkAll) {
        this.checkAllGroup = ['工步一', '工步二', '工步三', '工步四', '工步五'];
      } else {
        this.checkAllGroup = [];
      }
    },
    checkAllGroupChange (data) {
      /* window.console.log(this.checkAllGroup) */
      if (data.length === 5) {
        this.indeterminate = false;
        this.checkAll = true;
      } else if (data.length > 0) {
        this.indeterminate = true;
        this.checkAll = false;
      } else {
        this.indeterminate = false;
        this.checkAll = false;
      }
    },
    handleBtnClick (index) {

      window.console.log('btnIndex', index);

    },
    show (index) {
      this.$Modal.info({
        title: 'User Info',
        content: `编号：${this.data2[index].number}<br>工步名称：${this.data2[index].Working_name}<br>工步描述：${this.data2[index].Name_of_work_step}<br>单位：${this.data2[index].unit}<br>工步工时：${this.data2[index].Working_hour}<br>工步数量：${this.data2[index].Working_number}<br>生产工时：${this.data2[index].Production_hours}<br>辅助时间：${this.data2[index].Auxiliary_time}`
      })
    },
    remove (index) {
      window.console.log('removeIndex', index);
      this.datas.splice(index, 1);
    }
  },
  mounted () { }
}
</script>

<style >
.about {
  padding: 30px 50px;
}
.i_btn {
  margin-top: 15px;
}
</style>
