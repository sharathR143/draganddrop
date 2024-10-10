<template>
  <main
    class="bg-white bg-emerald-00 mt-10 pb-[40px] pt-5 3xl:px-[10px] 3xl:mt-5 rounded-lg xl:w-[1200px] 1xl:w-[1280px] 2xl:w-[1460px] 3xl:w-[1830px] xl:ml-[-60px] 1xl:ml-[-100px] 2xl:ml-[30px] 3xl:ml-[-60px] 3xl:h-[850px]"
  >
    <div>
      <h1
        class="font-bold uppercase mb-[10px] pl-5 text-[#992121] text-[20px] 1xl:text-[17px] 3xl:text-[23px]"
      >
        PICCOLO Design studio
      </h1>
    </div>

    <div class="flex">
      <aside
        class="container rounded-lg ml-5 1xl:h-[500px] 2xl:h-[560px] pb-10 1xl:w-[680px] 2xl:w-[800px] 3xl:w-[1000px] 3xl:h-[730px]"
        style="background-color: #eff2ef"
      >
        <div
          class="pr-2 mt-[0px] ml-4 bg-red-00 relative left-[-8px] top-[6px] 3xl:top-[5px] w-[100px] h-[20px]"
        >
          <div class="flex bg-red-00 w-[250px] justify-between">
            <v-btn
              v-if="!showPiccoloScenario"
              icon="mdi-plus"
              size="small"
              color="primary"
              @click="togglePiccoloScenario"
              class="cursor-pointer"
            ></v-btn>
          </div>
        </div>

        <header v-if="!showPiccoloScenario">
          <main
            class="overflow-auto 3xl:pt-[60px] 1xl:h-[480px] pt-[40px] 2xl:h-[550px] 3xl:h-[680px] bg-gray-00 bg-red-00"
          >
            <div
              class="flex gap-2 bg-red-00 1xl:ml-[10px] 2xl:ml-[0px] 3xl:pt-[10px] justify-start"
            >
              <div
                v-for="(card, index) in cards"
                :key="card.id"
                class="bg-whit bg-red-300 m 1xl:w-[260px] cursor-pointer 2xl:w-[310px] 2xl:h-[450px] 3xl:h-[530px] 3xl:w-[400px] 2xl:ml-10 rounded-lg relative"
                @click="selectCard(card)"
                @dblclick="deselectCard(card.id)"
                @mousedown="startLongPress(card)"
                @mouseup="endLongPress"
                @mouseleave="endLongPress"
                @touchstart="startLongPress(card)"
                @touchend="endLongPress"
                @touchcancel="endLongPress"
                :class="[
                  'bg-white border-2 pr-5 mx-10 mb-10 rounded-lg relative cursor-poi5nter transition-colors duration-300',
                  currentAutoIndex == index
                    ? 'border-[3px] border-red-500'
                    : 'border-blue-500',
                ]"
              >
                <!-- Delete icon (centered and initially hidden) -->
                {{ currentAutoIndex == index }}
                <div
                  v-if="
                    (longPressedCard === card ||
                      deleteIconVisibleCards.includes(card.id)) &&
                    !card.isDefault
                  "
                  class="absolute top-[464px] left-[140px] 3xl:top-[550px] 3xl:left-[200px] inset-0 flex items-center justify-center cursor-pointer z-20 bg-opacity-50 bg-yellow-200 h-[10px] w-[10px] animate-bounce"
                >
                  <v-icon
                    @click.stop="deleteCard(card)"
                    color="white"
                    size="large"
                    >mdi-delete</v-icon
                  >
                </div>

                <div class="bg-red-00 flex justify-center items-center">
                  <img
                    v-if="getImageForCard(card.name)"
                    :src="getImageForCard(card.name)"
                    alt="Car images"
                    class="absolute top-[14px] 2xl:top-[25px] 3xl:top-[30px] left-[15px] 3xl:left-[20px] 1xl:h-[150px] 1xl:w-[230px] 2xl:h-[150px] 2xl:w-[270px] 3xl:h-[200px] 3xl:w-[350px] rounded-lg"
                  />
                </div>

                <div
                  class="bg-yellow-00 1xl:w-[255px] 2xl:w-[300px] 3xl:w-[390px] flex justify-center capitalize pt-[170px] 2xl:pt-[180px] 3xl:pt-[240px] text-[#992121] font-bold mr-9"
                >
                  {{ card.name }}
                </div>

                <section
                  class="bg-red-00 h-[250px] pb-4 overflow-auto flex justify-center items-end"
                >
                  <div
                    class="flex justify-end items-end min-h-[250px] overflow-y-auto bg-red-00"
                  >
                    <div
                      class="w-[80px] h-[40px] absolute top-[280px] left-[50px] 3xl:top-[330px] 3xl:left-[100px]"
                      v-if="card.name === 'Eco mode ON for BMS'"
                    >
                      <svg
                        xmlns="http://www.w3.org/2000/svg"
                        viewBox="0 0 240 180"
                      >
                        <defs>
                          <!-- Cloud gradient -->
                          <linearGradient
                            id="cloudGradient"
                            x1="0%"
                            y1="0%"
                            x2="0%"
                            y2="100%"
                          >
                            <stop offset="0%" style="stop-color: #ffffff" />
                            <stop offset="100%" style="stop-color: #e0e0e0" />
                          </linearGradient>
                          <!-- Zzz gradient -->
                          <linearGradient
                            id="zzzGradient"
                            x1="0%"
                            y1="0%"
                            x2="100%"
                            y2="100%"
                          >
                            <stop offset="0%" style="stop-color: #6a8caf" />
                            <stop offset="100%" style="stop-color: #4a6a8c" />
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
                    <section
                      v-for="system in card.components"
                      :key="system.system"
                      :class="[
                        card.name === 'Eco mode ON for BMS' &&
                        system.system === 'HPC'
                          ? 'bg-gray-300 pt-2 rounded-lg opacity-50'
                          : '',
                      ]"
                    >
                      <div
                        class="bg-blue-300 1xl:px-2 1xl:py-1 1xl:mx-3 2xl:px-[15px] 2xl:py-[5px] mb-1 2xl:mx-3 3xl:px-3 3xl:py-2 3xl:mx-2 flex justify-center text-[16px] items-center"
                        v-for="containerName in system.containers"
                        :key="containerName"
                        :class="[
                          card.name === 'Eco mode ON for BMS' &&
                          system.system === 'HPC'
                            ? 'bg-gray-300 pt-2 rounded-lg opacity-50'
                            : '',
                        ]"
                      >
                        {{ containerName }}
                      </div>

                      <div
                        class="1xl:px-3 border-2 uppercase border-blue-500 border-dashed 1xl:py-1 1xl:mx-3 2xl:px-[15px] 2xl:py-[5px] mb-1 2xl:mx-3 3xl:px-3 3xl:py-2 3xl:mx-2 flex justify-center items-center"
                      >
                        {{ system.system }}
                      </div>
                    </section>
                  </div>
                </section>
              </div>
            </div>
          </main>
        </header>
        <PiccoloScenario
          v-else
          @close="handleCloseScenario"
          class="bg-red-00"
        />
      </aside>
      <aside>
        <Servicelocation
          :selectedCardName="selectedCardName"
          class="relative top-[-420px] left-[25px] xl:top-[-10px] xl:left-[30px] 1xl:top-[0px] 1xl:left-[10px] 2xl:top-[0px] 2xl:left-[20px] 3xl:left-[70px]"
        />
      </aside>
    </div>
  </main>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount, watch } from "vue";
// import axios from "axios";
// import yaml from "js-yaml";

// COMPONENTS
import PiccoloScenario from "./piccoloSenario.vue";
import Servicelocation from "./servicelocation.vue";

// IMAGES
import carDriving from "../public/img/driving.jpeg";
import carParking from "../public/img/parking.jpg";
import carCharging from "../public/img/charging.jpeg";

const nuxtApp = useNuxtApp();
const API_URL = nuxtApp.$config.public.apiUrl;

const showPiccoloScenario = ref(false);
const selectedCardId = ref(null);
const animationCardId = ref(null);
const arrowVisible = ref(false);
const deleteIconVisible = ref(false);
const longPressedCard = ref(null);
const longPressTimer = ref(null);
const deleteIconVisibleCards = ref([]);
const selectedCardName = ref(null);

const togglePiccoloScenario = () => {
  showPiccoloScenario.value = true;
};

const handleCloseScenario = () => {
  showPiccoloScenario.value = false;
  reloadPage();
};

const reloadPage = () => {
  initialiationMethod();
};
let cards = ref([
  {
    id: 1,
    name: "High-performance for BMS",
    isDefault: true,
    conditionsvalue: "30",
    targetsname: "performance",
    conditionsexpress: "ge",
    operandsname: "battery_capacity",
    components: [
      { system: "HPC", containers: ["frism", "blis", "mavd"] },
      { system: "ZONE", containers: ["rdv"] },
    ],
  },
  {
    id: 2,
    name: "Eco mode ON for BMS",
    isDefault: true,
    conditionsvalue: "30",
    conditionsexpress: "lt",
    targetsname: "ecu",
    operandsname: "battery_capacity",
    components: [
      { system: "HPC", containers: ["mavd"] },
      { system: "ZONE", containers: ["frism", "blis", "rdv"] },
    ],
  },
]);

let animationTimer = null;
let autoSelectTimer = null;
let currentAutoIndex = ref(0);

const getImageForCard = (cardName) => {
  const images = {
    "High-performance for BMS": carDriving,
    "Eco mode ON for BMS": carParking,
    "Charging for BMS": carCharging,
  };
  return images[cardName] || null;
};

// -------------------- Initialization -------------------- //
const initialiationMethod = () => {
  let localStorageCards = localStorage.getItem("cards");

  if (localStorageCards) {
    cards.value = JSON.parse(localStorageCards);
  } else {
    localStorage.setItem("cards", JSON.stringify(cards.value));
  }
  resetAutoSelection(); // Reset auto selection when cards are loaded
};

// -------------------- Selection Logic -------------------- //
const selectCard = async (card) => {
  if (selectedCardId.value === card.id) {
    resetAnimation(card.id);
    return;
  }

  selectedCardId.value = card.id;
  arrowVisible.value = true;
  deleteIconVisible.value = false;

  setTimeout(() => {
    deleteIconVisible.value = true;
  }, 2000);

  startAnimation(card.id);
  // resetAutoSelection();

  // Prepare data in YAML format
  const scenarioData = {
    apiVersion: "v1",
    kind: "Scenario",
    metadata: { name: "bms" },
    spec: {
      conditions: {
        express: card.conditionsexpress,
        value: card.conditionsvalue,
        operands: {
          type: "DDS",
          name: card.operandsname,
          value: `rt/piccolo/${card.operandsname}`,
        },
      },
      chargingStatus: card.chargingStatus,
      actions: [{ operation: "update" }],
      targets: [{ name: `bms-algorithm-${card.targetsname}` }],
    },
  };

  // const yamlData = yaml.dump(scenarioData);
  // try {
  //   const response = await axios.post(API_URL, yamlData, {
  //     headers: { "Content-Type": "application/x-yaml" },
  //   });
  //   console.log("Data sent successfully:", response.data);
  // } catch (error) {
  //   console.error("Error sending data:", error);
  // }
};

const deselectCard = (cardId) => {
  if (selectedCardId.value === cardId) {
    selectedCardId.value = null;
    animationCardId.value = null;
    clearAnimationTimer();
  }
};

// -------------------- Animation Logic -------------------- //
const startAnimation = (cardId) => {
  clearAnimationTimer();
  animationCardId.value = cardId;
  animationTimer = setTimeout(() => {
    animationCardId.value = null;
    animationTimer = null;
  }, 3000);
};

const resetAnimation = (cardId) => {
  // clearAnimationTimer();
  startAnimation(cardId);
};

const clearAnimationTimer = () => {
  if (animationTimer) {
    clearTimeout(animationTimer);
    animationTimer = null;
  }
};

// -------------------- Long Press Logic -------------------- //
const longPressDuration = 500; // milliseconds
const deleteIconVisibleDuration = 5000; // 5 seconds

const startLongPress = (card) => {
  if (longPressTimer.value) clearTimeout(longPressTimer.value);
  longPressTimer.value = setTimeout(() => {
    longPressedCard.value = card;
    if (!deleteIconVisibleCards.value.includes(card.id)) {
      deleteIconVisibleCards.value.push(card.id);
      setTimeout(() => {
        deleteIconVisibleCards.value = deleteIconVisibleCards.value.filter(
          (id) => id !== card.id
        );
      }, deleteIconVisibleDuration);
    }
  }, longPressDuration);
};

const endLongPress = () => {
  if (longPressTimer.value) {
    clearTimeout(longPressTimer.value);
    longPressTimer.value = null;
  }
  longPressedCard.value = null;
};

// -------------------- Auto Selection Logic -------------------- //
const startAutoSelection = () => {
  // if (autoSelectTimer) return;

  setInterval(() => {
    if (cards.value.length === 0) return;
    if (cards.value.length == currentAutoIndex.value) {
      currentAutoIndex.value = 0;
      // console.log("if");
    }

    const card = cards.value[currentAutoIndex.value];
    if (card) {
      console.log("currentAutoIndex", currentAutoIndex.value);
      // selectCard(card);
    }

    currentAutoIndex.value++;
    // currentAutoIndex;
  }, 3000); // 3000 milliseconds = 3 seconds
};

const resetAutoSelection = () => {
  // clearAutoSelection();
  // currentAutoIndex = 0;
  // currentAutoIndex.value;
  // startAutoSelection();
};

const clearAutoSelection = () => {
  if (autoSelectTimer) {
    clearInterval(autoSelectTimer);
    autoSelectTimer = null;
  }
};

// -------------------- Watchers -------------------- //
watch(selectedCardId, (newId) => {
  const selectedCard = cards.value.find((card) => card.id === newId);
  selectedCardName.value = selectedCard ? selectedCard.name : null;
});
watch(cards, (newvalue) => {
  console.log(newvalue, "card-new-value");
  // currentAutoIndex = 0;
  // startAutoSelection();
});
// -------------------- Lifecycle Hooks -------------------- //
onMounted(() => {
  initialiationMethod();
  currentAutoIndex.value = 0;
  startAutoSelection();
});

onBeforeUnmount(() => {
  clearAnimationTimer();
  clearAutoSelection();
  if (longPressTimer.value) clearTimeout(longPressTimer.value);
});

// -------------------- Card Management -------------------- //
const deleteCard = (card) => {
  if (card.isDefault) {
    alert("This card cannot be deleted.");
    return;
  }

  cards.value = cards.value.filter((c) => c.id !== card.id);
  localStorage.setItem("cards", JSON.stringify(cards.value));

  if (currentAutoIndex.value >= cards.value.length) {
    currentAutoIndex.value = 0; // Reset to 0 if we've deleted the last card
  }

  if (selectedCardId.value === card.id) {
    selectedCardId.value = null;
    animationCardId.value = null;
    clearAnimationTimer();
  }

  deleteIconVisibleCards.value = deleteIconVisibleCards.value.filter(
    (id) => id !== card.id
  );
};

// const addCard = (newCard) => {
//   cards.value.push(newCard);
//   localStorage.setItem("cards", JSON.stringify(cards.value));

//   // Automatically select the newly added card after 5 seconds
//   setTimeout(() => {
//     selectCard(newCard); // Select the new card
//   }, 1000); // 5000 milliseconds = 5 seconds

//   // Reset auto selection when a new card is added
//   resetAutoSelection();
// };
</script>

<style scoped>
.arrow-container {
  display: flex;
  justify-content: center;
  align-items: center;
  animation: moveArrow 2s infinite ease-in-out; /* Arrow animation */
}

.delete-icon-container {
  display: flex;
  justify-content: center;
  align-items: center;
  animation: 1s ease-in-out infinite; /* Delete icon animation */
}

@keyframes moveArrow {
  0% {
    transform: translateX(0);
  }
  50% {
    transform: translateX(0px); /* Move the arrow to the right */
  }
  100% {
    transform: translateX(0); /* Return to the original position */
  }
}

@keyframes delete-arrow {
  0%,
  100% {
    transform: rotate(180deg);
    transform: translate(0, 0);
  }
  50% {
    transform: rotate(180deg);
    transform: translate(10px, 0);
  }
}

.arrow {
  animation: moveArrow 2s infinite ease-in-out; /* Loop the animation */
}

.arrow-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh; /* Center the arrow vertically */
}

@keyframes moveArrow {
  0% {
    transform: translateX(0);
  }
  50% {
    transform: translateX(30px); /* Move the arrow to the right */
  }
  100% {
    transform: translateX(0); /* Return to the original position */
  }
}

.deletearrow {
  animation: delete-arrow 1s ease-in-out infinite;
}
@keyframes delete-arrow {
  0%,
  100% {
    transform: rotate(180deg);
    transform: translate(0, 0);
  }

  50% {
    transform: rotate(180deg);
    transform: translate(10px, 0);
  }
}

.v-icon {
  font-size: 36px;
}

.arrow-animation {
  animation: fadeInOut 4s forwards;
  z-index: 10;
  animation: bounceAnimation 3s infinite;
}

@keyframes bounceAnimation {
  0%,
  100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-20px);
  }
}

@keyframes fadeInOut {
  0% {
    opacity: 0;
    transform: translate(-50%, -20px);
  }
  20% {
    opacity: 1;
    transform: translate(-50%, 0);
  }
  80% {
    opacity: 1;
    transform: translate(-50%, 0);
  }
  100% {
    opacity: 0;
    transform: translate(-50%, 0);
  }
}

/* Fade transition effect */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to {
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
