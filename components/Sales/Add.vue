<template>
  <TransitionRoot as="template" :show="open">
    <Dialog as="div" class="relative z-10">
      <TransitionChild
        as="template"
        enter="ease-out duration-300"
        enter-from="opacity-0"
        enter-to="opacity-100"
        leave="ease-in duration-200"
        leave-from="opacity-100"
        leave-to="opacity-0"
      >
        <div
          class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity"
        />
      </TransitionChild>

      <div class="fixed inset-0 z-10 overflow-y-auto">
        <div
          class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0"
        >
          <TransitionChild
            as="template"
            enter="ease-out duration-300"
            enter-from="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
            enter-to="opacity-100 translate-y-0 sm:scale-100"
            leave="ease-in duration-200"
            leave-from="opacity-100 translate-y-0 sm:scale-100"
            leave-to="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
          >
            <DialogPanel
              class="relative transform overflow-hidden rounded-lg bg-white px-4 pb-4 pt-5 text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-sm sm:p-6"
            >
              <div>
                <button>
                  <!-- closing the modal on clickng the trash icon -->
                  <TrashIcon
                    class="w-5 h-5"
                    @click="$emit('closeModal', 'add')"
                  />
                </button>

                <div
                  class="mx-auto flex h-12 w-12 items-center justify-center rounded-full bg-green-100"
                >
                  <CheckIcon
                    class="h-6 w-6 text-green-600"
                    aria-hidden="true"
                  />
                </div>
                <div class="mt-3  sm:mt-5">
                  <DialogTitle
                    as="h3"
                    class="text-base text-center font-semibold leading-6 text-gray-900"
                    >Add lead details</DialogTitle
                  >
                  <div class="mt-2">
                    <div class="mt-2 mb-3">
                      <!-- Name field starts here -->
                      <label for="name" class="text-base  font-semibold leading-6 text-gray-900">Name</label>
                      <input
                        ref="text_input_ref"
                        v-model="lead.name"
                        id="name"
                        type="textarea"
                        oninvalid="Enter at least 5 characters"
                        aria-describedby="input-live-help input-url-feedback"
                        autofocus
                        placeholder="Enter  Name"
                        class="block w-full mt-2 rounded-md border-0 text-gray-900 shadow-sm p-[8px] ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 focus-visible:ring-2 sm:text-sm sm:leading-6 focus-within:outline-none focus-visible:outline-none focus-visible:shadow-none focus-visible:ring-indigo-600"
                      />
                    </div>
                    <!-- Name field ends here -->
                    <!-- status starts here -->
                    <div class="mt-2 mb-3">
                      <label
                        for="type"
                        class="text-base  font-semibold leading-6 text-gray-900"
                        >Status</label
                      >
                      <div class="mt-2.5">
                        <select
                          v-model="lead.status"
                          id="type"
                          class="block w-full mt-2 rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                        >
                          <option value="Active">Active</option>
                          <option value="Interested">Interested</option>
                          <option value="Hot Interest">Hot Interest</option>
                          <option value="Not Interested">Not Interested</option>
                          <option value="Closed">Closed</option>
                        </select>
                      </div>
                    </div>
                    <!-- status ends here -->
                    <!-- phone number starts here -->
                    <div class="mt-2 mb-3">
                      <label for="phoneNumber" class="text-base  font-semibold leading-6 text-gray-900">phone Number</label>
                      <input
                        ref="text_input_ref"
                        v-model="lead.phone_number"
                        id="phoneNumber"
                        type="textarea"
                        oninvalid="Enter at least 5 characters"
                        aria-describedby="input-live-help input-url-feedback"
                        autofocus
                        placeholder="Enter  phone number"
                        class="block w-full mt-2 rounded-md border-0 text-gray-900 shadow-sm p-[8px] ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 focus-visible:ring-2 sm:text-sm sm:leading-6 focus-within:outline-none focus-visible:outline-none focus-visible:shadow-none focus-visible:ring-indigo-600"
                      />
                    </div>
                    <!-- phone number ends here -->
                    <!-- email starts here -->
                    <div class="mt-2 mb-3">
                      <label for="email" class="text-base  font-semibold leading-6 text-gray-900">Email</label>
                      <input
                        ref="text_input_ref"
                        v-model="lead.email"
                        id="email"
                        type="textarea"
                        oninvalid="Enter at least 5 characters"
                        aria-describedby="input-live-help input-url-feedback"
                        autofocus
                        placeholder="Enter  Email"
                        class="block w-full mt-2 rounded-md border-0 text-gray-900 shadow-sm p-[8px] ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 focus-visible:ring-2 sm:text-sm sm:leading-6 focus-within:outline-none focus-visible:outline-none focus-visible:shadow-none focus-visible:ring-indigo-600"
                      />
                    </div>
                    <!-- email ends here -->
                    <!--   Address starts here  -->
                    <div class="mt-2">
                      <label for="address" class="text-base  font-semibold leading-6 text-gray-900">
                        Address</label>
                      <input
                        ref="text_input_ref"
                        v-model="lead.address"
                        id="address"
                        type="textarea"
                        oninvalid="Enter at least 5 characters"
                        aria-describedby="input-live-help input-url-feedback"
                        autofocus
                        placeholder="Enter  address"
                        class="block w-full mt-2 rounded-md border-0 text-gray-900 shadow-sm p-[8px] ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 focus-visible:ring-2 sm:text-sm sm:leading-6 focus-within:outline-none focus-visible:outline-none focus-visible:shadow-none focus-visible:ring-indigo-600"
                      />
                    </div>
                    <!-- address ends here -->
                  </div>
                </div>
              </div>
              <!-- add website button starts here -->
              <div class="mt-5 sm:mt-6">
                <button
                  type="button"
                  class="inline-flex w-full justify-center rounded-md bg-slate-900 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-slate-800 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
                  @click="addLead"
                >
                  Add lead
                </button>
              </div>
              <!-- add website button ends here -->
            </DialogPanel>
          </TransitionChild>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
</template>
    
    <script setup lang="ts">
import { ref } from "vue";
import {
  Dialog,
  DialogPanel,
  DialogTitle,
  TransitionChild,
  TransitionRoot,
} from "@headlessui/vue";
import { CheckIcon } from "@heroicons/vue/24/outline";
import { TrashIcon } from "@heroicons/vue/20/solid";

const open = ref(true);

//emits starts here
const emits = defineEmits(["addLeadDetails", "closeModal"]);
//emits ends here

//lead details object
const lead: any = ref({
    "name": "",
    "source": "GharPe",
    "phone_number": "",
    "email": "",
    "status": "Active",
    "purpose_of_buying": "Investment",
    "address": "",
    "preferred_floor": 0,
    "facing": "string",
    "starred": true,
    "mode_of_payment": "Full Payment",
    "down_payment": "string",
    "is_loan_required": true,
    "cdata1": "string",
    "cdata2": "string",
    "project_id": "string",
    "uid": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
  });

//emitting lead details starts here
const addLead = () => {
  emits("addLeadDetails", lead.value);
  open.value = false;
};
// emits ends here
</script>