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
                        >Application Details</DialogTitle
                      >
                      <div class="ml-3 flex h-7 items-center">
                        <button
                          type="button"
                          class="rounded-md bg-white text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2"
                          @click="open = false"
                        >
                          <XMarkIcon
                            @click="emtis('closeSidebar', 'add')"
                            class="h-6 w-6"
                            aria-hidden="true"
                          />
                        </button>
                      </div>
                    </div>
                  </div>

                  <div class="relative mt-6 flex-1 px-4 sm:px-6">
                    <!-- job posting  starts here -->

                    <div class="mt-2 mb-3">
                      <label
                        for="jobPosting"
                        class="text-base font-semibold leading-6 text-gray-900"
                        >Job posting ID</label
                      >
                      <input
                        ref="text_input_ref"
                        v-model="application.job_posting_id"
                        type="textarea"
                        oninvalid="Enter at least 5 characters"
                        aria-describedby="input-live-help input-url-feedback"
                        autofocus
                        id="jobPosting"
                        placeholder="Job Posting Id"
                        class="block w-full mt-2 rounded-md border-0 text-gray-900 shadow-sm p-[8px] ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 focus-visible:ring-2 sm:text-sm sm:leading-6 focus-within:outline-none focus-visible:outline-none focus-visible:shadow-none focus-visible:ring-indigo-600"
                      />
                    </div>
                    <!-- job posting  ends here -->
                    <!-- status starts here -->
                    <div class="mt-2 mb-3">
                      <label
                        for="status"
                        class="text-base font-semibold leading-6 text-gray-900"
                        >Status</label
                      >
                      <div class="mt-2.5">
                        <select
                        v-model="application.status"
                          id="status"
                          class="block w-full mt-2 rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                        >
                          <!-- <option>Applied</option>
                          <option>Disqualified</option>
                          <option>Shortlisted</option>
                          <option>Rejected</option> -->
                          <option value="Applied">Applied</option>
                          <option value="Disqualified">Disqualified</option>
                          <option value="Shortlisted">Shortlisted</option>
                          <option value="Rejected">Rejected</option>
                        </select>
                      </div>
                    </div>
                    <!-- status ends here -->

                    <!-- cover letter starts here -->
                    <div class="mt-2 mb-3">
                      <label
                        for="coverLetter"
                        class="text-base font-semibold leading-6 text-gray-900"
                        >Cover letter</label
                      >
                      <input
                        ref="text_input_ref"
                        v-model="application.cover_letter"
                        type="textarea"
                        oninvalid="Enter at least 5 characters"
                        aria-describedby="input-live-help input-url-feedback"
                        autofocus
                        id="coverLetter"
                        placeholder="cover letter"
                        class="block w-full mt-2 rounded-md border-0 text-gray-900 shadow-sm p-[8px] ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 focus-visible:ring-2 sm:text-sm sm:leading-6 focus-within:outline-none focus-visible:outline-none focus-visible:shadow-none focus-visible:ring-indigo-600"
                      />
                    </div>
                    <!-- cover letter ends here -->
                    <!-- resume url starts here -->
                    <div class="mt-2">
                      <label
                        for="resumeUrl"
                        class="text-base font-semibold leading-6 text-gray-900"
                        >Resume Url</label
                      >
                      <input
                        ref="text_input_ref"
                        v-model="application.resume_url"
                        type="textarea"
                        oninvalid="Enter at least 5 characters"
                        aria-describedby="input-live-help input-url-feedback"
                        autofocus
                        id="resumeUrl"
                        placeholder="Resume Url"
                        class="block w-full mt-2 rounded-md border-0 text-gray-900 shadow-sm p-[8px] ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 focus-visible:ring-2 sm:text-sm sm:leading-6 focus-within:outline-none focus-visible:outline-none focus-visible:shadow-none focus-visible:ring-indigo-600"
                      />
                    </div>
                    <!-- resume url ends here -->
                  </div>
                  <!-- add website button starts here -->
              <div class="mt-5 flex justify-between">
                <button
                  type="button"
                  @click="emtis('closeSidebar')"
                  class="inline-flex w-full mr-3  justify-center rounded-md bg-slate-900 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-slate-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
                >
                  Cancel
                </button>
                <button
                  type="button"
                  @click="addApplication"
                  class="inline-flex w-full justify-center rounded-md bg-slate-900 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-slate-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
                >
                  Add application
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
const emtis = defineEmits(["addApplication", "closeSidebar"]);


//application details object
const application = ref({
  candidate_id: "",
  job_posting_id: "",
  status: "Applied",
  resume_url: "",
  cover_letter: "",
  track_info: [],
  questionnaire: []
}); 

const addApplication = ()=> {
  emtis('addApplication',application.value)
}
</script>