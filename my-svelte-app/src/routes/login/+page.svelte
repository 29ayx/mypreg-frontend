<script>
    import { onMount } from "svelte";
    import Footer from "../../components/Footer.svelte";
    import {goto} from "$app/navigation"


    let email = "";
    let password = "";
    let notification = "";

    let loginSuccessful = false;
  
    async function handleLogin() {
      const body = { email, password };
  
      try {
        const response = await fetch("http://localhost:8000/login", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify(body),
        });
  
        const data = await response.json();
  
        if (response.ok) {
          document.cookie = `email=${email}; path=/;`;
          document.cookie = `token=${data.token}; path=/;`;
          notification = "Login successful!";
          loginSuccessful = true
          if(data.role == "doctor"){

            setTimeout(() => goto('/doctorboard'), 2000);

          }
          if(data.role == "pregnant"){
            setTimeout(() => goto('/account'), 2000);

          }
        } else {
          notification = data.error;
        }
      } catch (error) {
        notification = "Error connecting to the server!";
      }
    }
  </script>
  <div class="font-[sans-serif]">
    <div class="grid lg:grid-cols-3 md:grid-cols-2 items-center gap-6 h-full">
      <div class="max-md:order-1 lg:col-span-2 md:h-screen w-full bg-[#000842] md:rounded-tr-xl md:rounded-br-xl">
        <img src="/login_bg.jpeg" class="w-full h-full object-cover block mx-auto" alt="login-image" />
      </div>

    
      {#if !loginSuccessful}
      <div class="w-full p-6">
        <form on:submit|preventDefault={handleLogin}>
          <div class="mb-8 text-center">
            <h3 class="text-gray-800 text-3xl font-thin">Sign in to account</h3>
            <p class="text-sm mt-4 text-gray-800">Don't have an account <a href="/register" class="text-blue-600 font-semibold hover:underline ml-1 whitespace-nowrap">Register here</a></p>
            <p>{notification}</p>
          </div>

          <div>

            <div class="relative mb-8 flex items-center">
              <input name="email" type="text" bind:value={email} required class="w-full text-sm text-gray-800 bg-gray-100 focus:bg-transparent px-4 py-3.5 rounded-md outline-blue-600" placeholder="Enter email" />
              <svg xmlns="http://www.w3.org/2000/svg" fill="#bbb" stroke="#bbb" class="w-[18px] h-[18px] absolute right-4" viewBox="0 0 682.667 682.667">
                <defs>
                  <clipPath id="a" clipPathUnits="userSpaceOnUse">
                    <path d="M0 512h512V0H0Z" data-original="#000000"></path>
                  </clipPath>
                </defs>
                <g clip-path="url(#a)" transform="matrix(1.33 0 0 -1.33 0 682.667)">
                  <path fill="none" stroke-miterlimit="10" stroke-width="40" d="M452 444H60c-22.091 0-40-17.909-40-40v-39.446l212.127-157.782c14.17-10.54 33.576-10.54 47.746 0L492 364.554V404c0 22.091-17.909 40-40 40Z" data-original="#000000"></path>
                  <path d="M472 274.9V107.999c0-11.027-8.972-20-20-20H60c-11.028 0-20 8.973-20 20V274.9L0 304.652V107.999c0-33.084 26.916-60 60-60h392c33.084 0 60 26.916 60 60v196.653Z" data-original="#000000"></path>
                </g>
              </svg>
            </div>
          </div>

          <div class="mt-4">

            <div class="relative flex items-center">
              <input name="password"  type="password" bind:value={password} required class="w-full text-sm text-gray-800 bg-gray-100 focus:bg-transparent px-4 py-3.5 rounded-md outline-blue-600" placeholder="Enter password" />
              <svg xmlns="http://www.w3.org/2000/svg" fill="#bbb" stroke="#bbb" class="w-[18px] h-[18px] absolute right-4 cursor-pointer" viewBox="0 0 128 128">
                <path d="M64 104C22.127 104 1.367 67.496.504 65.943a4 4 0 0 1 0-3.887C1.367 60.504 22.127 24 64 24s62.633 36.504 63.496 38.057a4 4 0 0 1 0 3.887C126.633 67.496 105.873 104 64 104zM8.707 63.994C13.465 71.205 32.146 96 64 96c31.955 0 50.553-24.775 55.293-31.994C114.535 56.795 95.854 32 64 32 32.045 32 13.447 56.775 8.707 63.994zM64 88c-13.234 0-24-10.766-24-24s10.766-24 24-24 24 10.766 24 24-10.766 24-24 24zm0-40c-8.822 0-16 7.178-16 16s7.178 16 16 16 16-7.178 16-16-7.178-16-16-16z" data-original="#000000"></path>
              </svg>
            </div>
          </div>

          <div class="flex flex-wrap items-center justify-between gap-4 mt-4">
            <div class="flex items-center">
              <input id="remember-me" name="remember-me" type="checkbox" class="h-4 w-4 shrink-0 text-blue-600 focus:ring-blue-500 border-gray-300 rounded-md" />
              <label for="remember-me" class="ml-3 block text-sm">
                Remember me
              </label>
            </div>
            <div>
              <a href="/forgotpassword" class="text-blue-600 font-semibold text-sm hover:underline">
                Forgot Password?
              </a>
            </div>
          </div>
          <div class="mt-6">
            <button type="submit" class="py-3 px-4 w-full text-sm tracking-wide font-semibold rounded-md text-black bg-gradient-to-r  from-pink-300 to-pink-100 hover:bg-blue-700 focus:outline-none transition-all">
              Sign In
            </button>
          </div>



        </form>
      </div>
      {/if}


      {#if loginSuccessful}
      <div class="w-full p-6 flex flex-col items-center justify-center">
        <img src="/Assets/animatedicons/s3.gif" class="max-h-48" alt="">
        <p class="text-gray-800 text-3xl font-thin">Login Successful</p>
        <p class="text-gray-800 mt-5 font-thin">Redirecting....</p>
      </div>
      
      {/if}
    </div>
  </div>

  <Footer/>