<template>
    <div class="relative inset-0 w-full bg-black"> 
      <div class="min-w-full min-h-screen  flex items-center justify-center">
        <div class="h-1/2 min-w-full flex items-center justify-center">
          <form @submit.prevent="submitForm" class="h-96  flex w-3/4 bg-black bg-[linear-gradient(to_right,#E1E1E112_1px,transparent_1px),linear-gradient(to_bottom,#E1E1E112_1px,transparent_1px)] bg-[size:24px_24px] rounded-md bg-clip-padding backdrop-filter backdrop-blur-md bg-opacity-10 border border-gray-100" v-motion-slide-visible-top> 
            <div class="w-1/2 h-full flex rounded-md">
                <div class="bg-green-300 flex h-full w-16 rounded-md">
                  <button class="text-black bg-green-400 w-full rounded-md items-center flex flex-col justify-center" @click="loginWithGitHub">OAuth GitHub<img src="../images/icons8-github-50.png" class="w-10 h-10"></button>
                </div>
                <div class="w-full text-white flex flex-col items-center">
                  <h1 class="text-3xl my-12 text-center">Build your component</h1>
                  <h1 class=" text-xl w-64"><cite>"Chaque composant est essentiel dans un site il ne faut jamais les négligés surtout en tant qu'utilisateur l'UI/UX n'a jamais été aussi important qu'en 2024."</cite></h1>
                </div>
            </div>
            <div class="flex flex-col justify-center items-center w-1/2">
              <h1 class="text-white text-3xl text-center my-4">Login</h1>
              <input type="email" class="w-96 h-10 my-4 text-center rounded-xl" placeholder="youremail">
              <input type="password" class="w-96 h-10 my-4 text-center rounded-xl" placeholder="mypassword">
              <h2 ref="monRetour"></h2>
              <input type="submit" class="w-48 bg-green-400 h-8 mt-8 rounded-sm hover:bg-green-400" value="Login"> 
            </div>
          </form>
        </div>
      </div>
    </div>
  </template>
  
  <script setup lang="ts">
  import { SupabaseClient } from '@supabase/supabase-js';
  import { createClient } from '@supabase/supabase-js'
  import { ref } from 'vue';
  const supabase = createClient('https://hribmixdrzamlausyjsi.supabase.co','eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImhyaWJtaXhkcnphbWxhdXN5anNpIiwicm9sZSI6ImFub24iLCJpYXQiOjE3MTM2MjE2NDEsImV4cCI6MjAyOTE5NzY0MX0.NxEB38nmsvf27pyYOIBZ90E0EDEgh9DaF4tIe0EA2FI')
  
  let monRetour = ref('')
  let email = '';
  let password = '';
  
  async function submitForm() {
    try {
      const { data, error } = await supabase.auth.signInWithPassword({
        email,
        password,
      });
      if (error) {
        monRetour.value.style.color = 'red';
        monRetour.value.innerText = "Logins invalides.";
        throw error;
      } else {
        monRetour.value.innerText = "Bravo, vous êtes bien connecté.";
      }
      } catch (error) {
      console.error('erreur : ', error);
      }
  }
  async function loginWithGitHub() {
    const { data, error } = await supabase.auth.signInWithOAuth({
      provider: 'github',
    })
  }
  </script>
  