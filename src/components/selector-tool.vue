<script setup lang="ts">
import { onMounted, ref,defineEmits } from 'vue'
const emit = defineEmits(['select'])
const rectangle = ref()
const x = ref(0)
const y = ref(0)
const left = ref(0)
const top = ref(0)
const width = ref(0)
const height = ref(0)
const drag = ref(false)
function mousemove(ev:MouseEvent)
{
    const {clientX, clientY} = ev
    if(clientX < x.value)
    {
        left.value = clientX
        width.value = x.value - clientX
    }
    else
    {
        width.value = clientX - x.value
    }
    if(clientY < y.value)
    {
        top.value = clientY
        height.value = y.value - clientY
    }
    else
    {
        height.value = clientY - y.value
    }
}
document.onmousedown = (ev:MouseEvent)=>{
    ev.preventDefault()
    const {clientX, clientY} = ev
    x.value = clientX
    y.value = clientY
    left.value = clientX
    top.value = clientY
    width.value = 0
    height.value = 0
    document.onmousemove = mousemove
    drag.value = true
}
document.onmouseup = (ev:MouseEvent)=>{
    const {clientX, clientY} = ev
    let left, top, right, bottom

    if(clientX > x.value)
    {
        left = x.value
        right = clientX
    }
    else
    {
        left = clientX
        right = x.value
    }
    if(clientY > y.value)
    {
        top = y.value
        bottom = clientY
    }
    else
    {
        top = clientY
        bottom = y.value
    }
    
    emit('select',{
        left: left,
        top: top,
        right: right,
        bottom: bottom
    })
    document.onmousemove = null
    drag.value = false
}

</script>

<template>
<div ref="rectangle" class="rectangle" :style="`left:${left}px;top:${top}px;width:${width}px;height:${height}px;display:${drag?'visible':'none  '}`">
</div>
</template>

<style scoped>
.rectangle{
    position: fixed;
    z-index: 9999;
    border : 2px dashed rgb(4, 70, 253);
    background-color: rgba(4, 70, 253, 0.1);
}
</style>
