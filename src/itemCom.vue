<template>
    {{ label }}
      <el-dropdown placement="bottom" trigger="click">
      <span class="el-dropdown-link" style="margin-left: 100px">
        <el-icon >
          <MoreFilled />
        </el-icon>
      </span>
        <template #dropdown>
          <el-dropdown-menu>
            <el-dropdown-item @click="append">增加</el-dropdown-item>
            <el-dropdown-item @click="remove">删除</el-dropdown-item>
            <el-dropdown-item  @click="dialogVisible = true">修改</el-dropdown-item>
          </el-dropdown-menu>
        </template> 
    </el-dropdown>
    <!-- 修改提示框 -->
    <el-dialog
      v-model="dialogVisible"
      title="修改"
      width="500"
      :before-close="handleClose"
    >
    <el-input v-model="input" style="width: 240px" placeholder="请输入修改内容" />
      <template #footer>
        <div class="dialog-footer">
          <el-button @click="dialogVisible = false">取消</el-button>
          <el-button type="primary" @click="confirmClick">
            确认
          </el-button>
        </div>
      </template>
    </el-dialog>
</template>
<script setup>
import { defineProps, onMounted, ref } from 'vue'
const props = defineProps(['data', 'node', 'append', 'remove'])

let label = ref('')
let dialogVisible = ref(false)
const input = ref('')


onMounted(()=>{
  label.value =  props.data.label
})
// 增加
const append = () => {
  if (props.append) {
        props.append(props.data);
      }
}
// 删除
const remove = () => {
  // remove
  if (props.remove) {
        props.remove(props.node ,props.data);
      }
}
const confirmClick = () => {
  dialogVisible.value = false
  label.value = input.value
}
// 提示
const handleClose = () => {
  ElMessageBox.confirm('Are you sure to close this dialog?')
    .then(() => {
      done()
    })
    .catch(() => {
      // catch error
    })
}

</script>