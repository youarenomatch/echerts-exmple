<template>
  <div class="container" ref="container"></div>
</template>

<script setup>
import { onMounted, ref ,toRefs , watch} from "vue";
import * as echarts from "echarts";


// 接收一个 options 属性，用于接收图表配置
const props = defineProps({
  options: {
    type: Object,
    default: {},
    required: true,
  },
});
const { options } = toRefs(props);
// 定义一个ref来保存dom
const container = ref(null);
const chart = ref(null);

onMounted(()=>{
  // 导入 echarts 库进行初始化
   chart.value= echarts.init(container.value);
  // options 变化的时候，图表不会刷新 用watch来监听
  chart.value.setOption(props.options);
})

watch(
  options,
  (newOptions) => {
    chart.value.setOption(newOptions);
  },
  { deep: true }
)

</script>


<style scoped>
.container {
  width: 100%;
  height: 100%;
}
</style>

