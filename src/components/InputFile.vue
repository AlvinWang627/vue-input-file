<template>
  <label class="input-label" for="input-file">上傳檔案</label>
  <input id="input-file" type="file" @change="handleInputFile" multiple />
  <ul>
    <li v-for="item in fileArr" :key="item.id">
      {{ item.file.name }}
      <button @click="removeFile(item.id)">X</button>
    </li>
  </ul>
</template>

<script setup>
import { ref } from 'vue'
let uuid = self.crypto.randomUUID()
const fileArr = ref([])
const handleInputFile = (e) => {
  const file = e.target.files[0]
  // file only accept .pdf
  // if (file.type !== 'application/pdf') {
  //   alert('請上傳 PDF 檔案')
  //   return
  // }
  // file size limit 5MB
  if (file.size > 5 * 1024 * 1024) {
    alert('檔案大小超過 5MB')
    return
  }
  fileArr.value.push({ id: uuid, file })
  console.log(fileArr.value)

  // 抓file 副檔名
  const fileExtension = file.name.split('.').pop()
  console.log(fileExtension)
}
const removeFile = (id) => {
  console.log(fileArr.value)
  console.log(id)``
  fileArr.value = fileArr.value.filter((file) => file.id !== id)
}
</script>

<style lang="scss" scoped>
.input-label {
  border-radius: 6px;
  display: inline-block;
  background-color: #007bff;
  cursor: pointer;
  padding: 8px 12px;
  color: #fff;
}
#input-file {
  display: none;
}
</style>
