<template>
 <div>
<div class="flex mb-2 ml-1 pt-2 3xl:pb-4" >
  <v-btn @click="closeScenario" icon= 'mdi-close'  size="small" color="primary"  class="cursor-pointer "></v-btn>
  <div  class=" ml-4 mr-2 mt-2 text-[20px] text-[#992121] font-bold">Scenario Creator</div>

</div>
  <main class="bg-gray-200  1xl:h-[400px] 2xl:h-[500px]  rounded-lg" style="background-color:#EFF2EF;"> 
      <!-- scenario  -->
      <aside class="flex justify-evenly py-4 mx-4 rounded-lg bg-white  1xl:h-[140px] 2xl:h-[180px]  3xl:h-[230px] ">
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
      <div class="flex justify-center">
        <img src="/public/img/charging.png" alt="charging image" class="1xl:w-[120px] 1xl:h-[80px]  2xl:w-[150px] rounded-lg  2xl:h-[100px]  3xl:w-[200px] 3xl:h-[130px]"> 
      </div> 
      <div class="flex justify-center pt-1">
        <p class="text-[13px] font-bold text-[#992121] ">Charging for BMS</p>
      </div>
    </div>
    </div>

  
  </aside>

      <!-- host Name drag value section -->
      <aside class="mt-5 py-4 mx-4 rounded-lg bg-white 3xl:h-[130px] 3xl:flex justify-center items-center">
          <div class="flex justify-center items-center cursor-grab">
              <div v-for="(containerName, index) in dragElement" :key="index" draggable="true" @dragstart="onDragStart(containerName)">
                   <p class="flex justify-center items-center text-center bg-gray-300 border-black/20 border-solid border-2  1xl:my-1 1xl:px-3 1xl:py-1  1xl:mx-2   2xl:my-2 2xl:px-5 2xl:py-2  2xl:mx-3"
                    v-if="containerName == 'camera' || containerName == 'location' || containerName == 'DSM'">
                    {{ containerName }}
                  </p>
                  <p v-else class="flex justify-center items-center text-center bg-blue-300 border-black/20 border-solid border-2  1xl:my-1 1xl:px-3 1xl:py-1  1xl:mx-2  2xl:my-2 2xl:px-5 2xl:py-2  2xl:mx-3" >
                      {{ containerName }}
                  </p>
              </div>
          </div>
      </aside>


      
          <aside class="mt-5 py-4 mx-4 rounded-lg bg-red-00   bg-white overflow-auto  1xl:h-[120px] 2xl:h-[140px] 3xl:h-[200px]">
               <div class="flex justify-center items-center 2xl:mt-2 3xl:mt-[40px]" >
                  <header v-for="(host, index) in hostnames" :key="index"  class="mx-2 bg-green-00  bg-red-00  1xl:h-[120px]  2xl:h-[160px] 3xl:h-[200px] flex justify-end items-end  overflow-auto">
                    
                       <section class="overflow-auto  " >
                        <div v-for="chargingData in filteredChargingData" :key="chargingData"  class="bg-gray-500">
                        <div class="mb-4" v-if="chargingData.config['Hostname'] == host.system"  >
                          <div v-for="name in chargingData.names" :key="name" >
                            <div  v-if=" selectedImage === 'Charging for BMS'"  class="px-[5px] py-[5px] border  border-blue-500 bg-blue-300  text-center">
                              {{ name }}
                            </div>
                          </div>
                        </div>
                      </div>
                  
                      <div class="bg-yellow-00  " >
                        <div class="1xl:px-3  1xl:py-1 2xl:px-6  2xl:py-2 border-2 border-dashed  border-blue-500 text-center capitalize  text-black"
                         :class="{ 'py-2 px-2 border-3 border-blue-500 bg-gray-300 ': host.system  === 'zc front' ||  host.system  === 'zc rear'  }">
                          {{ host.system }}
                         </div>
                      </div>
                       </section>


                       <!-- <div  class="flex gap-2 items-end bg-red-00  3xl:w-[460px] ">
                        <div class="bg-red-00 3xl:ml-[20px]   cursor-pointer">
                           <div class="h-[270px]      2xl:overflow-auto  3xl:overscroll-none  bg-gray-00    bg-yellow-00">
                            <div class="flex gap- items-end justify-center px-[0px] h-[250px]  bg-gray-00  mb-5">
                              
                                 <div v-for="chargingData in filteredChargingData" :key="chargingData" >
                                   <div class="mb-4" v-if="chargingData.config['Hostname'] == host.system" >
                                    <div v-for="name in ChargingData.names" :key="name" class="px-[5px] py-[5px] 3xl:px-[10px]  3xl:py-[10px] mx-5 border-dashed border-black border-1 ele  bg-blue-300 text-center  transition delay-400 duration-030 ease-in-out">
                                    
                                      <div    v-if=" selectedImage === 'Charging for BMS'"
                                      >  {{ name }}</div>
                                    </div>
                                  </div>
                                 </div>
                                 
                                 <div class="1xl:px-[10px] capitalize 1xl:py-[5px] 2xl:px-[10px]  2xl:py-[7px] 3xl:px-[10px]  3xl:py-[10px]  3xl:w-[80px] mx-5  border-dashed border-blue-400  bg-gray-300 border-2 text-center" v-if="host.system  === 'zc front'||host.system  === 'zc front'">
                                  {{ host.system }}
                                  </div>
                                  <div class="1xl:px-[10px] capitalize   1xl:py-[5px] 2xl:px-[10px]  2xl:py-[7px]  3xl:px-[10px]  3xl:py-[10px] 3xl:w-[80px] mx-5  border-dashed border-blue-400 border-2 text-center" v-else>
                                    {{ host.system }}
                                     </div>
                                    </div>
                                  </div>
                                 </div>
                            
                              </div> -->
                  </header>
              </div>
          </aside>


      <footer class="3xl:mt-1">
          <div class="flex justify-end pt-2  ">
              <button class="px-2 py-2 mx-[10px] rounded-md w-[100px] text-sm text-white bg-gradient-to-r from-green-400 to-green-600 hover:from-green-500 hover:to-green-700 transition-all duration-300 shadow-md hover:shadow-lg transform hover:-translate-y-0.5 shadow-green-500/50"
                  @click="createTemplate" :disabled="!canCreate"  :class="{ 'opacity-50 cursor-not-allowed': !canCreate}">
                  Create
              </button>
              <button
               class="px-2 py-2 mx-[10px] rounded-md w-[100px] text-sm text-white bg-gradient-to-r from-red-400 to-red-600 hover:from-red-500 hover:to-red-700 transition-all duration-300 shadow-md hover:shadow-lg transform hover:-translate-y-0.5 shadow-red-500/50"
                @click="cancelTemplate"  :disabled="!canCreate"  :class="{ 'opacity-50 cursor-not-allowed': !canCreate}">
                Cancel
              </button>
          </div>
      </footer>
  </main>

 </div>
  
</template>


<script setup>
import { ref, computed } from "vue";
import chargingData  from   "../../data/container-charging.json"

const chargingJson=ref(chargingData)


const filteredChargingData = chargingJson.value.containers.filter((element) => {
  return element.annotation["piccolo.package.name"] == "bms";
});


const getchargingJsondata=()=>{
console.log('getdata-from-charging',filteredChargingData)
}



const dragElement = ref([ "rdv",  "mavd", "frism",  "blis"]);
console.log(dragElement.value);



const emit = defineEmits(['close']);

const closeScenario = () => {
  emit('close');
};

const hostnames = ref([
{ system: "Soc0", containers: [] },
{ system: "Soc1", containers: [] },
{ system: "Zc front", containers: [] },
{ system: "Zc rear", containers: [] },
]);


// const draggedItem = ref(null);
const draggedItem = ref(['mavd','rdv']);

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





// const createTemplate = () => {
// let localStorageCards = localStorage.getItem("cards");
// if (localStorageCards) {
//   localStorageCards = JSON.parse(localStorageCards);
//   localStorageCards.push({
//     name: selectedImage.value,
//     components: hostnames.value,
//   });
//   localStorage.setItem("cards", JSON.stringify(localStorageCards));
//   cancelTemplate()
// }
// };




const createTemplate = () => {
  let localStorageCards = localStorage.getItem("cards");

  // Parse the existing cards if available, otherwise initialize an empty array
  localStorageCards = localStorageCards ? JSON.parse(localStorageCards) : [];

  // Get the length of the existing array
  const localStorageLength = localStorageCards.length;
 
  console.log("Existing cards length:", localStorageLength);
  localStorageCards.push({
    id: localStorageLength + 1, 
    name: selectedImage.value, 
    components: [{ system: "Soc0", containers: [] },
{ system: "Soc1", containers: ['mavd','frism'] },
{ system: "Zc front", containers: ['blis','rdv'] },
{ system: "Zc rear", containers: [] },] 
  });

  // Save the updated array back to localStorage
  localStorage.setItem("cards", JSON.stringify(localStorageCards));

  cancelTemplate();
};

const handleClose = () => {
  // Optional: Check if there are unsaved changes and prompt the user

  // For simplicity, we'll assume changes are saved via 'createTemplate'

  // Emit the 'close' event to the parent component
  emitCloseEvent();
};

// Function to emit the 'close' event
const emitCloseEvent = () => {
  emit("close");
};

const cancelTemplate = () => {
  selectedImage.value = null; // Clear selected image
  draggedItem.value = null; // Clear dragged item
  hostnames.value.forEach(host => {
      host.containers = []; // Clear containers for all hosts
  });
};

// Computed property to determine if the Create button can be enabled
const canCreate = computed(() => selectedImage.value);

</script>

<style scoped>


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
