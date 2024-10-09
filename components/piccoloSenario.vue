<template>
  <div class="bg-red-00">
   <main class="bg-[rgb(254,243,199)] pt-[40px]  1xl:h-[400px] 2xl:h-[560px] 3xl:h-[730px] rounded-lg  relative top-[-20px]" > 
       <div class="flex mb-2 ml-2 pt-2 3xl:pb-4 absolute   top-[-3px] 00" >
   <v-btn @click="closeScenario" icon= 'mdi-close'  size="small" color="primary"  class="cursor-pointer "></v-btn>
   <div  class=" ml-4 mr-2 mt-2 text-[20px] text-[#992121] font-bold">Scenario Creator</div>
 </div>
       <!-- scenario  -->
       <aside class="flex justify-evenly mt-5  py-4 mx-4 rounded-lg bg-white  1xl:h-[140px] 2xl:h-[180px]  3xl:h-[230px] ">
     <div class="flex justify-center items-center  cursor-pointer bg-red-00 1xl:h-[120px] 2xl:h-[140px]  3xl:h-[180px]" :class="{ 'py-2 px-2 border-4 border-red-500': selectedImage === 'High-performance for BMS' }" @click="selectImage('High-performance for BMS')">
       <div>
 <div class="flex justify-center">
   <img src="/public/img/car.png" alt="parking image" class="1xl:w-[120px] 1xl:h-[80px]  2xl:w-[150px] rounded-lg  2xl:h-[100px]  3xl:w-[200px] 3xl:h-[130px] bg-red-400 "> 
 </div>       
  <div class="flex justify-center pt-1">
           <p class="text-[13px] font-bold text-[#992121] ">High-performance for BMS</p>
         </div>
       </div>
     </div>
 
     <div class="flex justify-center items-center  cursor-pointer  bg-red-00 1xl:h-[120px] 2xl:h-[140px]  3xl:h-[180px]" :class="{ 'py-2 px-2 border-4 border-red-500': selectedImage === 'Eco mode ON for BMS' }" @click="selectImage('Eco mode ON for BMS')">
     <div>
       <div class="flex justify-center">
         <img src="/public/img/car1.png" alt="parking image" class="1xl:w-[120px] 1xl:h-[80px]  2xl:w-[150px] rounded-lg  2xl:h-[100px] 3xl:w-[200px] 3xl:h-[130px]"> 
       </div> 
       <div class="flex justify-center pt-1">
         <p class="text-[13px] font-bold text-[#992121] ">Eco mode ON for BMS</p>
       </div>
     </div>
     </div>
 
     <div class="flex justify-center items-center cursor-pointer  bg-red-00 1xl:h-[120px] 2xl:h-[140px]  3xl:h-[180px]" :class="{ 'py-2 px-2 border-4 border-red-500': selectedImage === 'Charging for BMS' }" @click="selectImage('Charging for BMS')">
     <div  @click="getchargingJsondata">
       <div class="flex justify-center" @click="toggleLayout()">
         <img src="/public/img/charging.png" alt="charging image" class="1xl:w-[120px] 1xl:h-[80px]  2xl:w-[150px] rounded-lg  2xl:h-[100px]  3xl:w-[200px] 3xl:h-[130px]"> 
       </div> 
       <div class="flex justify-center pt-1">
         <p class="text-[13px] font-bold text-[#992121] ">Charging for BMS</p>
       </div>
     </div>
     </div>
 
   
   </aside>
 
 <!-- section by default bg-transparent when user click charging for bms -->
   <section :class="sectionClasses">
        <!-- host Name drag value section -->
       <div class="bg-white mx-4 rounded-lg">
         <aside class="mt-5 py-4 mx-4 rounded-lg bg-whit 3xl:h-[130px] 3xl:flex justify-center items-center">
           <div class="flex justify-center items-center " >
               <div v-for="(containerName, index) in dragElement" :key="index"  >
                   <p class="flex justify-center items-center text-center bg-blue-300 border-black/20 border-solid border-2  1xl:my-1 1xl:px-3 1xl:py-1  1xl:mx-2  2xl:my-2 2xl:px-5 2xl:py-2  2xl:mx-3" >
                       {{ containerName }}
                   </p>
               </div>
           </div>
       </aside>
 

            <aside class="mt-5 py-4 mx-4 rounded-lg bg-red-00   bg-whit overflow-auto  1xl:h-[120px] 2xl:h-[140px] 3xl:h-[200px]">
                <div class="flex justify-center items-end  2xl:mt-2 3xl:mt-[0px] box-container" ref="boxContainer" >
                   <header v-for="(host, index) in hostnames" :key="index"  class="mx-2 bg-green-00  ">
                     
                        <section class="overflow-auto  " >
                         <div v-for="chargingData in filteredChargingData" :key="chargingData"  class="bg-gray-500">
                         <div class="mb-4 ele" v-if="chargingData.config['Hostname'] == host.system"  >
                           <div v-for="name in chargingData.names" :key="name" >
                             <div  v-if=" selectedImage === 'Charging for BMS'"  class="ele px-[5px] py-[5px] border   border-blue-500 bg-blue-300  text-center">
                               {{ name }}
                             </div>
                           </div>
                         </div>
                       </div>
                   
                       <div class="bg-yellow-00  " >
                         <div class="1xl:px-3  1xl:py-1 2xl:px-6  2xl:py-2 border-2 border-dashed  border-blue-500 text-center capitalize  text-black"
                         >
                           {{ host.system }}
                          </div>
                       </div>
                        </section>
                   </header> 
               </div>
           </aside>
       </div>
           <!-- <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 37 53" width="37" height="53" preserveAspectRatio="xMidYMid meet" style="width: 100%; height: 100%; transform: translate3d(0px, 0px, 0px); content-visibility: visible;"><defs><clipPath id="__lottie_element_73"><rect width="37" height="53" x="0" y="0"></rect></clipPath></defs><g clip-path="url(#__lottie_element_73)"><g transform="matrix(1,0,0,1,18.5,26.5)" opacity="1" style="display: block;"><g opacity="1" transform="matrix(1,0,0,1,0,0)"><path stroke-linecap="round" stroke-linejoin="round" fill-opacity="0" stroke="rgb(255,105,59)" stroke-opacity="1" stroke-width="3" d=" M16.625,-24.5 C16.625,-24.5 22.19499969482422,3.2309999465942383 -13.267000198364258,19.836999893188477"></path></g></g><g transform="matrix(1,0,0,1,18.5,26.5)" opacity="1" style="display: block;"><g opacity="1" transform="matrix(1,0,0,1,0,0)"><path stroke-linecap="round" stroke-linejoin="round" fill-opacity="0" stroke="rgb(255,105,59)" stroke-opacity="1" stroke-width="3" d="M0 0"></path></g></g></g></svg> -->
 
       <footer class="3xl:mt-1">
           <div class="flex justify-end pt-2  ">
               <button class="px-2 py-2 mx-[10px] rounded-md w-[100px] text-sm  bg-white text-[black] border-2 border-solid   border-black/45 hover:border-red-400  transition-all duration-300 shadow-md hover:shadow-lg transform hover:-translate-y-0.5 shadow-gray-500/30"
                   @click="createTemplate" :disabled="!canCreate"  :class="{ 'opacity-50 cursor-not-allowed': !canCreate}">
                   Create
               </button>
               <button
                class="px-2 py-2 mx-[10px] rounded-md w-[100px] text-sm   bg-white text-[black] border-2 border-solid   border-black/45 hover:border-red-400  transition-all duration-300 shadow-md hover:shadow-lg transform hover:-translate-y-0.5  shadow-gray-500/30"
                 @click="cancelTemplate"  :disabled="!canCreate"  :class="{ 'opacity-50 cursor-not-allowed': !canCreate}">
                 Cancel
               </button>
           </div>
       </footer>
   </section>
     
   </main>
 
  </div>
   
 </template>
 
 
 <script setup>
 import { ref, computed } from "vue";
 
 
 import chargingData  from   "../../data/container-charging.json"
 
 const chargingJson=ref(chargingData)
 
 
 
 const emit = defineEmits(['close']);
 
 const closeScenario = () => {
   emit('close');
 };
 
 const filteredChargingData = chargingJson.value.containers.filter((element) => {
   return element.annotation["piccolo.package.name"] == "bms";
 });
 const getchargingJsondata=()=>{
 console.log('getdata-from-charging',filteredChargingData)
 }
 const dragElement = ref([ "rdv",  "mavd", "frism",  "blis"]);


 
 
 
 console.log(dragElement.value);
 
 const hostnames = ref([
 { system: "HPC", containers: [] },
 { system: "ZONE", containers: [] },
 ]);
 
 
 const draggedItem = ref(null);
 // const draggedItem = ref(['mavd','rdv']);
 
 const selectedImage = ref(null);
 
 
 const selectImage = (imageName) => {
 selectedImage.value = imageName;
 };
 
 
 const onDragStart = (item) => {
 draggedItem.value = item;
 };
 
 
 
 const onDropActions = (host) => {
 console.log(" draggedItem.value", draggedItem.value);
 console.log("host", host);
 hostnames.value.forEach((element) => {
   if (element.system == host.system) {
     element.containers.push(draggedItem.value);
   }
 });
 draggedItem.value = null;
 };
 
 
 const createTemplate = () => {
   let localStorageCards = localStorage.getItem("cards");
   localStorageCards = localStorageCards ? JSON.parse(localStorageCards) : [];
 
   // Get the length of the existing array
   const localStorageLength = localStorageCards.length;
  
   console.log("Existing cards length:", localStorageLength);
   localStorageCards.push({
     id: localStorageLength + 1, 
     name: selectedImage.value, 
     conditionsvalue:"BulkCharging",
     conditionsexpress: 'lt',
     chargingStatus:'on',
     targetsname:"charging",
     operandsname:"charging_status",
     components: [
     { system: "HPC", containers: [ "blis","mavd"] },
     { system: "ZONE", containers: [ "frism","rdv"] },
     ] 
   });
 
   // Save the updated array back to localStorage
   localStorage.setItem("cards", JSON.stringify(localStorageCards));
 
   cancelTemplate();
   closeScenario()
 };
 
 
 
 const handleClose = () => {
   emitCloseEvent();
 };
 
 const emitCloseEvent = () => {
   emit("close");
 };
 
 const cancelTemplate = () => {
   selectedImage.value = null; 
   draggedItem.value = null; 
   hostnames.value.forEach(host => {
       host.containers = []; 
   });
 };
 
 // Computed property to determine if the Create button can be enabled
 // const canCreate = computed(() => selectedImage.value);
 const canCreate = computed(() => selectedImage.value === 'Charging for BMS');
 
 const sectionClasses = computed(() => {
   return selectedImage.value === 'Charging for BMS' ? '' : 'pt-1 mx-4  bg-gray-600 opacity-40 cursor-not-allowed ';
   // Replace 'bg-originalColor' with your desired background class, e.g., 'bg-white'
 });
 
 </script>
 
 <style scoped>
 

 .ele {
   transition: opacity 3s cubic-bezier(0.4, 0, 0.2, 1);
   opacity: 10;
   animation: fadeIn 3s forwards; 
 }
 @keyframes fadeIn {
   0% {
     opacity: 0;
   }
   50% {
     opacity: 5;
   }
  
   100% {
     opacity: 1;
   }
 }
 .piccolo-scenario {
   padding: 20px;
   border: 1px solid #ccc;
   border-radius: 5px;
 }
 
 .close-button {
   margin-top: 10px;
   padding: 5px 10px;
   background-color: #f44336;
   color: white;
   border: none;
   border-radius: 3px;
   cursor: pointer;
 }
 
 .toggle-button-container {
   display: flex;
   align-items: center;
   padding: 10px;
 }
 
 .scenario-title {
   margin-left: 10px;
   font-size: 20px;
   color: #992121;
   font-weight: bold;
 }
 </style>
 
