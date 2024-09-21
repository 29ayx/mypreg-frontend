<script>

  import {goto} from "$app/navigation";
      // Import the goto function
  
    let firstname = "";
    let lastname = "";
    let role = "pregnant";
    let email = "";
    let password = "";
    let notification = "";
    let phoneno = "";
    let isDropdownOpen = false;
  
    async function handleRegister() {
      const body = { firstname, lastname, role, email, password };
  
      try {
        const response = await fetch("http://localhost:8000/register", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify(body),
        });
  
        const data = await response.json();
        if (response.ok) {

          notification = "Registration successful!";
          // Redirect to /login after successful registration
          goto("/login")
          
        } else {
          notification = data.error;
        }
      } catch (error) {
        notification = "Error connecting to the server!";
      }
    }
  
    function toggleDropdown() {
      isDropdownOpen = !isDropdownOpen;
    }
  
    function selectRole(selectedRole) {
      role = selectedRole;
      isDropdownOpen = false;
    }
  </script>
  <div class="font-[sans-serif]">
    <div class="grid lg:grid-cols-3 md:grid-cols-2 items-center gap-4 h-full">
      <div class="max-md:order-1 lg:col-span-2 md:h-screen w-full bg-[#000842] md:rounded-tr-xl md:rounded-br-xl">
        <img src="/login_bg.jpeg" class="w-full h-full object-cover mx-auto hidden sm:block" alt="login-image" />
      </div>

    

      <div class="w-full p-6">
       
  <form on:submit|preventDefault={handleRegister} >
    <div class="mb-8 text-center">
      <h3 class="text-gray-800 text-3xl font-thin">Create an account</h3>
      <p class="text-sm mt-4 text-gray-800">Already have an account <a href="/login" class="text-blue-600 font-semibold hover:underline ml-1 whitespace-nowrap">Login here</a></p>
      <p>{notification}</p>
    </div>


    <div class="grid gap-6">
      <div>

        <input name="name" type="text" required bind:value={firstname} class="bg-gray-100 w-full text-gray-800 text-sm px-4 py-3 rounded-md outline-blue-500" placeholder="Enter name" />
      </div>
      <div>

        <input name="lname" type="text" required bind:value={lastname} class="bg-gray-100 w-full text-gray-800 text-sm px-4 py-3 rounded-md outline-blue-500" placeholder="Enter last name" />
      </div>
      <div>

        <input name="email" type="text" required bind:value={email} class="bg-gray-100 w-full text-gray-800 text-sm px-4 py-3 rounded-md outline-blue-500" placeholder="Enter email" />
      </div>
      <div>

        <input name="number" type="phone" required bind:value={phoneno} class="bg-gray-100 w-full text-gray-800 text-sm px-4 py-3 rounded-md outline-blue-500" placeholder="Enter mobile number" />
      </div>
      <div>

        <input name="password" type="password" required bind:value={password} class="bg-gray-100 w-full text-gray-800 text-sm px-4 py-3 rounded-md outline-blue-500" placeholder="Enter password" />
      </div>
      <div>
        <div class="mt-1">
          <label class="text-gray-800 text-xs block mb-2">Account Role</label>
          <div class="relative">
            <button type="button" class="px-10 py-2.5 rounded text-white text-sm font-semibold border-none outline-none bg-blue-600 hover:bg-blue-700 active:bg-blue-600" on:click={toggleDropdown}>
              {role}
              <svg xmlns="http://www.w3.org/2000/svg" class="w-3 fill-white inline ml-3" viewBox="0 0 24 24">
                <path fill-rule="evenodd" d="M11.99997 18.1669a2.38 2.38 0 0 1-1.68266-.69733l-9.52-9.52a2.38 2.38 0 1 1 3.36532-3.36532l7.83734 7.83734 7.83734-7.83734a2.38 2.38 0 1 1 3.36532 3.36532l-9.52 9.52a2.38 2.38 0 0 1-1.68266.69734z" clip-rule="evenodd" />
              </svg>
            </button>
            {#if isDropdownOpen}
              <ul class="absolute block shadow-lg bg-white py-2 z-[1000] min-w-full w-max rounded max-h-96 overflow-auto">
                <li class='py-2.5 px-5 hover:bg-blue-50 text-black text-sm cursor-pointer' on:click={() => selectRole("pregnant")}>Pregnant</li>
                <li class='py-2.5 px-5 hover:bg-blue-50 text-black text-sm cursor-pointer' on:click={() => selectRole("doctor")}>Doctor</li>
              </ul>
            {/if}
          </div>
        </div>
        
      </div>
    </div>

    <div class="flex items-center mt-6">
      <input id="remember-me" name="remember-me" type="checkbox" required class="h-4 w-4 shrink-0 rounded" />
      <label for="remember-me" class="ml-3 block text-sm">
        I accept the <a href="javascript:void(0);" class="text-blue-500 font-semibold hover:underline ml-1">Terms and Conditions</a>
      </label>
    </div>

    <div class="mt-6">
      <button type="submit" class="py-3 px-4 w-full text-sm tracking-wide font-semibold rounded-md text-black bg-gradient-to-r  from-pink-300 to-pink-100 hover:bg-blue-700 focus:outline-none transition-all">
        Sign up
      </button>
    </div>
    
  </form>
      </div>
    </div>
  </div>


