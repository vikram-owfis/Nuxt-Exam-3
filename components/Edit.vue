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
                  <!-- closing the modal on clicing trash icon -->
                  <TrashIcon
                    class="w-5 h-5"
                    @click="emits('closeModal', 'edit')"
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
                <div class="mt-3 text-center sm:mt-5">
                  <DialogTitle
                    as="h3"
                    class="text-base font-semibold leading-6 text-gray-900"
                    >Update Webstite</DialogTitle
                  >
                  <div class="mt-2">
                    <!-- name field starts here -->
                    <div class="mt-2">
                      <input
                        ref="text_input_ref"
                        v-model="updateWebSite.name"
                        type="textarea"
                        oninvalid="Enter at least 5 characters"
                        aria-describedby="input-live-help input-url-feedback"
                        autofocus
                        placeholder="Enter name"
                        class="block w-full rounded-md border-0 text-gray-900 shadow-sm p-[8px] ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 focus-visible:ring-2 sm:text-sm sm:leading-6 focus-within:outline-none focus-visible:outline-none focus-visible:shadow-none focus-visible:ring-indigo-600"
                      />
                    </div>
                    <!-- Name field ends here -->
                    <!-- URL field starts here -->
                    <div class="mt-2">
                      <input
                        ref="text_input_ref"
                        v-model="updateWebSite.url"
                        type="textarea"
                        oninvalid="Enter at least 5 characters"
                        aria-describedby="input-live-help input-url-feedback"
                        autofocus
                        placeholder="Enter url"
                        class="block w-full rounded-md border-0 text-gray-900 shadow-sm p-[8px] ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 focus-visible:ring-2 sm:text-sm sm:leading-6 focus-within:outline-none focus-visible:outline-none focus-visible:shadow-none focus-visible:ring-indigo-600"
                      />
                    </div>
                    <!-- URL field ends here -->
                  </div>
                </div>
              </div>
              <!-- update button starts here -->
              <div class="mt-5 sm:mt-6">
                <button
                  type="button"
                  class="inline-flex w-full justify-center rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
                  @click="updateSelected"
                >
                  Update
                </button>
              </div>
              <!-- update button ends here -->
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

//define emits starts here
const emits = defineEmits(["updateWebSite", "closeModal"]);
//define emits ends here

//props schema starts here
interface UpdateWebSiteSchema {
  selectedWebSite: {
    name: string;
    url: string;
    uid: string;
  };
}
// props schema ends here

//defining props
const props = defineProps<UpdateWebSiteSchema>();

//website details  
const updateWebSite: any = ref({
  name: props.selectedWebSite.name,
  url: props.selectedWebSite.url,
  uid: props.selectedWebSite.uid,
});

//emiting the updated website starts here
const updateSelected = () => {
  console.log(updateWebSite, "sdf");
  emits("updateWebSite", updateWebSite);
  open.value = false;
};
//emitting the updated website ends here
</script>