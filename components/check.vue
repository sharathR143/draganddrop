


<template>
    <main class="bg-white mt-10 py-5 3xl:px-[10px] 3xl:mt-5 rounded-lg xl:w-[1200px] 1xl:w-[1280px] 2xl:w-[1460px] 3xl:w-[1830px] xl:ml-[-60px] 1xl:ml-[-100px] 2xl:ml-[-190px] 3xl:ml-[-60px] 3xl:h-[900px]">
       <div>
         <h1 class="font-bold uppercase mb-[10px] pl-5 text-[#992121] text-[20px] 1xl:text-[17px] 3xl:text-[23px]">PICCOLO Design Studio</h1>
       </div>
   
       <div class="flex">
         <aside class="container pt-10 rounded-lg ml-5 1xl:h-[500px] 2xl:h-[550px] pb-10 1xl:w-[680px] 2xl:w-[800px] 3xl:w-[1000px] 3xl:h-[740px]" style="background-color:#EFF2EF;">
           <div class="pr-2 mt-0 ml-4 bg-red-00 relative left-[-10px] top-[-30px] w-[100px] h-[30px]">
             <div class="flex bg-red-00 w-[250px] justify-between">
               <v-btn :icon="showPiccoloScenario ? 'mdi-close' : 'mdi-plus'" size="small" color="primary" @click="togglePiccoloScenario" class="cursor-pointer"></v-btn>
               <div v-if="showPiccoloScenario" class="mr-2 mt-2 text-[20px] text-[#992121] font-bold">Scenario Creator</div>
             </div>
           </div>
   
           <header v-if="!showPiccoloScenario">
             <main class="bg-red-00 overflow-auto pt-5 h-[450px]">
               <div class="flex gap-2 flex-wrap ml-[30px] py-5 justify-start">
                 <div
                   v-for="card in cards"
                   :key="card.id"
                   @click="selectCard(card)"
                   @dblclick="deselectCard(card.id)"
                   :class="[
                     'bg-white ml-10 mb-10 rounded-lg relative cursor-pointer transition-colors duration-300',
                     selectedCardId === card.id ? 'border-4 border-red-500' : 'border-2 border-blue-500'
                   ]"
                 >
                   <!-- SVG Animation -->
                   <div v-if="animationCardId === card.id" class="absolute top-[100px] left-[50%] transform -translate-x-1/2 text-4xl text-red-500 arrow-animation">
                     <!-- SVG Code -->
                     <svg
                       xmlns="http://www.w3.org/2000/svg"
                       viewBox="0 0 1080 1080"
                       width="80"
                       height="80"
                       preserveAspectRatio="xMidYMid meet"
                       class="w-full h-full transform rotate-90"
                     >
                       <!-- SVG Content -->
                       <defs>
                         <clipPath id="__lottie_element_27881">
                           <rect width="1080" height="1080" x="0" y="0"></rect>
                         </clipPath>
                       </defs>
                       <g clip-path="url(#__lottie_element_27881)">
                         <g
                           transform="matrix(3.19,0,0,3.19,424.1,338.81)"
                           opacity="1"
                           style="display: block"
                         >
                           <g opacity="1" transform="matrix(1,0,0,1,50.73,64.32)">
                             <path
                               fill="rgb(255,94,0)"
                               d="M46.055,5.84 C50.479,2.628 50.479,-2.629 46.055,-5.841 C46.055,-5.841 -44.6,-60.858 -44.6,-60.858 C-49.024,-64.071 -50.478,-61.874 -47.831,-55.977 C-47.831,-55.977 -16.658,0 -16.658,0 C-16.658,0 -47.831,55.977 -47.831,55.977 C-50.478,61.874 -49.024,64.071 -44.6,60.859 C-44.6,60.859 46.055,5.84 46.055,5.84z"
                             ></path>
                           </g>
                           <g opacity="1" transform="matrix(1,0,0,1,50.838,95.491)">
                             <path
                               fill="rgb(206,76,0)"
                               d="M-16.767,-31.169 C-16.767,-31.169 -47.941,24.808 -47.941,24.808 C-50.588,30.705 -49.134,32.902 -44.71,29.69 C-44.71,29.69 45.945,-25.329 45.945,-25.329 C48.157,-26.935 49.263,-29.052 49.263,-31.169 C49.263,-31.169 -16.767,-31.169 -16.767,-31.169z"
                             ></path>
                           </g>
                         </g>
                         <g
                           transform="matrix(3.19,0,0,3.19,264.098,338.813)"
                           opacity="1"
                           style="display: block"
                         >
                           <g opacity="1" transform="matrix(1,0,0,1,50.73,64.322)">
                             <path
                               fill="rgb(255,94,0)"
                               d="M46.055,5.84 C50.479,2.628 50.479,-2.629 46.055,-5.841 C46.055,-5.841 -44.6,-60.858 -44.6,-60.858 C-49.024,-64.071 -50.478,-61.874 -47.831,-55.977 C-47.831,-55.977 -16.658,0 -16.658,0 C-16.658,0 -47.831,55.977 -47.831,55.977 C-50.478,61.874 -49.024,64.071 -44.6,60.859 C-44.6,60.859 46.055,5.84 46.055,5.84z"
                             ></path>
                           </g>
                           <g opacity="1" transform="matrix(1,0,0,1,50.838,95.491)">
                             <path
                               fill="rgb(206,76,0)"
                               d="M-16.767,-31.169 C-16.767,-31.169 -47.941,24.808 -47.941,24.808 C-50.588,30.705 -49.134,32.902 -44.71,29.69 C-44.71,29.69 45.945,-25.329 45.945,-25.329 C48.157,-26.935 49.263,-29.052 49.263,-31.169 C49.263,-31.169 -16.767,-31.169 -16.767,-31.169z"
                             ></path>
                           </g>
                         </g>
                       </g>
                     </svg>
                   </div>
   
                   <!-- Card Image Section -->
                   <div class="bg-red-300 flex justify-center items-center relative h-[150px]">
                     <img
                       v-if="getImageForCard(card.name)"
                       :src="getImageForCard(card.name)"
                       alt="Car images"
                       class="absolute top-[10px] left-[15px] h-[150px] w-[270px] rounded-lg object-cover"
                     />
                   </div>
   
                   <!-- Card Name Section -->
                   <div class="bg-yellow-00 flex justify-center capitalize pt-[170px] mr-9 text-lg font-semibold text-[#992121]">
                     {{ card.name }}
                   </div>
   
                   <!-- Card Content Section -->
                   <section class="bg-red-00 min-h-[250px] mb-5 overflow-auto flex">
                     <div class="flex justify-end items-end w-full">
                       <div v-for="system in card.components" :key="system.system" class="w-full">
                         <div
                           class="bg-gray-300 px-2 py-1 mb-1 mx-3 flex justify-center text-[16px] items-center rounded"
                           v-for="containerName in system.containers"
                           :key="containerName"
                         >
                           {{ containerName }}
                         </div>
                         <div class="bg-blue-300 px-5 py-1 mb-1 mx-3 flex justify-center items-center rounded">
                           {{ system.system }}
                         </div>
                       </div>
                     </div>
                   </section>
                 </div>
               </div>
             </main>
           </header>
   
           <PiccoloScenario v-else @close="showPiccoloScenario = false" />
         </aside>
   
         <aside>
           <Servicelocation :selectedCardName="selectedCardName" class="relative top-[-420px] left-[25px] xl:top-[-10px] xl:left-[30px] 1xl:top-[0px] 1xl:left-[10px] 2xl:top-[0px] 2xl:left-[20px] 3xl:left-[70px]" />
         </aside>
       </div>
     </main>
   
     <!-- <main class="bg-white mt-10  py-5  3xl:px-[10px] 3xl:mt-5 rounded-lg  xl:w-[1200px] 1xl:w-[1280px] 2xl:w-[1460px] 3xl:w-[1830px] xl:ml-[-60px] 1xl:ml-[-100px] 2xl:ml-[-190px] 3xl:ml-[-60px]  3xl:h-[900px]">
       <div>
         <h1 class="font-bold  uppercase  mb-[10px]  pl-5 text-[#992121]  text-[20px] 1xl:text-[17px] 3xl:text-[23px]">PICCOLO Design studio</h1>
       </div>
   
       
       <div class="flex">
         <aside  class="container pt-10  rounded-lg  ml-5  1xl:h-[500px] 2xl:h-[550px] pb-10  1xl:w-[680px] 2xl:w-[800px]  3xl:w-[1000px] 3xl:h-[740px]  " style="background-color:#EFF2EF;">
           <div class="pr-2 mt-[0px] ml-4  bg-red-00 relative left-[-10px] top-[-30px]  w-[100px] h-[30px]">
             <div class="flex  bg-red-00 w-[250px] justify-between">
               <v-btn :icon="showPiccoloScenario ? 'mdi-close' : 'mdi-plus'" size="small" color="primary" @click="togglePiccoloScenario"  class="cursor-pointer "></v-btn>
               <div v-if="showPiccoloScenario" class="mr-2 mt-2 text-[20px] text-[#992121] font-bold">Scenario Creator</div>
             </div>
           </div>
   
   
         <header v-if="!showPiccoloScenario" >
           <main class=" bg-red-00  overflow-auto pt-5  h-[450px]">
             <div class="flex gap-2 flex-wrap ml-[30px] py-5 justify-start">
               <div v-for="card in cards" :key="card"  class="bg-white   ml-10 mb-10  rounded-lg  relative"
                 @click="selectCard(card)" @dblclick="deselectCard"
                 :class="['bg-white border-2 ml-10 mb-10 rounded-lg relative cursor-pointer transition-colors duration-300',
                     selectedCard === card.name ? 'border-4 border-red-500' : 'border-blue-500'
                   ]">
                  <div v-if="animationCard === card.name"
                  class="absolute top-[-50px]  left-[110px] transform -translate-x-1/2 text-4xl text-red-500 arrow-animation"
                  >
                   <svg
                     xmlns="http://www.w3.org/2000/svg"
                     xmlns:xlink="http://www.w3.org/1999/xlink"
                     viewBox="0 0 1080 1080"
                     width="80"
                     height="80"
                     preserveAspectRatio="xMidYMid meet"
                     style="
                       width: 100%;
                       height: 100%;
                       transform: translate3d(0px, 0px, 0px) rotate(90deg);
                       content-visibility: visible;
                     "
                   >
                     <defs>
                       <clipPath id="__lottie_element_27881">
                         <rect width="1080" height="1080" x="0" y="0"></rect>
                       </clipPath>
                     </defs>
                     <g clip-path="url(#__lottie_element_27881)">
                       <g
                         transform="matrix(3.190000057220459,0,0,3.190000057220459,424.0982666015625,338.81280517578125)"
                         opacity="1"
                         style="display: block"
                       >
                         <g
                           opacity="1"
                           transform="matrix(1,0,0,1,50.72800064086914,64.3219985961914)"
                         >
                           <path
                             fill="rgb(255,94,0)"
                             fill-opacity="1"
                             d=" M46.05500030517578,5.840000152587891 C50.479000091552734,2.628000020980835 50.479000091552734,-2.628999948501587 46.05500030517578,-5.841000080108643 C46.05500030517578,-5.841000080108643 -44.599998474121094,-60.858001708984375 -44.599998474121094,-60.858001708984375 C-49.02399826049805,-64.07099914550781 -50.47800064086914,-61.874000549316406 -47.83100128173828,-55.97700119018555 C-47.83100128173828,-55.97700119018555 -16.658000946044922,0 -16.658000946044922,0 C-16.658000946044922,0 -47.83100128173828,55.97700119018555 -47.83100128173828,55.97700119018555 C-50.47800064086914,61.874000549316406 -49.02399826049805,64.07099914550781 -44.599998474121094,60.85900115966797 C-44.599998474121094,60.85900115966797 46.05500030517578,5.840000152587891 46.05500030517578,5.840000152587891z"
                           ></path>
                         </g>
                         <g
                           opacity="1"
                           transform="matrix(1,0,0,1,50.8380012512207,95.49099731445312)"
                         >
                           <path
                             fill="rgb(206,76,0)"
                             fill-opacity="1"
                             d=" M-16.767000198364258,-31.16900062561035 C-16.767000198364258,-31.16900062561035 -47.941001892089844,24.808000564575195 -47.941001892089844,24.808000564575195 C-50.5880012512207,30.704999923706055 -49.13399887084961,32.902000427246094 -44.709999084472656,29.690000534057617 C-44.709999084472656,29.690000534057617 45.94499969482422,-25.32900047302246 45.94499969482422,-25.32900047302246 C48.15700149536133,-26.934999465942383 49.26300048828125,-29.052000045776367 49.26300048828125,-31.16900062561035 C49.26300048828125,-31.16900062561035 -16.767000198364258,-31.16900062561035 -16.767000198364258,-31.16900062561035z"
                           ></path>
                         </g>
                       </g>
                       <g
                         transform="matrix(3.190000057220459,0,0,3.190000057220459,264.09820556640625,338.81280517578125)"
                         opacity="1"
                         style="display: block"
                       >
                         <g
                           opacity="1"
                           transform="matrix(1,0,0,1,50.72800064086914,64.3219985961914)"
                         >
                           <path
                             fill="rgb(255,94,0)"
                             fill-opacity="1"
                             d=" M46.05500030517578,5.840000152587891 C50.479000091552734,2.628000020980835 50.479000091552734,-2.628999948501587 46.05500030517578,-5.841000080108643 C46.05500030517578,-5.841000080108643 -44.599998474121094,-60.858001708984375 -44.599998474121094,-60.858001708984375 C-49.02399826049805,-64.07099914550781 -50.47800064086914,-61.874000549316406 -47.83100128173828,-55.97700119018555 C-47.83100128173828,-55.97700119018555 -16.658000946044922,0 -16.658000946044922,0 C-16.658000946044922,0 -47.83100128173828,55.97700119018555 -47.83100128173828,55.97700119018555 C-50.47800064086914,61.874000549316406 -49.02399826049805,64.07099914550781 -44.599998474121094,60.85900115966797 C-44.599998474121094,60.85900115966797 46.05500030517578,5.840000152587891 46.05500030517578,5.840000152587891z"
                           ></path>
                         </g>
                         <g
                           opacity="1"
                           transform="matrix(1,0,0,1,50.8380012512207,95.49099731445312)"
                         >
                           <path
                             fill="rgb(206,76,0)"
                             fill-opacity="1"
                             d=" M-16.767000198364258,-31.16900062561035 C-16.767000198364258,-31.16900062561035 -47.941001892089844,24.808000564575195 -47.941001892089844,24.808000564575195 C-50.5880012512207,30.704999923706055 -49.13399887084961,32.902000427246094 -44.709999084472656,29.690000534057617 C-44.709999084472656,29.690000534057617 45.94499969482422,-25.32900047302246 45.94499969482422,-25.32900047302246 C48.15700149536133,-26.934999465942383 49.26300048828125,-29.052000045776367 49.26300048828125,-31.16900062561035 C49.26300048828125,-31.16900062561035 -16.767000198364258,-31.16900062561035 -16.767000198364258,-31.16900062561035z"
                           ></path>
                         </g>
                       </g>
                     </g>
                   </svg>
                 </div>
   
   
                 <div class="bg-red-300 flex justify-center items-center ">
                   <img v-if="getImageForCard(card.name)"  :src='getImageForCard(card.name)'  alt="Car images" class="absolute top-[10px] left-[15px] h-[150px] w-[270px]  rounded-lg" />
                 </div>
                 <div class=" bg-yellow-00 flex justify-end capitalize  pt-[170px] mr-9" >
                   {{ card.name }}
                 </div>
   
   
                 <section class="bg-red-00  min-h-[250px] mb-5 overflow-auto flex ">
                 <div class="flex justify-end items-end ">
                   <div v-for="system in card.components" :key="system" class="">
                     <div class="bg-gray-300  px-2  py-1  mb-1  mx-3 flex justify-center text-[16px] items-center" v-for="containerName in system.containers" :key="containerName">
                       {{ containerName  }}
                     </div>
   
                     <div class="bg-blue-300  px-5  py-1  mb-1  mx-3 flex justify-center items-center ">
                       {{ system.system }}
                     </div>
                   </div>
                 </div>
                 </section>
   
               </div>
             </div>
   
         </main>
         </header>
   
         <PiccoloScenario v-else @close="showPiccoloScenario = false" />
       </aside>
        <aside>
         <Servicelocation :selectedCardName="selectedCard" class="relative top-[-420px] left-[25px] xl:top-[-10px] xl:left-[30px]  1xl:top-[0px] 1xl:left-[10px]  2xl:top-[0px] 2xl:left-[20px]  3xl:left-[70px]" />
       </aside> 
   
     </div>
   </main>  -->
   </template>
   <script setup>
   import { ref, onMounted, onBeforeUnmount, watch } from 'vue';
   // COMPONENTS
   import PiccoloScenario from './PiccoloScenario.vue';
   import Servicelocation from "../mco/service-location.vue";
   
   // IMAGES
   import carDriving from '../../public/img/car.png';
   import carParking from '../../public/img/car1.png';
   import carCharging from '../../public/img/charging.png';
   import carLowbattery from '../../public/img/lowbattery.png';
   
   // Reactive state for scenario creator visibility
   const showPiccoloScenario = ref(false);
   
   // Toggle function for the scenario creator
   const togglePiccoloScenario = () => {
     initialiationMethod();
     showPiccoloScenario.value = !showPiccoloScenario.value;
   };
   
   // Reactive state for cards with unique IDs
   let cards = ref([
     {
       id: 1, // Unique ID
       name: "driving",
       components: [
         { system: "soc0", containers: [] },
         { system: "soc1", containers: ["rdv", "mavd", "frism", "blis"] },
         { system: "zonal", containers: [] },
       ],
     },
     {
       id: 2, // Unique ID
       name: "parking",
       components: [
         { system: "soc0", containers: ["blis"] },
         { system: "soc1", containers: [] },
         { system: "zonal", containers: ["frism"] },
       ],
     },
    
     // Add more cards as needed
   ]);
   
   // Function to get image path based on card name
   const getImageForCard = (cardName) => {
     const images = {
       driving: carDriving,
       parking: carParking,
       charging: carCharging,
       lowbattery: carLowbattery
     };
     return images[cardName] || null;
   };
   
   // Reactive state to track the selected card's ID
   const selectedCardId = ref(null);
   
   // Reactive state to track which card is showing the animation
   const animationCardId = ref(null);
   
   // Timer reference to control the animation timeout
   let animationTimer = null;
   
   // Function to check if a card is selected
   const isSelected = (card) => selectedCardId.value === card.id;
   
   // Function to select a card (single click)
   const selectCard = (card) => {
     // If the same card is clicked again, restart the animation
     if (selectedCardId.value === card.id) {
       resetAnimation(card.id);
       return;
     }
   
     // Set the selected card ID
     selectedCardId.value = card.id;
     console.log('Selected Card ID:', selectedCardId.value);
   
     // Start the SVG animation
     startAnimation(card.id);
   };
   
   // Function to deselect a card (double click)
   const deselectCard = (cardId) => {
     if (selectedCardId.value === cardId) {
       selectedCardId.value = null;
       animationCardId.value = null;
       clearAnimationTimer();
       console.log('Deselected Card ID:', cardId);
     }
   };
   
   // Function to start the animation
   const startAnimation = (cardId) => {
     // Clear any existing animation timer
     clearAnimationTimer();
   
     // Set the animationCardId to the selected card
     animationCardId.value = cardId;
   
     // Start a new timer to hide the animation after 3 seconds
     animationTimer = setTimeout(() => {
       animationCardId.value = null;
       animationTimer = null;
     }, 3000);
   };
   
   // Function to reset the animation (optional)
   const resetAnimation = (cardId) => {
     // Clear existing timer
     clearAnimationTimer();
   
     // Restart the animation
     startAnimation(cardId);
   };
   
   // Function to clear the animation timer
   const clearAnimationTimer = () => {
     if (animationTimer) {
       clearTimeout(animationTimer);
       animationTimer = null;
     }
   };
   
   // Initialize method to handle localStorage
   const initialiationMethod = () => {
     let localStorageCards = localStorage.getItem("cards");
     if (localStorageCards) {
       cards.value = JSON.parse(localStorageCards);
     } else {
       localStorage.setItem("cards", JSON.stringify(cards.value));
       cards.value = JSON.parse(localStorage.getItem("cards"));
     }
   };
   
   // Initialize on mount
   onMounted(() => {
     initialiationMethod();
   });
   
   // Clean up the timer when the component is unmounted
   onBeforeUnmount(() => {
     clearAnimationTimer();
   });
   
   // Compute the selected card's name to pass as a prop
   const selectedCardName = ref(null);
   
   watch(selectedCardId, (newId) => {
     const selectedCard = cards.value.find(card => card.id === newId);
     selectedCardName.value = selectedCard ? selectedCard.name : null;
   });
   </script>
   
   
   <!-- 
   <script setup>
   import { ref, onMounted,onBeforeUnmount} from 'vue';
   // COMPONENTS
   import PiccoloScenario from './PiccoloScenario.vue';
   import Servicelocation from "../mco/service-location.vue";
   
   // IMAGES
   import carDriving  from '../../public/img/car.png'
   import carParking  from '../../public/img/car1.png'
   import carCharging  from '../../public/img/charging.png'
   import carLowbattery  from '../../public/img/lowbattery.png'
   
   
   
   
   
   const showPiccoloScenario = ref(false);
   
   const togglePiccoloScenario = () => {
     initialiationMethod();
     showPiccoloScenario.value = !showPiccoloScenario.value;
   };
   
   let cards = ref([
     {
       name: "driving",
       components: [
         { system: "soc0",  containers: [] },
         { system: "soc1",  containers: ["rdv", "mavd", "frism", "blis"] },
         { system: "zonal", containers: [] },
       ],
     },
     {
       name: "parking",
       components: [
         { system: "soc0",  containers: ["blis"] },
         { system: "soc1",  containers: [] },
         { system: "zonal", containers: ["frism"] },
       ],
     },
   ]);
   
   const getImageForCard = (cardName) => {
     const images = {
       driving: carDriving,
       parking: carParking,
       charging: carCharging, 
       lowbattery: carLowbattery
     }
     return images[cardName] || null 
   }
   
   
   onMounted(() => {
     initialiationMethod();
   });
   
   
   
   const initialiationMethod = () => {
     let localStorageCards = localStorage.getItem("cards");
     if (localStorageCards) {
       cards.value = JSON.parse(localStorageCards);
     } else {
       localStorageCards = localStorage.setItem(
         "cards",
         JSON.stringify(cards.value)
       );
       if (localStorageCards) {
         cards.value = JSON.parse(localStorageCards);
       }
     }
   };
   
   
   const selectedCard = ref(null);
   
   // Reactive state to track the card currently showing the animation
   const animationCard = ref(null);
   
   // Timer reference to control the animation timeout
   let animationTimer = null;
   
   // Function to check if a card is selected
   const isSelected = (card) => selectedCard.value === card.name;
   
   // Function to select a card (single click)
   const selectCard = (card) => {
     // If clicking the same card again, do nothing or reset the animation
     if (selectedCard.value === card.name) {
       // Optionally, you can reset the animation
       resetAnimation(card.name);
       return;
     }
    // Set the selected card
    selectedCard.value = card.name;
    console.log('selectedCard',selectedCard.value)
      // Start the animation
      startAnimation(card.name);
   };
   
   
   // Function to deselect a card (double click)
   const deselectCard = () => {
     selectedCard.value = null;
     animationCard.value = null;
     clearAnimationTimer();
   };
   
   // Function to start the animation
   const startAnimation = (cardName) => {
     // Clear any existing animation timer
     clearAnimationTimer();
     // Set the animationCard to the selected card
     animationCard.value = cardName;
   
     // Start a new timer to hide the animation after 3 seconds
     animationTimer = setTimeout(() => {
       animationCard.value = null;
       animationTimer = null;
     }, 3000);
   };
   
   
   // Function to reset the animation (optional)
   const resetAnimation = (cardName) => {
     // Clear existing timer
     clearAnimationTimer();
     // Restart the animation
     startAnimation(cardName);
   };
   
   
   // Function to clear the animation timer
   const clearAnimationTimer = () => {
     if (animationTimer) {
       clearTimeout(animationTimer);
       animationTimer = null;
     }
   };
   
   onBeforeUnmount(() => {
     clearAnimationTimer();
   });
   
   </script>
    -->
   
   <style scoped>
   .v-icon {
     font-size: 25px;
   }
   
   .arrow-animation {
     animation: fadeInOut 4s forwards;
     animation: bounceAnimation 3s infinite; 
   }
   
   @keyframes bounceAnimation {
     0%, 100% {
       transform: translateY(0); 
     }
     50% {
       transform: translateY(-20px); 
     }
   }
   
   @keyframes fadeInOut {
     0% { opacity: 0; transform: translate(-50%, -20px); }
     20% { opacity: 1; transform: translate(-50%, 0); }
     80% { opacity: 1; transform: translate(-50%, 0); }
     100% { opacity: 0; transform: translate(-50%, 0); }
   }
   
   /* Fade transition effect */
   .fade-enter-active, .fade-leave-active {
     transition: opacity 0.5s;
   }
   .fade-enter, .fade-leave-to {
     opacity: 0;
   }
   
   /* Arrow Animation */
   .arrow-right {
     animation: moveRightArrow 0.5s forwards;
   }
   
   .arrow-left {
     animation: moveLeftArrow 0.5s forwards;
   }
   
   @keyframes moveRightArrow {
     0% {
       opacity: 0;
       transform: translate(-50%, -50%) translateX(-20px);
     }
     50% {
       opacity: 1;
       transform: translate(-50%, -50%) translateX(0);
     }
     100% {
       opacity: 3;
       transform: translate(-50%, -50%) translateX(10px);
     }
   }
   
   @keyframes moveLeftArrow {
     0% {
       opacity: 0;
       transform: translate(-50%, -50%) translateX(20px);
     }
     50% {
       opacity: 1;
       transform: translate(-50%, -50%) translateX(0);
     }
     100% {
       opacity: 2;
       transform: translate(-50%, -50%) translateX(-20px);
     }
   }
   
   /* Optional: Add transition for border color change */
   .selected-card {
     transition: border-color 0.3s ease;
   }
   </style>
   
   
   
   <!-- 
   
   <style scoped> 
   .v-icon {
   font-size: 25px; 
   }
   
   
   .arrow-animation {
   
   animation: fadeInOut 4s forwards;
   animation: bounceAnimation 3s infinite; 
   }
   
   @keyframes bounceAnimation {
   0%, 100% {
     transform: translateY(0); 
   }
   50% {
     transform: translateY(-20px); 
   }
   }
   
   @keyframes fadeInOut {
   0% { opacity: 0; transform: translate(-50%, -20px); }
   20% { opacity: 1; transform: translate(-50%, 0); }
   80% { opacity: 1; transform: translate(-50%, 0); }
   100% { opacity: 0; transform: translate(-50%, 0); }
   }
   
   
   
   
   
   
   .fade-enter-active, .fade-leave-active {
     transition: opacity 0.5s;
   }
   .fade-enter, .fade-leave-to {
     opacity: 0;
   }
   
   .arrow-right {
     animation: moveRightArrow 0.5s forwards;
   }
   
   .arrow-left {
     animation: moveLeftArrow 0.5s forwards;
   }
   
   @keyframes moveRightArrow {
     0% {
       opacity: 0;
       transform: translate(-50%, -50%) translateX(-20px);
     }
     50% {
       opacity: 1;
       transform: translate(-50%, -50%) translateX(0);
     }
     100% {
       opacity: 3;
       transform: translate(-50%, -50%) translateX(10px);
     }
   }
   
   @keyframes moveLeftArrow {
     0% {
       opacity: 0;
       transform: translate(-50%, -50%) translateX(20px);
     }
     50% {
       opacity: 1;
       transform: translate(-50%, -50%) translateX(0);
     }
     100% {
       opacity: 2;
       transform: translate(-50%, -50%) translateX(-20px);
     }
   }
   
   </style>
   
   -->
