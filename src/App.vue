<template>
  <div class="grid grid-cols-[330px_auto_280px] h-[100vh]">
    <div class="grid grid-cols-[68px_auto] h-full bg-white">
      <div class="border">
        <a class="flex justify-center items-center h-[80px]" href="#">
          <img class="w-[36px]" src="./svg/logo.svg" alt="">
        </a>
        <div class="flex justify-center">
          <i class='bx bx-objects-horizontal-center text-xl'></i>
        </div>
      </div>

      <!-- Sidebar -->
      <div class="border-r" id="sidebar">
        <div class="grid grid-cols-3 gap-2 px-4 py-4">
          <div class="border py-5 flex justify-center rounded-xl bg-gray-100 cursor-pointer" draggable="true" 
          @dragstart="drag($event, 'div', 'Container', 'grid grid-cols-2 gap-4 border border-[2px] border-dashed p-3')">
            <i class='bx bxs-collection text-2xl'></i>
          </div>

          <div class="border py-5 flex justify-center rounded-xl bg-gray-100 cursor-pointer" draggable="true" @dragstart="drag($event, 'div', 'Container', 'border border-[5px] border-dashed p-3 w-[50%]')">
            <i class='bx bx-columns text-2xl' ></i>
          </div>

          <div class="border py-5 flex justify-center rounded-xl bg-gray-100 cursor-pointer" draggable="true" @dragstart="drag($event, 'span', 'Thông tin', 'bg-green-500')">
            <i class='bx bx-font-color text-2xl'></i>
          </div>

          <div class="border py-5 flex justify-center rounded-xl bg-gray-100 cursor-pointer" draggable="true" @dragstart="drag($event, 'p', 'Nội dung')">
            <i class='bx bxs-brush text-2xl'></i>
          </div>
          
          <div class="border py-5 flex justify-center rounded-xl bg-gray-100 cursor-pointer" draggable="true" @dragstart="drag($event, 'h1', 'Tiêu đề lớn')">
            <i class='bx bxs-color-fill text-2xl'></i>
          </div>
        </div>
      </div>
    </div>

    <!-- Content -->
    <div class="p-6 flex flex-col gap-2" id="content" @dragover="allowDrop" @drop="drop">
    </div>

    <!-- Sidebar right -->
    <div class="p-5 border-l">
      <h2>Thông tin chi tiết phần thử kéo vào:</h2>
    </div>
  </div>
</template>

<script setup>
import Container from "./components/Container.vue";
import { ref } from 'vue';

const allowDrop = (event) => { event.preventDefault();}

const drag = (event, tag, content, style) => {
  event.dataTransfer.setData(
    "text", `<${tag} class="${style}" contenteditable="true">${content}</${tag}>`
  );
}

const drop = (event) => {
  event.preventDefault();
  var data = event.dataTransfer.getData("text");
  var tempDiv = document.createElement("div");
  tempDiv.innerHTML = data;
  var element = tempDiv.firstChild;
  element.setAttribute("draggable", "true");
  element.setAttribute("ondragstart", "drag(event)");
  event.target.appendChild(element);
}
</script>
