<template>
  <h1 class="">張珮綺</h1>
  <!-- 自我介紹 -->
  <div class=' rounded-lg shadow-2xl m-2 p-4'>
    <h2 class="font-semibold text-gray-900">基本資料</h2>
    <div class="mt-6 border-t border-gray-100">
      <dl class="divide-y divide-gray-100">
        <div class="px-4 py-6 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-0">
          <dt class="mb-2 font-semibold">電子郵件</dt>
          <dd class="mt-1 text-sm leading-6 text-gray-700 sm:col-span-2 sm:mt-0">{{ personalInfo.email }}</dd>
          <dt class="mb-2 font-semibold">手機</dt>
          <dd class="mt-1 text-sm leading-6 text-gray-700 sm:col-span-2 sm:mt-0">{{ personalInfo.phone }}</dd>
          <dt class="mb-2 font-semibold">地址</dt>
          <dd class="mt-1 text-sm leading-6 text-gray-700 sm:col-span-2 sm:mt-0">{{ personalInfo.address }}</dd>
        </div>
      </dl>
    </div>
    <!-- 學歷 -->
    <h2 class="font-semibold text-gray-900">學歷</h2>
    <div class="mt-6 border-t border-gray-100">
      <dl class="divide-y divide-gray-100">
        <div class="px-4 py-6 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-0" v-for="edu in education" :key="edu.id">
          <dt class="mb-2 font-semibold">{{ edu.degree }}</dt>
          <dd class="mt-1 text-sm leading-6 text-gray-700 sm:col-span-2 sm:mt-0">{{ edu.school }} &nbsp; {{ edu.year }}
          </dd>
        </div>
      </dl>
    </div>
    <!-- 工作經歷 -->
    <h2 class="font-semibold text-gray-900">工作經歷</h2>
    <div class="mt-6 border-t border-gray-100">
      <dl class="divide-y divide-gray-100">
        <div class="px-4 py-6 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-0" v-for="exp in experience" :key="exp.id">
          <dt class="mb-2 font-semibold">職稱</dt>
          <dd class="mt-1 text-sm leading-6 text-gray-700 sm:col-span-2 sm:mt-0">{{ exp.position }}</dd>
          <dt class="mb-2 font-semibold">公司</dt>
          <dd class="mt-1 text-sm leading-6 text-gray-700 sm:col-span-2 sm:mt-0">{{ exp.company }}</dd>
          <dt class="mb-2 font-semibold">時間</dt>
          <dd class="mt-1 text-sm leading-6 text-gray-700 sm:col-span-2 sm:mt-0">{{ exp.year }}</dd>
        </div>
      </dl>
    </div>
    <!-- 專業技能 -->
    <h2 class="font-semibold text-gray-900">專業技能</h2>
    <div class="mt-6 border-t border-gray-100">
      <div class="mt-6 px-4 mb-6 sm:px-6 lg:px-8 border rounded">
        <div class="flow-root">
          <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
            <div class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8">
              <table class="min-w-full divide-y divide-gray text-center">
                <thead>
                  <tr class="divide-x divide-gray ">
                    <th scope="col" class="py-3.5 pl-4 pr-4  text-sm font-semibold text-gray-900 sm:pl-0">前端技能
                    </th>
                    <th scope="col" class="px-4 py-3.5  text-sm font-semibold text-gray-900">後端技能</th>
                    <th scope="col" class="px-4 py-3.5  text-sm font-semibold text-gray-900">資料庫</th>
                  </tr>
                </thead>
                <tbody class="divide-y divide-gray bg-white text-left">
                  <tr v-for="skill in skills_row1" :key="skill.id " class="divide-x divide-gray">
                    <td class="whitespace-nowrap py-4 pl-4 pr-4 text-sm font-medium text-gray-900 sm:pl-0">{{
                      skill.frontend_name }}</td>
                    <td class="whitespace-nowrap p-4 text-sm text-black">{{ skill.backend_name }}</td>
                    <td class="whitespace-nowrap p-4 text-sm text-black">{{ skill.database_name }}</td>
                  </tr>
                  <tr v-for="skill in skills_row2" :key="skill.id" class="divide-x divide-gray">
                    <td class="whitespace-nowrap py-4 pl-4 pr-4 text-sm font-medium text-gray-900 sm:pl-0">{{
                      skill.frontend_name }}</td>
                    <td class="whitespace-nowrap p-4 text-sm text-black">{{ skill.backend_name }}</td>
                    <td class="whitespace-nowrap p-4 text-sm text-black">{{ skill.database_name }}</td>
                  </tr>
                  <tr v-for="skill in skills_row3" :key="skill.id" class="divide-x divide-gray">
                    <td class="whitespace-nowrap py-4 pl-4 pr-4 text-sm font-medium text-gray-900 sm:pl-0">{{
                      skill.frontend_name }}</td>
                    <td class="whitespace-nowrap p-4 text-sm text-black">{{ skill.backend_name }}</td>
                    <td class="whitespace-nowrap p-4 text-sm text-black">{{ skill.database_name }}</td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- 作品連結 -->
    <h2 class="font-semibold text-gray-900">作品集連結</h2>
    <div class="mt-6 border-t border-gray-100">
      <dl class="divide-y divide-gray-100">
        <div class="px-4 py-6 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-0">
          <dt class="mb-2 font- inline-flex">
            <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6" viewBox="0 0 24 24">
              <path
                d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v-3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z" />
            </svg>Github
          </dt>
          <a class="mt-1 text-sm leading-6 text-gray-700 sm:col-span-2 sm:mt-0 line hover:text-blue"
            href="https://github.com/peggy0418">Github</a>
        </div>
      </dl>
    </div>
    <!-- 自我介紹 -->
    <h2 class="font-semibold text-gray-900">關於我</h2>
    <div class=" border-t px-4 py-6 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-0">
      <dl class="divide-y divide-gray-100">
        <div class="px-4 py-6 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-0">
          <dd class="mt-1 text-sm leading-6 text-gray-700 sm:col-span-2 sm:mt-0">Fugiat ipsum ipsum deserunt culpa aute
            sint
            do nostrud anim incididunt cillum culpa consequat. Excepteur qui ipsum aliquip consequat sint. Sit id mollit
            nulla mollit nostrud in ea officia proident. Irure nostrud pariatur mollit ad adipisicing reprehenderit
            deserunt
            qui eu.
          </dd>
        </div>
      </dl>
    </div>
  </div>
</template>


<script setup>
import { PaperClipIcon } from '@heroicons/vue/20/solid'

const personalInfo = {
  name: "張珮綺",
  email: "test@email.com",
  phone: "0912-345-678",
  address: "台中市 龍井區",
};

const education = [
  {
    id: 1,
    degree: "學士",
    school: "國立雲林科技大學",
    year: "2019-2022",
  },
];

const experience = [
  {
    id: 1,
    position: "前端工程師-實習生",
    company: "Monosparta",
    year: "2023/7-現在",
    description: "",
  },
];
const skills_row1 =
  [
    {
      frontend_name: "html",
      backend_name: "php",
      database_name: "mysql"
    },
  ]
const skills_row2 =
  [
    {
      frontend_name: "css",
      backend_name: "node.js",
      database_name: "maria db"
    },
  ];
const skills_row3 =
  [
    {
      frontend_name: "javascript",
      backend_name: "",
      database_name: ""
    },
  ];
</script> 
