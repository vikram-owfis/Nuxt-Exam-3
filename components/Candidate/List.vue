<template>
  <div>
    <!--  pending block starts here-->
    <div v-if="pending">
      <div class="flex flex-1 flex-col p-8">
        <img
          class="mx-auto h-72 w-72 flex-shrink-0 rounded-full"
          :src="'https://cdn1.vectorstock.com/i/1000x1000/49/90/loading-icon-on-black-vector-24544990.jpg'"
          alt=""
        />
      </div>
    </div>
    <!-- pending block ends here -->

    <!-- add button start here -->
    <button
      v-if="!pending && candidateMockList.length == 0"
      type="button"
      @click="isAdding = true"
      class="rounded-md bg-gray-950 px-3.5 py-2.5 text-sm font-semibold text-white shadow-sm hover:bg-gray-500 mb-5"
    >
      {{ addButton }}
    </button>
    <!-- add button start here -->

    <!-- candidate details  starts here -->
    <div v-if="candidateMockList && candidateMockList.length">
      <div class="px-4 sm:px-6 lg:px-8">
        <div class="sm:flex sm:items-center">
          <div class="sm:flex-auto">
            <h1 class="text-base font-semibold leading-6 text-gray-900">
              {{ heading }}
            </h1>
            <p class="mt-2 text-sm text-gray-700">
              {{ subHeading }}
            </p>
          </div>
          <div class="mt-4 sm:ml-16 sm:mt-0 sm:flex-none">
            <button
              type="button"
              @click="isAdding = true"
              class="rounded-md bg-gray-950 px-3.5 py-2.5 text-sm font-semibold text-white shadow-sm hover:bg-gray-500 mb-5"
            >
              Add Mock
            </button>
          </div>
        </div>
        <div class="mt-8 flow-root">
          <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
            <div
              class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8"
            >
              <div
                class="overflow-hidden shadow ring-1 ring-black ring-opacity-5 sm:rounded-lg"
              >
                <table class="min-w-full divide-y divide-gray-300">
                  <thead class="bg-gray-50">
                    <tr>
                      <th
                        scope="col"
                        class="py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-6"
                      >
                        Name
                      </th>
                      <th
                        scope="col"
                        class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
                      >
                        Type
                      </th>
                      <th
                        scope="col"
                        class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
                      >
                     Difficulty Level
                      </th>
                      <th
                        scope="col"
                        class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
                      >
                      Description
                      </th>
                    </tr>
                  </thead>
                  <tbody class="divide-y divide-gray-200 bg-white">
                    <tr
                      v-for="(candidae, index) in candidateMockList"
                      :key="index"
                    >
                      <td
                        class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:pl-6"
                      >
                        {{ candidae.name }}
                      </td>
                      <td
                        class="whitespace-nowrap px-3 py-4 text-sm text-gray-500"
                      >
                        {{ candidae.type }}
                      </td>
                      <td
                        class="whitespace-nowrap px-3 py-4 text-sm text-gray-500"
                      >
                        {{ candidae.difficulty_level }}
                      </td>
                      <td
                        class="whitespace-nowrap px-3 py-4 text-sm text-gray-500"
                      >
                        {{ candidae.description }}
                      </td>
                      
                    </tr>
                  </tbody>
                </table>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- candidate details ends here -->

    <!-- add candidate slide bar  starts here -->
    <div>
      <CandidateAdd
        v-if="isAdding"
        @addCandidateMock="addCandidateMock"
        @closeSidebar="closeSidebar"
      />
    </div>
    <!-- add candidate slide bar ends here -->

    <!-- No candidate data starts here -->
    <div v-if="candidateMockList.length == 0 && !pending">
      <div class="flex flex-col items-center">
        <img
          class="h-72 w-72 mb-4"
          src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRU3rUmjOvvo41Ga_G44WjcenlHmAJhBZpWtg&usqp=CAU"
        />
        <h1 class="text-2xl font-bold">
          No Candidte Mock Details found Here
        </h1>
      </div>
    </div>
    <!-- No candidae  data ends here -->
  </div>
</template>
  
  <script setup lang="ts">
import { PencilIcon, TrashIcon } from "@heroicons/vue/24/outline";

//props schema
interface PropsSchema {
  baseUrl: string;
  heading: string;
  subHeading: string;
  addButton: string;
}
//props schema ends here

// getting Props starts here
const props = defineProps<PropsSchema>();
// getting Props ends here

//varialbe declarations starts here
const candidateMockList: any = ref([]);
const isAdding: any = ref(false);
const pending: any = ref(true);
//varialbe declarations ends here

// authorization headers starts here
const authHeader: any = ref({
  "Content-Type": "application/json",
  Authorization:
    "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiZjVmNDA1ZDI2OTY4NDZjYWE2ZmM5Njg2Y2RmZjkxNmIiLCJkIjoiMTY4MDA5MCIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMyODI5OTR9._rhH6CTYng4fHBadjPUrBL3PdhYUO4y4z9XjtB6qHWo",
});
// authorization headers ends here

//getting  candidate mock detailss on mounted starts here
onMounted(async () => {
  await getCandidteDetails();
});
// getting candidte mock details on mounted ends here

//getting  candidate mock detailss  starts here
const getCandidteDetails = async () => {
  const data: any = await $fetch(
    `${props.baseUrl}/?offset=0&limit=100&sort_column=id&sort_direction=desc`,
    {
      method: "GET",
      headers: authHeader.value,
    }
  );
  candidateMockList.value = data;
  pending.value = false;
  return data.reverse(); //we are showing last in first reversing the array
};
//getting candidate mock detailss  ends here

//post call adding application to db starts here
const addCandidateMock = async (application: any) => {
  console.log(application);

  const { data, pending, error } = await useFetch(`${props.baseUrl}/`, {
    method: "POST",
    headers: authHeader.value,
    body: JSON.stringify(application),
  });
  isAdding.value = false;
  candidateMockList.value = getCandidteDetails(); //get candidate details
  //Note: we calling this function to get uid for the newly added data .if we directly add data into array we will not get uid
};
//post call ends here

//closing  add candidate mock detailss  sidebar
const closeSidebar = () => {
  isAdding.value = false;
};
</script>
  