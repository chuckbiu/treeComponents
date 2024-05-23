<script setup lang="jsx">
import { ref } from 'vue'
import Node from 'element-plus/es/components/tree/src/model/node'
import { ArrowDown } from '@element-plus/icons-vue'
import itemCom  from './itemCom.vue'

const handleNodeClick = (data) => {
  console.log(data)
}
const append = (data) => {

  let { id } = data
  const newChild = { id: id++, label: '可定义内容', children: [] }
  if (!data.children) {
    data.children = []
  }
  data.children.push(newChild)
  dataSource.value = [...dataSource.value]
}
const remove = (node, data) => {
  const parent = node.parent
  const children = parent.data.children || parent.data
  const index = children.findIndex((d) => d.id === data.id)
  children.splice(index, 1)
  dataSource.value = [...dataSource.value]
}
// 数据来源
const dataSource = ref([
  {
    label: 'a',
    id: 1,
    value: 1,
    children: [
      {
        label: 'a-a',
        id: 2,
        value: 2,
        children: [
          {
            label: 'a-a-a',
            id: 3,
            value: 3
          },
        ],
      },
    ],
  }
])

const defaultProps = {
  children: 'children',
  label: 'label',
}

const renderContent = (
  h,
  {
    node,
    data,
    store,
  }
) => {
  console.log(node,data);
  return (
    <div>
      <itemCom data={data} node={node} append={append} remove={remove}></itemCom>
    </div>
  )
}

</script>

<template>
  <div>
    <p>欢迎使用</p>
    <el-tree style="max-width: 600px" :data="dataSource" :props="defaultProps" @node-click="handleNodeClick"
      node-key="id" default-expand-all :expand-on-click-node="false" :render-content="renderContent">
    </el-tree>
      
  </div>
</template>

<style scoped>
 .example-showcase .el-dropdown-link {
  cursor: pointer;
  color: var(--el-color-primary);
  display: flex;
  align-items: center;
}


</style>
