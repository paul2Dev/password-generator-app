<script setup>
import { ref } from 'vue'
import { useClipboard, usePermission } from '@vueuse/core'

const { text, isSupported, copy, copied } = useClipboard()
const permissionRead = usePermission('clipboard-read')
const permissionWrite = usePermission('clipboard-write')

const password = ref('')
const passwordLength = 16
const chars = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789!@#$%^&*()_+{}:<>?[]'


const generatePassword = () => {
  let generatedPassword = ''
  for(let i=0; i<passwordLength; i++) {
    generatedPassword += chars.charAt(Math.floor(Math.random() * chars.length))
  }
  password.value = generatedPassword
}

</script>

<template>
  <div class="container mx-auto h-screen flex items-center justify-center">
    <div class="flex flex-col bg-slate-800 text-green-500 p-10">
      <div class="text-center text-xl mb-2">
        <h1>Password Generator</h1>
      </div>
      <div class="flex">
        <div class="p-2 flex bg-white rounded-lg">
          <input class="text-slate-800 text-center  mr-2 focus:outline-none focus:ring-1 focus:ring-green-500" type="text" v-model="password" autofocus>
          <div class=" bg-white">
            <svg v-if='!copied' class="w-6 h-6 cursor-pointer" @click="copy(password)" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path d="M8 3a1 1 0 011-1h2a1 1 0 110 2H9a1 1 0 01-1-1z"></path><path d="M6 3a2 2 0 00-2 2v11a2 2 0 002 2h8a2 2 0 002-2V5a2 2 0 00-2-2 3 3 0 01-3 3H9a3 3 0 01-3-3z"></path></svg>
            <svg v-else class="w-6 h-6 text-white cursor-pointer" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path d="M8 3a1 1 0 011-1h2a1 1 0 110 2H9a1 1 0 01-1-1z"></path><path d="M6 3a2 2 0 00-2 2v11a2 2 0 002 2h8a2 2 0 002-2V5a2 2 0 00-2-2 3 3 0 01-3 3H9a3 3 0 01-3-3z"></path></svg>
          </div>
        </div>
        <div class="p-2">
          <svg class="w-6 h-6 cursor-pointer" @click="generatePassword" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M4 2a1 1 0 011 1v2.101a7.002 7.002 0 0111.601 2.566 1 1 0 11-1.885.666A5.002 5.002 0 005.999 7H9a1 1 0 010 2H4a1 1 0 01-1-1V3a1 1 0 011-1zm.008 9.057a1 1 0 011.276.61A5.002 5.002 0 0014.001 13H11a1 1 0 110-2h5a1 1 0 011 1v5a1 1 0 11-2 0v-2.101a7.002 7.002 0 01-11.601-2.566 1 1 0 01.61-1.276z" clip-rule="evenodd"></path></svg>
        </div>
      </div>
    </div>
  </div>
</template>

