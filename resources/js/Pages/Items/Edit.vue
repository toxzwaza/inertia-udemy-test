<script setup>
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";
import { Head } from "@inertiajs/inertia-vue3";
import { reactive } from "vue";
import { Inertia } from "@inertiajs/inertia";
// import BreezeValidationErrors from '@/Components/ValidationErrors.vue';
import errorInput from "@/Components/InputError.vue";

const props = defineProps({
  item: Object,
});

const form = reactive({
  id: props.item.id,
  name: props.item.name,
  memo: props.item.memo,
  price: props.item.price,
  is_selling: props.item.is_selling,
});

// const storeItem = () => {
//     console.log(form);
//     Inertia.post("/items", form);
// };
const updateItem = (id) => {
  Inertia.put(route("items.update", { item: form.id }), form);
};

const deleteItem = (id) => {
  // console.log(id);
  Inertia.delete(route("items.destroy", { item: id }), {
    onBefore: () => {
      confirm("本当に削除しますか？");
    },
  });
};
</script>

<template>
  <Head title="Dashboard" />

  <AuthenticatedLayout>
    <template #header>
      <h2 class="font-semibold text-xl text-gray-800 leading-tight">
        商品編集
      </h2>
    </template>

    <div class="py-12">
      <!-- <BreezeValidationErrors :errors="errors"/> -->

      <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
        <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
          <section class="text-gray-600 body-font relative">
            <button
              @click="deleteItem(item.id)"
              class="mt-16 flex mx-auto text-white bg-red-500 border-0 py-2 px-8 focus:outline-none hover:bg-red-600 rounded text-lg"
            >
              削除する
            </button>

            <form action="" @submit.prevent="updateItem(form.id)">
              <div class="container px-5 py-4 mx-auto">
                <div class="lg:w-1/2 md:w-2/3 mx-auto">
                  <div class="flex flex-wrap -m-2">
                    <div class="p-2 w-full">
                      <div class="relative">
                        <label
                          for="name"
                          class="leading-7 text-sm text-gray-600"
                          >商品名</label
                        >

                        <input
                          type="text"
                          id="name"
                          name="name"
                          v-model="form.name"
                          class="w-full bg-gray-100 bg-opacity-50 rounded border border-gray-300 focus:border-indigo-500 focus:bg-white focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
                        />
                      </div>
                    </div>
                    <div class="p-2 w-full">
                      <div class="relative">
                        <label
                          for="price"
                          class="leading-7 text-sm text-gray-600"
                          >価格</label
                        >

                        <input
                          type="text"
                          id="price"
                          name="price"
                          v-model="form.price"
                          class="w-full bg-gray-100 bg-opacity-50 rounded border border-gray-300 focus:border-indigo-500 focus:bg-white focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
                        />
                      </div>
                    </div>
                    <div class="p-2 w-full">
                      <div class="relative">
                        <label
                          for="is_selling"
                          class="leading-7 text-sm text-gray-600"
                          >ステータス</label
                        ><br />

                        <label for="" class="mr-4">販売中</label>
                        <input
                          type="radio"
                          name="is_selling"
                          id=""
                          v-model="form.is_selling"
                          value="1"
                        />

                        <label for="" class="mr-4">停止中</label>
                        <input
                          type="radio"
                          name="is_selling"
                          id=""
                          v-model="form.is_selling"
                          value="0"
                        />
                      </div>
                    </div>

                    <div class="p-2 w-full">
                      <div class="relative">
                        <label
                          for="memo"
                          class="leading-7 text-sm text-gray-600"
                          >メモ</label
                        >

                        <textarea
                          id="memo"
                          name="memo"
                          v-model="form.memo"
                          class="w-full bg-gray-100 bg-opacity-50 rounded border border-gray-300 focus:border-indigo-500 focus:bg-white focus:ring-2 focus:ring-indigo-200 h-32 text-base outline-none text-gray-700 py-1 px-3 resize-none leading-6 transition-colors duration-200 ease-in-out"
                        ></textarea>
                      </div>
                    </div>
                    <div class="p-2 w-full flex justify-center">
                      <button
                        class="flex mx-auto text-white bg-indigo-500 border-0 py-2 px-8 focus:outline-none hover:bg-indigo-600 rounded text-lg"
                      >
                        更新
                      </button>
                    </div>
                    <div
                      class="p-2 w-full pt-8 mt-8 border-t border-gray-200 text-center"
                    >
                      <a class="text-indigo-500">example@email.com</a>
                      <p class="leading-normal my-5">
                        49 Smith St. <br />Saint Cloud, MN 56301
                      </p>
                      <span class="inline-flex">
                        <a class="text-gray-500">
                          <svg
                            fill="currentColor"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            class="w-5 h-5"
                            viewBox="0 0 24 24"
                          >
                            <path
                              d="M18 2h-3a5 5 0 00-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 011-1h3z"
                            ></path>
                          </svg>
                        </a>
                        <a class="ml-4 text-gray-500">
                          <svg
                            fill="currentColor"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            class="w-5 h-5"
                            viewBox="0 0 24 24"
                          >
                            <path
                              d="M23 3a10.9 10.9 0 01-3.14 1.53 4.48 4.48 0 00-7.86 3v1A10.66 10.66 0 013 4s-4 9 5 13a11.64 11.64 0 01-7 2c9 5 20 0 20-11.5a4.5 4.5 0 00-.08-.83A7.72 7.72 0 0023 3z"
                            ></path>
                          </svg>
                        </a>
                        <a class="ml-4 text-gray-500">
                          <svg
                            fill="none"
                            stroke="currentColor"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            class="w-5 h-5"
                            viewBox="0 0 24 24"
                          >
                            <rect
                              width="20"
                              height="20"
                              x="2"
                              y="2"
                              rx="5"
                              ry="5"
                            ></rect>
                            <path
                              d="M16 11.37A4 4 0 1112.63 8 4 4 0 0116 11.37zm1.5-4.87h.01"
                            ></path>
                          </svg>
                        </a>
                        <a class="ml-4 text-gray-500">
                          <svg
                            fill="currentColor"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            class="w-5 h-5"
                            viewBox="0 0 24 24"
                          >
                            <path
                              d="M21 11.5a8.38 8.38 0 01-.9 3.8 8.5 8.5 0 01-7.6 4.7 8.38 8.38 0 01-3.8-.9L3 21l1.9-5.7a8.38 8.38 0 01-.9-3.8 8.5 8.5 0 014.7-7.6 8.38 8.38 0 013.8-.9h.5a8.48 8.48 0 018 8v.5z"
                            ></path>
                          </svg>
                        </a>
                      </span>
                    </div>
                  </div>
                </div>
              </div>
            </form>
          </section>
        </div>
      </div>
    </div>
  </AuthenticatedLayout>
</template>
