<template>
  <TransitionRoot as="template" :show="open">
    <Dialog as="div" class="relative z-10">
      <div class="fixed inset-0" />

      <div class="fixed inset-0 overflow-hidden">
        <div class="absolute inset-0 overflow-hidden">
          <div
            class="pointer-events-none fixed inset-y-0 right-0 flex max-w-full pl-10 sm:pl-16"
          >
            <TransitionChild
              as="template"
              enter="transform transition ease-in-out duration-500 sm:duration-700"
              enter-from="translate-x-full"
              enter-to="translate-x-0"
              leave="transform transition ease-in-out duration-500 sm:duration-700"
              leave-from="translate-x-0"
              leave-to="translate-x-full"
            >
              <DialogPanel class="pointer-events-auto w-screen max-w-2xl">
                <div
                  class="flex h-full flex-col overflow-y-scroll bg-white py-6 shadow-xl"
                >
                  <div class="px-4 sm:px-6">
                    <div class="flex items-start justify-between">
                      <DialogTitle
                        class="text-base font-semibold leading-6 text-gray-900"
                        >Builder Details</DialogTitle
                      >
                      <div class="ml-3 flex h-7 items-center">
                        <button
                          type="button"
                          class="rounded-md bg-white text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2"
                          @click="open = false"
                        >
                          <XMarkIcon
                            @click="emtis('closeModal', 'add')"
                            class="h-6 w-6"
                            aria-hidden="true"
                          />
                        </button>
                      </div>
                    </div>
                  </div>

                  <div class="relative mt-6 flex-1 px-4 sm:px-6">
                    <!-- builder name starts here -->

                    <div class="mt-2 mb-3">
                      <label
                        for="name"
                        class="text-base font-semibold leading-6 text-gray-900"
                        >Name</label
                      >
                      <input
                        ref="text_input_ref"
                        v-model="builder.name"
                        type="textarea"
                        oninvalid="Enter at least 5 characters"
                        aria-describedby="input-live-help input-url-feedback"
                        autofocus
                        id="name"
                        placeholder="Enter Name"
                        class="block w-full mt-2 rounded-md border-0 text-gray-900 shadow-sm p-[8px] ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 focus-visible:ring-2 sm:text-sm sm:leading-6 focus-within:outline-none focus-visible:outline-none focus-visible:shadow-none focus-visible:ring-indigo-600"
                      />
                    </div>
                    <!-- builder name ends here -->
                    <!-- phone number  starts here -->
                    <div class="mt-2 mb-3">
                      <label
                        for="phoneNumber"
                        class="text-base font-semibold leading-6 text-gray-900"
                        >Phone Number</label
                      >
                      <input
                        ref="text_input_ref"
                        v-model="builder.phone_number"
                        type="textarea"
                        oninvalid="Enter at least 5 characters"
                        aria-describedby="input-live-help input-url-feedback"
                        autofocus
                        id="phoneNumber"
                        placeholder="Enter phone number"
                        class="block w-full mt-2 rounded-md border-0 text-gray-900 shadow-sm p-[8px] ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 focus-visible:ring-2 sm:text-sm sm:leading-6 focus-within:outline-none focus-visible:outline-none focus-visible:shadow-none focus-visible:ring-indigo-600"
                      />
                    </div>
                    <!-- phone number ends here -->

                    <!-- email  starts here -->
                    <div class="mt-2 mb-3">
                      <label
                        for="email"
                        class="text-base font-semibold leading-6 text-gray-900"
                        >Email</label
                      >
                      <input
                        ref="text_input_ref"
                        v-model="builder.email"
                        type="textarea"
                        oninvalid="Enter at least 5 characters"
                        aria-describedby="input-live-help input-url-feedback"
                        autofocus
                        id="email"
                        placeholder="Enter email"
                        class="block w-full mt-2 rounded-md border-0 text-gray-900 shadow-sm p-[8px] ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 focus-visible:ring-2 sm:text-sm sm:leading-6 focus-within:outline-none focus-visible:outline-none focus-visible:shadow-none focus-visible:ring-indigo-600"
                      />
                    </div>
                    <!-- email  ends here -->
                    <!-- Description starts here -->
                    <div class="mt-2">
                      <label
                        for="establishedYear"
                        class="text-base font-semibold leading-6 text-gray-900"
                      >
                        Established year</label
                      >
                      <input
                        ref="text_input_ref"
                        v-model="builder.established_year"
                        type="textarea"
                        oninvalid="Enter at least 5 characters"
                        aria-describedby="input-live-help input-url-feedback"
                        autofocus
                        id="establishedYear"
                        placeholder="Enter Established Year"
                        class="block w-full mt-2 rounded-md border-0 text-gray-900 shadow-sm p-[8px] ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 focus-visible:ring-2 sm:text-sm sm:leading-6 focus-within:outline-none focus-visible:outline-none focus-visible:shadow-none focus-visible:ring-indigo-600"
                      />
                    </div>
                    <!-- Description ends here -->
                  </div>
                  <!-- add builder button starts here -->
                  <div class="mt-5 flex justify-between">
                    <button
                      type="button"
                      @click="emtis('closeModal')"
                      class="inline-flex w-full mr-3 justify-center rounded-md bg-slate-900 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-slate-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
                    >
                      Cancel
                    </button>
                    <button
                      type="button"
                      @click="addBuilder"
                      class="inline-flex w-full justify-center rounded-md bg-slate-900 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-slate-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
                    >
                      Add Builder
                    </button>
                  </div>
                  <!-- add builder button ends here -->
                </div>
              </DialogPanel>
            </TransitionChild>
          </div>
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
import { XMarkIcon } from "@heroicons/vue/24/outline";

const open = ref(true);
//defining emits
const emtis = defineEmits(["addBuilder", "closeModal"]);

//builder details object
const builder = ref({
  name: "",
  email: "",
  phone_number: "",
  established_year: "",
  tag_line: "",
  reg_details: "",
  reg_rera_url: "",
  is_active: true,
});

//emitting the builder details
const addBuilder = () => {
  emtis("addBuilder", builder.value);
};
</script>