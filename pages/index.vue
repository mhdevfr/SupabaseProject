<template>
    <div class="h-screen w-screen flex justify-evenly" id="main">
      <div class=" h-full flex flex-col justify-center">
        <h1 class="text-xl text-start"><span class="bg-red-400 w-32 rounded-sm">🪫</span> unauthenticated</h1>
        <h1 class="text-7xl text-start mt-4">Build your</h1>
        <h1 class="text-7xl text-start my-2">component by AI</h1>
        <p class="w-96 my-4">Make your own component with any CSS framework, UI/UX in few seconds with some words..</p>
        <div class="flex w-96">
          <nuxt-link to="/login" class="p-2 w-32 bg-blue-900 text-white rounded-xl mr-4 text-center">Login</nuxt-link>
          <nuxt-link to="/signUp" class="w-32 p-2 bg-gray-200 rounded-xl border-dotted border-2 text-center border-gray-400">Sign up</nuxt-link>
        </div>
      </div>
      <div class="flex justify-center items-center" id="xcomponent">
        <exampleComponent id="inc"/>
        </div>
    </div>
</template>

<style scoped>

#main{
    background-color: black;
    opacity: 1;
    background-image: radial-gradient(#444cf7 0.5px, #e5e5f7 0.5px);
    background-size: 10px 10px;
}
#xcomponent{
  perspective: 1000px;
}

#inc{
  transform: rotateX(360deg) rotateY(328deg);
  transform-style: preserve-3d;
}

</style>

<script setup lang="ts">
import useSupabaseAuthClient from '@nuxtjs/supabase';

const client = useSupabaseAuthClient()
const user = useSupabaseUser()
const loading = ref(false)

const logout = async () => {
  loading.value = true
  const { error } = await client.auth.signOut()
  if (error) {
    loading.value = false
    return alert('Something went wrong !')
  }
}

useHead({
  title: 'supaAuth',
  meta: [
    { name: 'description', content: 'Authentication template with email and password, using Supabase. If you want to a quick start to your next Nuxt3 app, please feel free to use this template.' }
  ]
})



</script>