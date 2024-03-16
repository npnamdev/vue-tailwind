<template>
  <div>
    <input type="file" ref="fileInput" @change="handleFileChange">
    <button @click="uploadFile">Upload</button>
    <ul>
      <li v-for="item in apiData" :key="item.id">
        <pre>{{ item }}</pre>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

const fileInput = ref(null);
const apiData = ref([]);

const fetchDataFromApi = async () => {
  try {
    const response = await axios.get('http://localhost:6789/api/v1/auth/upload/cloudinary');
    apiData.value = response.data.data.resources;
  } catch (error) {
    console.error('Error while fetching data from API:', error);
  }
};

const uploadFile = async () => {
  try {
    const file = fileInput.value.files[0];
    const formData = new FormData();
    formData.append('file', file);

    const response = await axios.post('http://localhost:6789/api/v1/auth/upload/cloudinary', formData);

    console.log(response);

    fetchDataFromApi();
  } catch (error) {
    console.error('Error while uploading file:', error);
  }
};

const handleFileChange = (event) => {
  // Xử lý sự kiện thay đổi của input file nếu cần
};

onMounted(() => {
  fetchDataFromApi();
});
</script>
