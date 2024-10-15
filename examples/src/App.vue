<script setup lang="ts">
import {ref, onMounted} from 'vue'
import {init} from 'pptx-preview'

let domRef = ref()
let pptxPreviewer:any

onMounted(()=>{
    pptxPreviewer = init(domRef.value, {
        width: 1200,
        height: window.innerHeight - 52
    })
    fetch('/pptx-preview/examples/dist/1.pptx').then(response=>{
       return response.arrayBuffer()
    }).then(res =>{
        pptxPreviewer.preview(res)
    })
})

function beforeUpload(file: any){
    let reader = new FileReader();
    reader.onload = (loadEvent) => {
        let arrayBuffer = loadEvent?.target?.result as ArrayBuffer;
        pptxPreviewer.preview(arrayBuffer);
    };
    reader.readAsArrayBuffer(file);
}
</script>

<template>
    <div class="wrapper">
        <el-upload
            action=""
            :show-file-list="false"
            accept=".pptx"
            :before-upload="beforeUpload"
        >
            <el-button type="primary" class="upload-button">选择要预览的pptx文件</el-button>
        </el-upload>
        <div ref="domRef">

        </div>
    </div>
</template>

<style scoped>
.wrapper {
    width: 1200px;
    margin: 0 auto;
    background: #000000;
}

.upload-button {
    margin: 10px 0 10px 80px;
}
</style>
