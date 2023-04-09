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
                        >Candidate Mock</DialogTitle
                      >
                      <div class="ml-3 flex h-7 items-center">
                        <button
                          type="button"
                          class="rounded-md bg-white text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2"
                          @click="open = false"
                        >
                          <XMarkIcon
                            @click="emtis('closeSidebar')"
                            class="h-6 w-6"
                            aria-hidden="true"
                          />
                        </button>
                      </div>
                    </div>
                  </div>

                  <div class="relative mt-6 flex-1 px-4 sm:px-6">
                    <!-- candidate name starts here -->

                    <div class="mt-2 mb-3">
                      <label
                        for="name"
                        class="text-base font-semibold leading-6 text-gray-900"
                        >Name</label
                      >
                      <input
                        ref="text_input_ref"
                        v-model="candidae.name"
                        type="textarea"
                        oninvalid="Enter at least 5 characters"
                        aria-describedby="input-live-help input-url-feedback"
                        autofocus
                        id="name"
                        placeholder="Enter Name"
                        class="block w-full mt-2 rounded-md border-0 text-gray-900 shadow-sm p-[8px] ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 focus-visible:ring-2 sm:text-sm sm:leading-6 focus-within:outline-none focus-visible:outline-none focus-visible:shadow-none focus-visible:ring-indigo-600"
                      />
                    </div>
                    <!-- candidate name ends here -->
                    <!-- type  starts here -->
                    <div class="mt-2 mb-3">
                      <label
                        for="type"
                        class="text-base font-semibold leading-6 text-gray-900"
                        >Type</label
                      >
                      <div class="mt-2.5">
                        <select
                          v-model="candidae.type"
                          id="type"
                          class="block w-full mt-2 rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                        >
                          <!-- <option>Applied</option>
                            <option>Disqualified</option>
                            <option>Shortlisted</option>
                            <option>Rejected</option> -->
                          <option value="practice">practice</option>
                          <option value="videoprofile">videoprofile</option>
                        </select>
                      </div>
                    </div>
                    <!-- type ends here -->

                    <!-- difficulty level starts here -->
                    <div class="mt-2 mb-3">
                      <label
                        for="type"
                        class="text-base font-semibold leading-6 text-gray-900"
                        >Difficulty Level</label
                      >
                      <div class="mt-2.5">
                        <select
                          v-model="candidae.difficulty_level"
                          id="type"
                          class="block w-full mt-2 rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                        >
                          <!-- <option>Applied</option>
                            <option>Disqualified</option>
                            <option>Shortlisted</option>
                            <option>Rejected</option> -->
                          <option value="Easy">Easy</option>
                          <option value="Medium">Medium</option>
                          <option value="Hard">Hard</option>
                        </select>
                      </div>
                    </div>
                    <!-- difficulty level ends here -->
                    <!-- Description starts here -->
                    <div class="mt-2">
                      <label
                        for="Description"
                        class="text-base font-semibold leading-6 text-gray-900"
                        >Description</label
                      >
                      <input
                        ref="text_input_ref"
                        v-model="candidae.description"
                        type="textarea"
                        oninvalid="Enter at least 5 characters"
                        aria-describedby="input-live-help input-url-feedback"
                        autofocus
                        id="Description"
                        placeholder="Resume Url"
                        class="block w-full mt-2 rounded-md border-0 text-gray-900 shadow-sm p-[8px] ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 focus-visible:ring-2 sm:text-sm sm:leading-6 focus-within:outline-none focus-visible:outline-none focus-visible:shadow-none focus-visible:ring-indigo-600"
                      />
                    </div>
                    <!-- Description ends here -->
                  </div>
                  <!-- add website button starts here -->
                  <div class="mt-5 flex justify-between">
                    <button
                      type="button"
                      @click="emtis('closeSidebar')"
                      class="inline-flex w-full mr-3 justify-center rounded-md bg-slate-900 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-slate-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
                    >
                      Cancel
                    </button>
                    <button
                      type="button"
                      @click="addCandidate"
                      class="inline-flex w-full justify-center rounded-md bg-slate-900 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-slate-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
                    >
                      Add Mock
                    </button>
                  </div>
                  <!-- add website button ends here -->
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
const emtis = defineEmits(["addCandidateMock", "closeSidebar"]);

//candidate details object
const candidae = ref({
  name: "",
  type: "practice",
  max_time_allowed: 0,
  due_date: "2023-04-09T11:42:54.118Z",
  difficulty_level: "Easy",
  description: "",
  questions: {},
  multiple_attempts_allowed: 0,
  instructions: {},
  status: 0,
  owner_id: "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  last_modified_date: "2023-04-09T11:42:54.118Z",
});

//emitting the added values
const addCandidate = () => {
  emtis("addCandidateMock", candidae.value);
};
</script>