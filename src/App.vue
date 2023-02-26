<script setup>
  import { ref } from 'vue'
  import axios from 'axios'
  
  const username = ref('')
  let profilePicture = ref('')

  const generatePicture = async () => {
    try {
      const res = await axios.get('https://robohash.org/' + username.value + '?set=any')
      profilePicture.value = res.request.responseURL
    } catch (err) {
      throw err
    }
  }
</script>

<template>

  <div class="w-full md:max-w-sm">
    <form @submit.prevent="generatePicture">
      <input v-model="username" type="text" class="form-input w-full rounded border-gray-400" placeholder="Ketik nama Anda...">
      <div class="flex justify-center mt-5">
        <button type="submit" class="bg-green-600 text-white rounded px-5 py-2.5">
          Buat Profile Picture!
        </button>
      </div>
    </form>
    <div class="flex justify-center mt-7">
      <div v-show="profilePicture" class="w-48 h-48 flex justify-center items-center bg-white rounded-full overflow-hidden border-2 border-white ring-2 ring-gray-300">
        <img :src="profilePicture" alt="Profile picture" class="w-full aspect-square object-contain">
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>
