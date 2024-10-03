<template>
  <main>
    <!-- scenario  -->
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
          alt="charging image"
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
          alt="low battery image"
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
            v-else
            class="flex justify-center items-center text-center bg-blue-300 border-black/20 border-solid border-2 my-2 px-5 py-2 mx-3"
          >
            {{ containerName }}
          </p>
        </div>
      </div>
    </aside>

    <aside
      class="mt-5 py-4 mx-4 rounded-lg bg-red-00 bg-white overflow-auto h-[140px]"
    >
      <div class="flex justify-center items-center">
        <header
          v-for="(host, index) in hostnames"
          :key="index"
          class="mx-6 bg-green-00 overflow-auto"
        >
          <div
            class="border-dashed border-[2px] hover:border-dashed hover:border-3 px-2 bg-red-00 min-h-[30px] border-gray-300 mb-5"
            @dragover.prevent
            @drop="onDropActions(host)"
          >
            <div
              v-for="container in host.containers"
              :key="container"
              class="border-gray-400 border-solid mt-1 border-2 text-center text-[14px] px-2 bg-red-00 mb-1"
            >
              {{ container }}
            </div>
          </div>

          <section class="bg-yellow-00">
            <div
              class="px-6 py-2 border bg-blue-400 border-gray-500 text-white text-center"
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
          :disabled="!canCreate"
          :class="{ 'opacity-50 cursor-not-allowed': !canCreate }"
        >
          Create
        </button>
        <button
          class="px-2 py-2 mx-[10px] rounded-md w-[100px] text-sm text-white bg-gradient-to-r from-red-400 to-red-600 hover:from-red-500 hover:to-red-700 transition-all duration-300 shadow-md hover:shadow-lg transform hover:-translate-y-0.5 shadow-red-500/50"
          @click="cancelTemplate"
          :disabled="!canCreate"
          :class="{ 'opacity-50 cursor-not-allowed': !canCreate }"
        >
          Cancel
        </button>
      </div>
    </footer>
  </main>
</template>

<script setup>
// import { ref } from "vue";
import { ref, computed } from "vue";

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

const draggedItem = ref(null);
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
//   let localStorageCards = localStorage.getItem("cards");
//   const localStorageLength = localStorageCards.length;
//   console.log("localStorageLength", localStorageLength);
//   if (localStorageCards) {
//     localStorageCards = JSON.parse(localStorageCards);
//     localStorageCards.push({
//       id: localStorageLength + 1,
//       name: selectedImage.value,
//       components: hostnames.value,
//     });
//     localStorage.setItem("cards", JSON.stringify(localStorageCards));
//     cancelTemplate();
//   }
// };

const createTemplate = () => {
  // Retrieve the existing cards from localStorage, if none exist, initialize an empty array
  let localStorageCards = localStorage.getItem("cards");

  // Parse the existing cards if available, otherwise initialize an empty array
  localStorageCards = localStorageCards ? JSON.parse(localStorageCards) : [];

  // Get the length of the existing array
  const localStorageLength = localStorageCards.length;

  console.log("Existing cards length:", localStorageLength);

  // Add a new card with id incremented based on the current length
  localStorageCards.push({
    id: localStorageLength + 1, // New card id will be length + 1
    name: selectedImage.value, // Assuming selectedImage is an input field or variable with value
    components: hostnames.value, // Assuming hostnames is an input field or variable with value
  });

  // Save the updated array back to localStorage
  localStorage.setItem("cards", JSON.stringify(localStorageCards));

  // Call the function to clear/reset the template after saving
  cancelTemplate();
};

const cancelTemplate = () => {
  selectedImage.value = null; // Clear selected image
  draggedItem.value = null; // Clear dragged item
  hostnames.value.forEach((host) => {
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
</style>
