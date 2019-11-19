<template>
  <div class="about">
    <h1>This is an stepTable page</h1>
    <ul id="example-1">
      <li v-for="(item,index) in data"
          :key='item.id'>
        <i-button @click="modal1 = true"
                  class="i_btn">{{item.text}}</i-button>
        <p>index: {{index}}</p>
        <Modal v-model="modal1"
               title="请勾选您需要显示的工序并确认"
               @on-ok="ok(index,)"
               @on-cancel="cancel">
          <p>Content of dialog</p>
          <div style="border-bottom: 1px solid #e9e9e9;padding-bottom:6px;margin-bottom:6px;">
            <Checkbox :indeterminate="indeterminate"
                      :value="checkAll"
                      @click.prevent.native="handleCheckAll">全选</Checkbox>
          </div>
          <CheckboxGroup v-model="checkAllGroup"
                         @on-change="checkAllGroupChange">
      <li v-for="(gongxuItem,index) in item.gongxu"
          :key='gongxuItem.id'>
        <Checkbox :label="gongxuItem.label">indexs: {{index}}</Checkbox>
      </li>
      </CheckboxGroup>
      </Modal>
      <Table :columns="columns1"
             :data="data1"
             v-if='tableShow'></Table>
      </li>
      <!-- <Table :columns="columns1"
             :data="data1"
             v-if='tableShow'></Table> -->
    </ul>
  </div>
</template>

<script>
export default {
  components: {
  },
  data () {
    return {
      /* border: ['香蕉'], */
      tableShow: false,
      indeterminate: true,
      checkAll: false,
      checkAllGroup: ['工序1', '工序2', '工序3', '工序4', '工序5'],
      modal1: false,
      columns1: [
        {
          title: '工步名称',
          key: 'name'
        },
        {
          title: '工步描述',
          key: 'desc'
        },
        {
          title: '单位',
          key: 'unit'
        },
        {
          title: '工步工时',
          key: 'time'
        },
        {
          title: '工步数量',
          key: 'number'
        },
        {
          title: '成产工时',
          key: 'product_time'
        },
        {
          title: '辅助时间',
          key: 'sub_time'
        },
      ],
      data1: [
        {
          name: '剪线长',
          desc: '以100mm为单位递增，（限电缆线）',
          unit: '根',
          time: 1,
          number: 0,
          product_time: '自动计算',
          sub_time: '自动计算'
        },
        {
          name: '剪线长2',
          desc: '以100mm为单位递增，（限电缆线）2',
          unit: '根2',
          time: 12,
          number: 2,
          product_time: '自动计算2',
          sub_time: '自动计算2'
        },
      ],
      data: [
        {
          id: 'gongbu1',
          text: '公步1',
          gongxu: [
            {
              id: 'gongxu1',
              label: '工序1',
              value: 1,
              gongxu_detail: {
                name: '剪线长',
                desc: '以100mm为单位递增，（限电缆线）',
                unit: '根',
                time: 1,
                number: 0,
                product_time: '自动计算',
                sub_time: '自动计算'
              }
            },
            {
              id: 'gongxu2',
              label: '工序2',
              value: 2,
              gongxu_detail: {
                name: '2剪线长',

                desc: '2以100mm为单位递增，（限电缆线）',
                unit: '2根',
                time: 21,
                number: 20,
                product_time: '2自动计算',
                sub_time: '2自动计算'
              }
            },
            {
              id: 'gongxu3',
              label: '工序3',
              value: 3,
              gongxu_detail: {
                name: '2剪线长',

                desc: '2以100mm为单位递增，（限电缆线）',
                unit: '2根',
                time: 21,
                number: 20,
                product_time: '2自动计算',
                sub_time: '2自动计算'
              }
            },
            {
              id: 'gongxu4',
              label: '工序4',
              value: 4,
              gongxu_detail: {
                name: '4剪线长',

                desc: '4以100mm为单位递增，（限电缆线）',
                unit: '4根',
                time: 4,
                number: 40,
                product_time: '4自动计算',
                sub_time: '4自动计算'
              }
            },
            {
              id: 'gongxu5',
              label: '工序5',
              value: 5,
              gongxu_detail: {
                name: '5剪线长',

                desc: '5以100mm为单位递增，（限电缆线）',
                unit: '5根',
                time: 51,
                number: 50,
                product_time: '5自动计算',
                sub_time: '5自动计算'
              }
            },
          ]
        },
        {
          id: 'gongbu2',
          text: '公步2',
          gongxu: [
            {
              id: 'gongxu1',
              label: '工序1',
              value: 1,
              gongxu_detail: {
                name: '剪线长',

                desc: '以100mm为单位递增，（限电缆线）',
                unit: '根',
                time: 1,
                number: 0,
                product_time: '自动计算',
                sub_time: '自动计算'
              }
            },
            {
              id: 'gongxu2',
              label: '工序2',
              value: 2,
              gongxu_detail: {
                name: '2剪线长',

                desc: '2以100mm为单位递增，（限电缆线）',
                unit: '2根',
                time: 21,
                number: 20,
                product_time: '2自动计算',
                sub_time: '2自动计算'
              }
            },
            {
              id: 'gongxu3',
              label: '工序3',
              value: 3,
              gongxu_detail: {
                name: '3剪线长',

                desc: '3以100mm为单位递增，（限电缆线）',
                unit: '3根',
                time: 31,
                number: 30,
                product_time: '3自动计算',
                sub_time: '3自动计算'
              }
            },
            {
              id: 'gongxu4',
              label: '工序4',
              value: 4,
              gongxu_detail: {
                name: '4剪线长',

                desc: '4以100mm为单位递增，（限电缆线）',
                unit: '4根',
                time: 41,
                number: 40,
                product_time: '42自动计算',
                sub_time: '42自动计算'
              }
            },
            {
              id: 'gongxu5',
              label: '工序5',
              value: 5,
              gongxu_detail: {
                name: '5剪线长',

                desc: '5以100mm为单位递增，（限电缆线）',
                unit: '5根',
                time: 51,
                number: 50,
                product_time: '5自动计算',
                sub_time: '5自动计算'
              }
            },
          ]
        },
      ]
    }
  },
  methods: {
    ok (index) {
      this.$Message.info('Clicked ok')
      window.console.log('您勾选的数组集合为： ', this.checkAllGroup)
      this.tableShow = true
      window.console.log(index);
    },
    cancel () {
      this.$Message.info('Clicked cancel');
    },
    handleCheckAll () {
      if (this.indeterminate) {
        this.checkAll = false;
      } else {
        this.checkAll = !this.checkAll;
      }
      this.indeterminate = false;

      if (this.checkAll) {
        this.checkAllGroup = ['工序1', '工序2', '工序3', '工序4', '工序5'];
      } else {
        this.checkAllGroup = [];
      }
    },
    checkAllGroupChange (data) {
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
    }
  },
  mounted () { }
}
</script>

<style >
.about {
  padding: 5px 15px;
}
.about li {
  list-style: none;
}
.i_btn {
  margin-top: 15px;
}
</style>
