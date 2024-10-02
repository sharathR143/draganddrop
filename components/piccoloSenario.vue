<template>
  <main>
    <aside class="flex justify-evenly py-4 mx-4 rounded-lg bg-white">
      <div
        class="cursor-pointer"
        :class="{ 'border-4 border-blue-500': selectedImage === 'driving' }"
        @click="selectImage('driving')"
      >
        <img
          src="/public/img/driving.jpeg"
          alt="parking image"
          class="w-[150px] rounded-lg h-[100px]"
        />
        <div class="flex justify-center">
          <p>Driving</p>
        </div>
      </div>

      <div
        class="cursor-pointer"
        :class="{ 'border-4 border-blue-500': selectedImage === 'parking' }"
        @click="selectImage('parking')"
      >
        <img
          src="/public/img/parking.jpg"
          alt="parking image"
          class="w-[150px] rounded-lg h-[100px]"
        />
        <div class="flex justify-center">
          <p>Parking</p>
        </div>
      </div>

      <div
        class="cursor-pointer"
        :class="{ 'border-4 border-blue-500': selectedImage === 'charging' }"
        @click="selectImage('charging')"
      >
        <img
          src="/public/img/charging.jpeg"
          alt="parking image"
          class="w-[150px] rounded-lg h-[100px]"
        />
        <div class="flex justify-center">
          <p>Charging</p>
        </div>
      </div>

      <div
        class="cursor-pointer"
        :class="{ 'border-4 border-blue-500': selectedImage === 'lowbattery' }"
        @click="selectImage('lowbattery')"
      >
        <img
          src="/public/img/lowbattery.jpeg"
          alt="parking image"
          class="w-[150px] rounded-lg h-[100px]"
        />
        <div class="flex justify-center">
          <p>Low Battery</p>
        </div>
      </div>
    </aside>

    <!-- host Name drag value section -->
    <aside class="mt-5 py-4 mx-4 rounded-lg bg-white">
      <div class="flex justify-center items-center cursor-grab">
        <div
          v-for="(containerName, index) in dragelement"
          :key="index"
          draggable="true"
          @dragstart="onDragStart(containerName)"
        >
          <p
            class="flex justify-center items-center text-center bg-gray-300 border-black/20 border-solid border-2 my-2 px-5 py-2 mx-3"
            v-if="
              containerName == 'camera' ||
              containerName == 'location' ||
              containerName == 'DSM'
            "
          >
            {{ containerName }}
          </p>
          <p
            class="flex justify-center items-center text-center bg-blue-300 border-black/20 border-solid border-2 my-2 px-5 py-2 mx-3"
            v-else
          >
            {{ containerName }}
          </p>
        </div>
      </div>
    </aside>

    <aside class="mt-5 py-4 mx-4 rounded-lg bg-white">
      <div class="flex justify-center items-center">
        <header v-for="(host, index) in hostnames" :key="index" class="mx-6">
          <div
            class="border-dashed border-2 min-h-[30px] border-gray-400 mb-5"
            @dragover.prevent
            @drop="onDropActions(host)"
          >
            <div v-for="container in host.containers" :key="container">
              {{ container }}
            </div>
            <!-- Render the dropped item for this specific host -->
            <!-- <div v-if="!droppedItems[host]" class="text-gray-500 px-3 py-2">
              drop
            </div>
            <div v-else class="px-3 py-2 bg-green-300">
              {{ droppedItems[host] }}
            </div> -->
          </div>

          <section class="bg-red-300">
            <div
              class="px-3 py-2 border bg-blue-400 border-gray-500 text-white text-center"
            >
              {{ host.system }}
            </div>
          </section>
        </header>
      </div>
    </aside>

    <footer>
      <div class="flex justify-end pt-2">
        <button
          class="px-2 py-2 mx-[10px] rounded-md w-[100px] text-sm text-white bg-gradient-to-r from-green-400 to-green-600 hover:from-green-500 hover:to-green-700 transition-all duration-300 shadow-md hover:shadow-lg transform hover:-translate-y-0.5 shadow-green-500/50"
          @click="createTemplate"
        >
          Create
        </button>
        <button
          class="px-2 py-2 mx-[10px] rounded-md w-[100px] text-sm text-white bg-gradient-to-r from-red-400 to-red-600 hover:from-red-500 hover:to-red-700 transition-all duration-300 shadow-md hover:shadow-lg transform hover:-translate-y-0.5 shadow-red-500/50"
          @click="cancelTemplate"
        >
          Cancel
        </button>
      </div>
    </footer>
  </main>
</template>

<script setup>
import { ref } from "vue";

const dragelement = ref([
  "rdv",
  "camera",
  "location",
  "mavd",
  "frism",
  "DSM",
  "bils",
]);
console.log(dragelement.value);

const hostnames = ref([
  { system: "soc0", containers: [] },
  { system: "soc1", containers: [] },
  { system: "zonal", containers: [] },
]);

const droppedItems = ref({
  soc0: null,
  soc1: null,
  zonal: null,
});

// Track the currently dragged item
const draggedItem = ref(null);

const onDragStart = (item) => {
  draggedItem.value = item;
};

// Handle when an item is dropped into the drop area for a specific host
const onDropActions = (host) => {
  console.log(" draggedItem.value", draggedItem.value);
  // Check if this host already has a dropped item
  console.log("host", host);
  hostnames.value.forEach((element) => {
    if (element.system == host.system) {
      element.containers.push(draggedItem.value);
    }
  });
  // if (!droppedItems.value[host]) {
  //   droppedItems.value[host] = draggedItem.value;
  // }

  draggedItem.value = null;
};

const selectedImage = ref(null);

// Handle selecting an image and applying the highlight
const selectImage = (imageName) => {
  selectedImage.value = imageName;
};

// Function to generate JSON data for dropped elements
const createTemplate = () => {
  let localStorageCards = localStorage.getItem("cards");
  if (localStorageCards) {
    localStorageCards = JSON.parse(localStorageCards);
    localStorageCards.push({
      name: selectedImage.value,
      components: hostnames.value,
    });
    localStorage.setItem("cards", JSON.stringify(localStorageCards));
  }

  // const template = {};
  // Object.keys(droppedItems.value).forEach((host) => {
  //   if (droppedItems.value[host]) {
  //     template[host] = droppedItems.value[host];
  //   }
  // });
  // console.log(JSON.stringify(template, null, 2));
};
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
</style>
