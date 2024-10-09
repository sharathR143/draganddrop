

 
<template>
  <div class="w-[900px] xl:w-[550px] 1xl:w-[550px] 2xl:w-[600px] 3xl:w-[700px] h-[400px] xl:h-[390px] 1xl:h-[500px] 2xl:h-[560px] 3xl:h-[730px] rounded-lg"  style="background-color:#EFF2EF;">
    <header class="flex justify-between mt-0 ml-5">
        <div>
          <p class="font-bold px-5 py-5 xl:text-[17px] 1xl:text-[17px] 3xl:text-[19px] uppercase text-[#992121]">Service Location</p>
        </div>
      </header>

    <aside  class="mr-5 xl:h-[250px] 1xl:h-[380px] 2xl:h-[400px] 3xl:h-[550px] 2xl:w-[520px] 3xl:w-[620px]  mx-10 rounded-lg  xl:mt-3 1xl:mt-3 2xl:mt-5" style="background-color:#FFFFFF">
      <div class="bg-red-00 h-[30px] flex">
        <p class="text-[18px] ml-4  font-bold mt-2">BMS Information</p>
      </div>

      <div class="flex justify-evenly mr-5 xl:h-[250px] 1xl:h-[290px] 2xl:h-[380px]   mx-10 rounded-lg  xl:mt-3 1xl:mt-3 2xl:mt-5">
        <div class="flex gap-2 items-end  border-red-300 h-[300px]  3xl:h-[400px] mt-[15px]">
         
            <div v-if="selectedCardName== 'Eco mode ON for BMS'"  class="flex gap-2 items-end bg-red-00  3xl:w-[560px] ">

            <div class="bg-yellow-00  3xl:ml-[-20px]   cursor-pointer 3xl:w-[600px]">
              <div class="h-[270px]      2xl:overflow-auto  3xl:overscroll-none  bg-gray-00    bg-yellow-00">
                 <div class="flex gap- items-end justify-center px-[0px] h-[250px]  bg-gray-00  mb-5">
                  <div v-if="hasHPCContainers" class="absolute top-[340px] left-[250px] 3xl:top-[420px] 3xl:left-[270px]   transform -translate-x-1/2 -mt-24 z-10">
                    <!-- Cloud SVG -->
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 240 180" class="w-24 h-24">
                      <defs>
                        <!-- Cloud gradient -->
                        <linearGradient id="cloudGradient" x1="0%" y1="0%" x2="0%" y2="100%">
                          <stop offset="0%" style="stop-color:#FFFFFF" />
                          <stop offset="100%" style="stop-color:#FFFFFF" />
                        </linearGradient>
                        <!-- Zzz gradient -->
                        <linearGradient id="zzzGradient" x1="0%" y1="110%" x2="100%" y2="100%" class="mr-5">
                          <stop offset="0%" style="stop-color:#6A8CAF" />
                          <stop offset="100%" style="stop-color:#4A6A8C" />
                        </linearGradient>
                      </defs>
                      <!-- Main cloud body -->
                      <path
                        d="M45 100 Q25 100 25 80 Q25 65 40 65 Q40 40 70 40 Q90 25 110 40 Q125 30 140 40 Q160 30 175 45 Q200 45 210 65 Q230 70 230 90 Q230 110 210 115 Q215 130 200 140 Q180 150 160 140 Q150 150 130 145 Q110 155 90 145 Q70 155 55 140 Q40 140 35 125 Q20 115 30 100"
                        fill="url(#cloudGradient)"
                        stroke="#B0B0B0"
                        stroke-width="3"
                        stroke-linejoin="round"
                      />
                      <!-- Zzz symbols -->
                      <g transform="translate(160, 30) rotate(-10)">
                        <path
                          d="M0 0 L20 0 L0 20 L25 20"
                          stroke="url(#zzzGradient)"
                          stroke-width="5"
                          fill="none"
                          stroke-linejoin="round"
                          stroke-linecap="round"
                        >
                          <animate
                            attributeName="opacity"
                            values="0;1;0"
                            dur="4s"
                            repeatCount="indefinite"
                          />
                        </path>
                        <path
                          d="M10 25 L25 25 L10 40 L30 40"
                          stroke="url(#zzzGradient)"
                          stroke-width="4"
                          fill="none"
                          stroke-linejoin="round"
                          stroke-linecap="round"
                          opacity="0.8"
                        >
                          <animate
                            attributeName="opacity"
                            values="0;0.8;0"
                            dur="4s"
                            repeatCount="indefinite"
                            begin="0.5s"
                          />
                        </path>
                        <path
                          d="M20 45 L30 45 L20 55 L35 55"
                          stroke="url(#zzzGradient)"
                          stroke-width="3"
                          fill="none"
                          stroke-linejoin="round"
                          stroke-linecap="round"
                          opacity="0.6"
                        >
                          <animate
                            attributeName="opacity"
                            values="0;0.6;0"
                            dur="4s"
                            repeatCount="indefinite"
                            begin="1s"
                          />
                        </path>
                      </g>
                    </svg>
                  </div>
                  <div v-for="host in hostnames" :key="host">

                     <section :class="['p-2', host === 'HPC' ? 'bg-gray-200 rounded-lg  opacity-50 ' : '']" >
                      <div v-for="ParkingData in filteredParkingData" :key="ParkingData">
                      <div class="mb-4" v-if="ParkingData.config['Hostname'] == host">
                        <div v-for="name in ParkingData.names" :key="name" class="px-[5px] py-[5px] 3xl:px-[10px]  3xl:py-[10px] 3xl:w-[100px]  mx-5 border-dashed border-black border-1 ele  bg-blue-300 text-center  transition delay-400 duration-030 ease-in-out">
                          {{ name }}
                        </div>
                      </div>
                    </div>
                    
                   
                       <div class="1xl:px-[10px] capitalize  1xl:py-[5px] 2xl:px-[15px]  2xl:py-[5px]  3xl:px-[10px]  3xl:py-[10px] 3xl:w-[100px] mx-5  border-dashed border-blue-400 border-2 text-center" >
                        {{ host }}
                      </div>
                     </section>
                    </div>
                  </div> 

           </div>
          </div>
          </div>

          <div v-else-if="selectedCardName== 'Charging for BMS'"  class="flex gap-2 items-end bg-red-00  3xl:w-[560px] ">
            <div class="bg-red-00 3xl:ml-[-20px]   cursor-pointer 3xl:w-[600px]">
              <div class="h-[270px]      2xl:overflow-auto  3xl:overscroll-none  bg-gray-00    bg-yellow-00">
                 <div class="flex gap- items-end justify-center px-[0px] h-[250px]  bg-gray-00  mb-5">
                  <div v-for="host in hostnames" :key="host">
                     <div v-for="ChargingData in filteredChargingData" :key="ChargingData">
                      <div class="mb-4" v-if="ChargingData.config['Hostname'] == host">
                        <div v-for="name in ChargingData.names" :key="name" class="px-[5px] py-[5px] 3xl:px-[10px]  3xl:py-[10px]  mx-5 border-dashed border-black border-1 ele  bg-blue-300 text-center  transition delay-400 duration-030 ease-in-out">
                          {{ name }}
                        </div>
                      </div>
                    </div>
                    
                   
                       <div class="1xl:px-[10px] capitalize   1xl:py-[5px]  2xl:px-[15px]  2xl:py-[5px]   3xl:px-[10px]  3xl:py-[10px]  3xl:w-[100px] mx-5  border-dashed border-blue-400 border-2 text-center" >
                        {{ host }}
                      </div>
                    </div>
                  </div> 

           </div>
          </div>
          </div>

          <div v-else  class="flex gap-2 items-end bg-red-00  3xl:w-[560px] ">
            <div class="bg-red-00 3xl:ml-[-20px]   cursor-pointer 3xl:w-[600px]">
              <div class="h-[270px]      2xl:overflow-auto  3xl:overscroll-none  bg-gray-00    bg-yellow-00">
                 <div class="flex gap- items-end justify-center h-[250px]  bg-gray-00  mb-5">
                  <div v-for="host in hostnames" :key="host">
                     <div v-for="DrivingData in filteredDrivingData" :key="DrivingData">
                      <div class="mb-4" v-if="DrivingData.config['Hostname'] == host">
                        <div v-for="name in DrivingData.names" :key="name" class="px-[5px] py-[5px] 2xl:px-[15px]  2xl:py-[10px] 2xl:mx-10 3xl:px-[10px]  3xl:py-[10px] mx-5 border-dashed border-black border-1 ele  bg-blue-300 text-center  transition delay-400 duration-030 ease-in-out">
                          {{ name }}
                        </div>
                      </div>
                    </div>
                       <div class="1xl:px-[10px] capitalize   1xl:py-[5px] 2xl:px-[15px]  2xl:py-[5px]  3xl:px-[10px]  3xl:py-[10px] 3xl:w-[100px] mx-5  border-dashed border-blue-400 border-2 text-center" >
                        {{ host }}
                      </div>
                    </div>
                  </div> 

           </div>
          </div>
          </div>

         
      </div>
      </div>
    </aside>
  </div>
</template> 


 <script setup>
import driving from "../../data/container-Driving.json";
import parking from "../../data/container-parking.json";
import chargingData  from   "../../data/container-charging.json"

const json = ref(driving);
const parkingJson = ref(parking);
const chargingJson=ref(chargingData)




const props = defineProps(["selectedCardName"]);
const hostnames = ["HPC","ZONE"];


const filteredDrivingData = json.value.containers.filter((element) => {
  return element.annotation["piccolo.package.name"] == "bms";
});
const filteredParkingData = parkingJson.value.containers.filter((element) => {
  return element.annotation["piccolo.package.name"] == "bms";
});
const filteredChargingData = chargingJson.value.containers.filter((element) => {
  return element.annotation["piccolo.package.name"] == "bms";
});

// Computed property to check if there are any HPC containers
const hasHPCContainers = computed(() => {
  // Check in all data sets
  return (
    filteredDrivingData.some((data) => data.config['Hostname'] === 'HPC') ||
    filteredParkingData.some((data) => data.config['Hostname'] === 'HPC') ||
    filteredChargingData.some((data) => data.config['Hostname'] === 'HPC')
  );
});
</script>


<!-- <style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s cubic-bezier(0.4, 0, 0.2, 1);
}
.list-enter-active, .list-leave-active {
  transition: all 0.5s ease;
}
.list-enter-from, .list-leave-to {
  opacity: 0;
  transform: translateY(10px);
}
.list-enter-to, .list-leave-from {
  opacity: 1;
  transform: translateY(0);
}
/* Fade transition effect */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
.fade-enter-to,
.fade-leave-from {
  opacity: 1;
}
.ele {
  transition: opacity 3s cubic-bezier(0.4, 0, 0.2, 1);
  opacity: 10;
  animation: fadeIn 3s forwards; 
}
@keyframes fadeIn {
  0% {
    opacity: 0;
  }
 
  100% {
    opacity: 1;
  }
}
</style>
 -->
 <style scoped>
 .fade-enter-active,
 .fade-leave-active {
   transition: opacity 0.5s cubic-bezier(0.4, 0, 0.2, 1);
 }
 .list-enter-active,
 .list-leave-active {
   transition: all 0.5s ease;
 }
 .list-enter-from,
 .list-leave-to {
   opacity: 0;
   transform: translateY(10px);
 }
 .list-enter-to,
 .list-leave-from {
   opacity: 1;
   transform: translateY(0);
 }
 
 /* Fade transition effect */
 .fade-enter-active,
 .fade-leave-active {
   transition: opacity 0.5s ease;
 }
 .fade-enter-from,
 .fade-leave-to {
   opacity: 0;
 }
 .fade-enter-to,
 .fade-leave-from {
   opacity: 1;
 }
 
 .ele {
   transition: opacity 3s cubic-bezier(0.4, 0, 0.2, 1);
   opacity: 1; /* Changed from 10 to 1 for valid opacity */
   animation: fadeIn 3s forwards;
 }
 
 @keyframes fadeIn {
   0% {
     opacity: 0;
   }
 
   100% {
     opacity: 1;
   }
 }
 
 /* Optional: Adjust SVG size and position for responsiveness */
 svg {
   max-width: 100%;
   height: auto;
 }
 </style>
 
