<template>
    <div>
        <div>【关键词条】</div>
        <div ref='target' class=" h-full"></div>
    </div>
</template>

<script setup>
import {ref,onMounted,watch, render} from 'vue'
import * as echarts from 'echarts'
import 'echarts-wordcloud'
import { data } from 'autoprefixer';

    const props = defineProps({
        data:{
            type:Object,
            required:true
        }
    })

    let mChart = null
    const target = ref(null)

    onMounted(() =>{
        mChart = echarts.init(target.value)
        renderChart()
    })

    const randomRGB = () => {
        const r = Math.floor(Math.random()*255)
        const g = Math.floor(Math.random()*255)
        const b = Math.floor(Math.random()*255)
        return `rgb(${r},${g},${b})`
    }

    watch(() => props.data, ()=>{renderChart()})
    const renderChart = () => {
        const options = {
            series:[
                {
                    type:'wordCloud',
                    sizeRange:[8,46],
                    rotationRange:[0,0],
                    gridSize:0,
                    layoutAnimation:true,
                    textStyle:{
                        color:randomRGB
                    },
                    emphasis:{
                        textStyle:{
                            fontWeight:'bold',
                            color:'#000'
                        }
                    },
                    data:props.data.datas
                }
            ]
        }

        mChart.setOption(options)
    }
</script>

<style lang="scss" scoped></style>