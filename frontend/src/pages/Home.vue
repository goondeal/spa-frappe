<template>
  <div class="w-full h-full bg-white flex flex-col">
    <div class="text-2xl w-full text-white text-center px-12 py-6 bg-blue-600 flex justify-between items-center">
      Branch / Store / Cashier
      <div class="flex content-center items-center">
        <button class="text-white w-8 h-8 mx-4" @click="addBranch">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="#fff">
            <path fill-rule="evenodd"
              d="M12 2.25c-5.385 0-9.75 4.365-9.75 9.75s4.365 9.75 9.75 9.75 9.75-4.365 9.75-9.75S17.385 2.25 12 2.25ZM12.75 9a.75.75 0 0 0-1.5 0v2.25H9a.75.75 0 0 0 0 1.5h2.25V15a.75.75 0 0 0 1.5 0v-2.25H15a.75.75 0 0 0 0-1.5h-2.25V9Z"
              clip-rule="evenodd" />
          </svg>
        </button>
        <button class="text-white w-8 h-8" @click="saveBranch">
          <svg viewBox="0 0 30 30" xmlns="http://www.w3.org/2000/svg" fill="#fff">
            <path
              d="M22,4h-2v6c0,0.552-0.448,1-1,1h-9c-0.552,0-1-0.448-1-1V4H6C4.895,4,4,4.895,4,6v18c0,1.105,0.895,2,2,2h18  c1.105,0,2-0.895,2-2V8L22,4z M22,24H8v-6c0-1.105,0.895-2,2-2h10c1.105,0,2,0.895,2,2V24z" />
            <rect height="5" width="2" x="16" y="4" />
          </svg>
        </button>
      </div>
    </div>
    <div v-if="branches.data?.length" class="flex-1 m-8">
      <form class="">
        <div class="flex flex-wrap items-center justify-between">
          <FormControl
            class="m-4 sm:w-full md:w-auto md:flex-grow"
            :type="'text'"
            label="Branch"
            size="md"
            variant="outline"
            placeholder=""
            :disabled="true"
            v-model="branch.name"
          />
          <FormControl
          class="m-4 sm:w-full md:w-auto md:flex-grow"
            :type="'number'"
            label="Custom No"
            size="md"
            variant="outline"
            placeholder=""
            :disabled="false"
            v-model="branch.custom_no"
          />
        </div>
        <div class="flex flex-wrap items-center justify-between">
          <FormControl
          class="m-4 sm:w-full md:w-auto md:flex-grow"
            :type="'text'"
            label="Arabic Name"
            size="md"
            variant="outline"
            placeholder=""
            :disabled="false"
            v-model="branch.arabic_name"
          />
          <FormControl
          class="m-4 sm:w-full md:w-auto md:flex-grow"
            :type="'text'"
            label="Arabic Description"
            size="md"
            variant="outline"
            placeholder=""
            :disabled="false"
            v-model="branch.arabic_description"
          />
        </div>
        <div class="flex flex-wrap items-center justify-between">
          <FormControl
          class="m-4 sm:w-full md:w-auto md:flex-grow"
            :type="'text'"
            label="English Name"
            size="md"
            variant="outline"
            placeholder=""
            :disabled="false"
            v-model="branch.english_name"
          />
          <FormControl
          class="m-4 sm:w-full md:w-auto md:flex-grow"
            :type="'text'"
            label="English Description"
            size="md"
            variant="outline"
            placeholder=""
            :disabled="false"
            v-model="branch.english_description"
          />
        </div>
        <div class="flex flex-wrap items-center justify-between">
          <FormControl
          class="m-4 sm:w-full md:w-auto md:flex-grow"
            :type="'textarea'"
            label="Notes"
            size="lg"
            variant="outline"
            placeholder=""
            :disabled="false"
            v-model="branch.notes"
          />
          <FormControl
          class="m-4 sm:w-full md:w-auto md:flex-grow"
            :type="'textarea'"
            label="Address"
            size="lg"
            variant="outline"
            placeholder=""
            :disabled="false"
            v-model="branch.address"
          />
        </div>
      </form>
    </div>
    <div v-else class="text-center text-3xl h-1/2 m-8">
      No branches yet
    </div>
    <div class="text-black p-4 flex items-center justify-center">
      <!-- First -->
      <button @click="navBranch(0)" :disabled="getPrevBranchesCount() - 1 <= 0" :class="getPrevBranchesCount() - 1 > 0 ? 'text-black' : 'text-gray-400'" class="mx-4">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"
          class="w-6 h-6">
          <path stroke-linecap="round" stroke-linejoin="round" d="m18.75 4.5-7.5 7.5 7.5 7.5m-6-15L5.25 12l7.5 7.5" />
        </svg>
      </button>
      <!-- Prev -->
      <button @click="navBranch(selectedIndex - 1)" :disabled="getPrevBranchesCount() - 1 <= 0" :class="getPrevBranchesCount() - 1 > 0 ? 'text-black' : 'text-gray-400'">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"
          class="w-6 h-6">
          <path stroke-linecap="round" stroke-linejoin="round" d="M15.75 19.5 8.25 12l7.5-7.5" />
        </svg>
      </button>
      <!-- Count -->
      <span class="mx-8"> {{branches.data && branches.data.length > 0 ? getPrevBranchesCount() : 0}} / {{branches.data?.length || 0}}</span>
      <!-- Next -->
      <button @click="navBranch(selectedIndex + 1)" class="mx-4" :disabled="getNextBranchesCount() <= 0" :class="getNextBranchesCount() > 0 ? 'text-black' : 'text-gray-400'">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"
          class="w-6 h-6">
          <path stroke-linecap="round" stroke-linejoin="round" d="m8.25 4.5 7.5 7.5-7.5 7.5" />
        </svg>
      </button>
      <!-- Last -->
      <button @click="navBranch(branches.data.length - 1)" :disabled="getNextBranchesCount() <= 0" :class="getNextBranchesCount() > 0 ? 'text-black' : 'text-gray-400'">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"
          class="w-6 h-6">
          <path stroke-linecap="round" stroke-linejoin="round" d="m5.25 4.5 7.5 7.5-7.5 7.5m6-15 7.5 7.5-7.5 7.5" />
        </svg>
      </button>
    </div>
  </div>
</template>
<script setup>
import { ref, watch } from 'vue'
import { FormControl, createListResource } from 'frappe-ui'
// import { session } from '../data/session'

const selectedIndex = ref(0)
const branch = ref(
  {
    name: '',
    customNO: '',
    arabicName: '',
    arabicDescription: '',
    englishName: '',
    englishDescription: '',
    address: '',
    notes: '',
})


const branches = createListResource({
  // url: '/api/branches',
  doctype: 'MyBranch',
  fields: [
    "name",
    "custom_no",
    "arabic_name",
    "arabic_description",
    "english_name",
    "english_description",
    "notes",
    "address"
  ],
  onError(error) {
    console.log('branches fetch error', error)
  },
  onSuccess(data) {
    console.log('branches', data)
    branch.value = {...(branches.data[selectedIndex.value])}
    console.log('branch', branch.value)
    console.log('branches.data.length', branches.data.length)
  },
  // auto: true,
})

branches.reload()

// Navigation
const getPrevBranchesCount = () => {
  if (branches.data) {
    return selectedIndex.value + 1
  }
  return 0
}

const getNextBranchesCount = () => {
  if (branches.data) {
    return branches.data.length - getPrevBranchesCount()
  }
  return 0
}

// Nav Branches
const navBranch = (index) => {
  if (index >= 0 && branches.data && index < branches.data.length) {
    selectedIndex.value = index
  }
}

// Add Branch
const addBranch = () => {
  console.log('Adding New Branch')
  branches.insert.submit({})
  branches.reload()
  selectedIndex.value = branches.data.length
  console.log('selectedIndex', selectedIndex.value)
  console.log('branches.data.length', branches.data.length)
}

// Save Branch
const saveBranch = () => {
  console.log('Saving Branch', branch.name)
  // const {name, ...newBranchData} = branch.value
  // console.log('newBranchData', newBranchData)
  branches.setValue.submit(branch.value)
}

// watchers
watch(selectedIndex, (index) => {
  if (branches.data) {
    branch.value = {...branches.data[index]}
  }
})
</script>
