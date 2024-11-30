<script setup lang="ts">
import {ref, onMounted} from 'vue'
import {init} from 'pptx-preview'

let domRef = ref()
let loading = ref(false);
let pptxPreviewer:any

onMounted(()=>{
    loading.value = true;
    pptxPreviewer = init(domRef.value, {
        width: Math.min(window.innerWidth, 960),
        height: window.innerHeight - 52
    })
    fetch('/pptx-preview/examples/dist/test.pptx').then(response=>{
       return response.arrayBuffer()
    }).then(res =>{
        pptxPreviewer.preview(res).finally(()=>{
            loading.value = false;
        })
    })
})

function beforeUpload(file: any){
    loading.value = true;
    let reader = new FileReader();
    reader.onload = (loadEvent) => {
        let arrayBuffer = loadEvent?.target?.result as ArrayBuffer;
        pptxPreviewer.preview(arrayBuffer).finally(()=>{
            loading.value = false;
        });
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
        <div ref="domRef" v-loading="loading" class="pptx-init-dom">

        </div>
    </div>
</template>

<style scoped>
.wrapper {
    width: 100vw;
    background: #000000;
    display: flex;
    flex-direction: column;
    align-items: center;
}
.pptx-init-dom {
    margin: 0 auto;
}
.upload-button {
    margin: 10px 0 10px 80px;
}
</style>
