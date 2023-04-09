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
      v-if="!pending"
      type="button"
      @click="isAdding = true"
      class="rounded-md bg-gray-950 px-3.5 py-2.5 text-sm font-semibold text-white shadow-sm hover:bg-gray-500"
    >
      <!--  -->
      {{ addButton }}
    </button>
    <!-- add button start here -->

    <!-- leads cards starts here -->
    <div v-if="leadDetailsList && leadDetailsList.length">
      <div>
        <ul
          role="list"
          class="p-2 grid grid-cols-1 gap-6 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 h-full"
        >
          <li
            v-for="(lead, index) in leadDetailsList"
            :key="index"
            class="col-span-1 flex flex-col divide-y divide-gray-200 rounded-lg bg-white text-center shadow"
          >
            <div class="flex flex-1 flex-col p-2">
              <h3 class="mt-6 text-base font-bold text-gray-900">
                Name: <span class="ml-3">{{ lead.name }}</span> 
              </h3>
              <dl class="mt-1 flex flex-grow flex-col justify-between">
                <dd class="text-base font-bold text-gray-900">
                  Phone Number:<span class="ml-3">{{ lead.phone_number }}</span> 
                </dd>
                <dd class="ftext-base font-bold text-gray-900">
                  Status:<span class="ml-3">{{ lead.status }}</span> 
                </dd>
                <dd class="mt-3">
                  <a
                    class="rounded-full bg-white px-2 py-1text-base font-bold text-blue-800 cursor-pointer"
                    >Email: <span class="ml-3">{{ lead.email }}</span> </a
                  >
                </dd>
                <dd class="text-base font-bold text-gray-900">
                  Address:<span class="ml-3">{{ lead.address }}</span> 
                </dd>
              
              </dl>
            </div>
            <div>
              <div class="-mt-px flex divide-x divide-gray-200">
                <div
                  class="flex w-0 flex-1 cursor-pointer"
                  @click="updateSelectedLead(lead)"
                >
                  <a
                    class="relative -mr-px inline-flex w-0 flex-1 items-center justify-center gap-x-3 rounded-bl-lg border border-transparent py-4 text-sm font-semibold text-gray-900"
                  >
                    <PencilIcon
                      class="h-5 w-5 text-gray-400"
                      aria-hidden="true"
                    />
                    Edit
                  </a>
                </div>
                <div
                  class="-ml-px flex w-0 flex-1 cursor-pointer"
                  @click="deleteLead(lead)"
                >
                  <a
                    class="relative inline-flex w-0 flex-1 items-center justify-center gap-x-3 rounded-br-lg border border-transparent py-4 text-sm font-semibold text-gray-900"
                  >
                    <TrashIcon
                      class="h-5 w-5 text-gray-400"
                      aria-hidden="true"
                    />
                    Delete
                  </a>
                </div>
              </div>
            </div>
          </li>
        </ul>
      </div>
      <div></div>
    </div>
    <!-- leads cards ends here -->

    <!-- And and Edit modals -->
    <div>
      <!-- Add modal starts here -->
      <SalesAdd
        v-if="isAdding"
        @addLeadDetails="addLeadDetails"
        @closeModal="closeModal"
      />
      <!-- add modal ends here -->

      <!-- edit modal stars here -->
      <SalesEdit
        v-if="isEditing"
        :selectedLead="selectedLead"
        @updateLead="updateLead"
        @closeModal="closeModal"
      />
      <!-- edit modal ends here -->
    </div>
    <!-- No lead  details starts here -->
    <div v-if="leadDetailsList.length == 0 && !pending">
      <div class="flex flex-col items-center">
        <img
          class="h-72 w-72 mb-4"
          src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRU3rUmjOvvo41Ga_G44WjcenlHmAJhBZpWtg&usqp=CAU"
        />
        <h1 class="text-2xl font-bold">No data Found</h1>
      </div>
    </div>
    <!-- No lead details ends here -->
  </div>
</template>
    
    <script setup lang="ts">
import { PencilIcon, TrashIcon } from "@heroicons/vue/20/solid";

//Props Schema
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
const leadDetailsList: any = ref([]);
const isAdding: any = ref(false);
const isEditing: any = ref(false);
const pending: any = ref(true);
const selectedLead: any = ref();
let indexOfSelected;
//varialbe declarations ends here

// authorization headers starts here
const authHeader: any = ref({
  "Content-Type": "application/json",
  Authorization:
    "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiZjVmNDA1ZDI2OTY4NDZjYWE2ZmM5Njg2Y2RmZjkxNmIiLCJkIjoiMTY4MDA5MCIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMyODI5OTR9._rhH6CTYng4fHBadjPUrBL3PdhYUO4y4z9XjtB6qHWo",
});
// authorization headers ends here

//getting lead details on mounted starts here
onMounted(async () => {
  await getLeadDetails();
});
// getting lead details on mounted ends here

//finding the index  starts here
const getIndexOfSelected = (uid: any) => {
  let index = leadDetailsList.value.findIndex((item: any) => item.uid == uid);
  return index;
};
// finding the index  ends here

const updateSelectedLead = (website: any) => {
  selectedLead.value = website;
  isEditing.value = true;
};

//getting  lead details starts here
const getLeadDetails = async () => {
  const data = await $fetch(
    `${props.baseUrl}/?offset=0&limit=100&sort_column=id&sort_direction=desc`,
    {
      method: "GET",
      headers: authHeader.value,
    }
  );
  leadDetailsList.value = data;
  pending.value = false;

  return data;
};
//getting lead details ends here

//post call adding lead details to db starts here
const addLeadDetails = async (webSite: any) => {
  const { data, pending, error } = await useFetch(`${props.baseUrl}/`, {
    method: "POST",
    headers: authHeader.value,
    body: JSON.stringify(webSite),
  });
  isAdding.value = false;
  let sites = getLeadDetails();
  leadDetailsList.value = sites;
};
//post call adding lead details to db starts here

//updating the selected lead on click on update button starts here
const updateLead = async (updatedLead: any) => {
  const { data, error } = await useFetch(
    `${props.baseUrl}/${updatedLead.value.uid}`,
    {
      method: "PUT",
      headers: authHeader.value,
      body: JSON.stringify(updatedLead.value),
    }
  );

  //get the index of lead
  indexOfSelected = getIndexOfSelected(updatedLead.value.uid);
  leadDetailsList.value[indexOfSelected] = updatedLead.value;
  isEditing.value = false;
};
//update call ends here

//delete lead starts here on click on trash icon
const deleteLead = async (lead: any) => {
  const { data, error } = await useFetch(`${props.baseUrl}/${lead.uid}`, {
    method: "DELETE",
    headers: authHeader.value,
  });
  //get the index of lead
  indexOfSelected = getIndexOfSelected(lead.uid);
  leadDetailsList.value.splice(indexOfSelected, 1);
};
//delete call ends here

//closing add or edit modal
const closeModal = (value: any) => {
  if (value == "edit") isEditing.value = false;
  isAdding.value = false;
};
</script>