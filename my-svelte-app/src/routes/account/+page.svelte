<script>
    import HeaderMother from "../../components/Header_Mother.svelte";
    import FooterMother from "../../components/Footer.svelte";
    import { onMount } from "svelte";
  
    let profileData = null;  // To store the profile data
    let notification = "";   // To display notifications
  
    // Function to get the cookie value
    function getCookie(name) {
      const value = `; ${document.cookie}`;
      const parts = value.split(`; ${name}=`);
      if (parts.length === 2) return parts.pop().split(';').shift();
    }
  
    // Fetch the profile data
    async function fetchProfile() {
      const email = getCookie('email');  // Get email from cookie
      const token = getCookie('token');  // Get token from cookie
  
      if (!email || !token) {
        notification = "Email or token not found in cookies!";
        return;
      }
  
      try {
        const response = await fetch(`http://localhost:8000/mother-profile?email=${email}`, {
          method: "GET",
          headers: {
            "Authorization": `Bearer ${token}`, // Send token in Authorization header
            "Content-Type": "application/json",
          },
        });
  
        const data = await response.json();
        if (response.ok) {
          profileData = data;
        } else {
          notification = data.message || "Failed to load profile!";
        }
      } catch (error) {
        notification = "Error connecting to the server!";
      }
    }
  
    // Function to update profile data (PUT request)
    async function updateProfile(event) {
      event.preventDefault(); // Prevent form default submission behavior
  
      const form = event.target; // Get form reference
      const formData = new FormData(form); // Capture form data
  
      // Convert FormData to a plain object for JSON.stringify
      const updatedData = Object.fromEntries(formData.entries());
  
      const token = getCookie('token');  // Get token from cookie
  
      try {
        const response = await fetch(`http://localhost:8000/mother-profile/${profileData.id}`, {
          method: "PUT",
          headers: {
            "Authorization": `Bearer ${token}`,
            "Content-Type": "application/json",
          },
          body: JSON.stringify(updatedData)  // Send updated form data
        });
  
        const data = await response.json();
        if (response.ok) {
          notification = "Profile updated successfully!";
          await fetchProfile();  // Reload the form with updated data
        } else {
          notification = data.message || "Failed to update profile!";
        }
      } catch (error) {
        notification = "Error updating profile!";
      }
    }
  
    // Call fetchProfile on component mount
    onMount(() => {
      fetchProfile();
    });
  </script>
  <HeaderMother />
  
  {#if profileData}
  <div class="max-w-5xl max-lg:max-w-3xl  mx-auto bg-white my-6 font-[sans-serif]">
      <h2 class="text-3xl font-extrabold text-gray-800">My Account</h2>
      <div class="flex items-center max-md:flex-col gap-6 bg-gradient-to-tr from-blue-700 to-purple-400 text-white px-6 py-3.5 rounded font-[sans-serif]">
        <p class="text-base flex-1 max-md:text-center">Don't miss out on our amazing summer sale! Get up to 50% off on a wide range of products. Make the most of your summer shopping.</p>
  
        <div>
          <button type="button" class="bg-white  text-blue-500 py-2.5 px-5 rounded text-sm">
            Get Offer
          </button>
          <svg xmlns="http://www.w3.org/2000/svg"
            class="w-3.5 cursor-pointer fill-white inline-block ml-4" viewBox="0 0 320.591 320.591">
            <path
              d="M30.391 318.583a30.37 30.37 0 0 1-21.56-7.288c-11.774-11.844-11.774-30.973 0-42.817L266.643 10.665c12.246-11.459 31.462-10.822 42.921 1.424 10.362 11.074 10.966 28.095 1.414 39.875L51.647 311.295a30.366 30.366 0 0 1-21.256 7.288z"
              data-original="#000000" />
            <path
              d="M287.9 318.583a30.37 30.37 0 0 1-21.257-8.806L8.83 51.963C-2.078 39.225-.595 20.055 12.143 9.146c11.369-9.736 28.136-9.736 39.504 0l259.331 257.813c12.243 11.462 12.876 30.679 1.414 42.922-.456.487-.927.958-1.414 1.414a30.368 30.368 0 0 1-23.078 7.288z"
              data-original="#000000" />
          </svg>
        </div>
      </div>
    <div class="grid lg:grid-cols-3 border border-pink-200 items-start gap-4 p-2 shadow-[0_2px_10px_-3px_rgba(6,81,237,0.3)] rounded-lg mt-12">

        <div class="rounded-lg p-6 h-full order-1">
          <img src="https://readymadeui.com/team-3.webp" class="w-56 h-56 rounded-full border-2 border-pink-300 p-0.5 mx-auto"/>

            <ul class="mt-16 space-y-8">
                <li class="flex items-center">
                  
                    <a href="javascript:void(0)" class="text-black text-sm text-gray-500 ml-4">
                        info@example.com
                    </a>
                </li>
                <li class="flex items-center">
                
                    <a href="javascript:void(0)" class="text-black text-sm text-gray-500 ml-4">
                        +158 996 888
                    </a>
                </li>
                <li class="flex items-center">
               
                    <a href="javascript:void(0)" class="text-black text-sm text-gray-500 ml-4">
                        123 Street 256 House
                    </a>
                </li>
            </ul>

            <ul class="flex flex-wrap gap-4 mt-16">
                <li class="bg-gray-800 hover:bg-gray-900 h-10 w-10 rounded-full flex items-center justify-center shrink-0">
                    <a href="javascript:void(0)">
                        <svg xmlns="http://www.w3.org/2000/svg" width="18px" height="18px" fill='#fff'
                            viewBox="0 0 24 24">
                            <path
                                d="M6.812 13.937H9.33v9.312c0 .414.335.75.75.75l4.007.001a.75.75 0 0 0 .75-.75v-9.312h2.387a.75.75 0 0 0 .744-.657l.498-4a.75.75 0 0 0-.744-.843h-2.885c.113-2.471-.435-3.202 1.172-3.202 1.088-.13 2.804.421 2.804-.75V.909a.75.75 0 0 0-.648-.743A26.926 26.926 0 0 0 15.071 0c-7.01 0-5.567 7.772-5.74 8.437H6.812a.75.75 0 0 0-.75.75v4c0 .414.336.75.75.75zm.75-3.999h2.518a.75.75 0 0 0 .75-.75V6.037c0-2.883 1.545-4.536 4.24-4.536.878 0 1.686.043 2.242.087v2.149c-.402.205-3.976-.884-3.976 2.697v2.755c0 .414.336.75.75.75h2.786l-.312 2.5h-2.474a.75.75 0 0 0-.75.75V22.5h-2.505v-9.312a.75.75 0 0 0-.75-.75H7.562z"
                                data-original="#000000" />
                        </svg>
                    </a>
                </li>
                <li class="bg-gray-800 hover:bg-gray-900 h-10 w-10 rounded-full flex items-center justify-center shrink-0">
                    <a href="javascript:void(0)">
                        <svg xmlns="http://www.w3.org/2000/svg" width="18px" height="18px" fill='#fff'
                            viewBox="0 0 511 512">
                            <path
                                d="M111.898 160.664H15.5c-8.285 0-15 6.719-15 15V497c0 8.285 6.715 15 15 15h96.398c8.286 0 15-6.715 15-15V175.664c0-8.281-6.714-15-15-15zM96.898 482H30.5V190.664h66.398zM63.703 0C28.852 0 .5 28.352.5 63.195c0 34.852 28.352 63.2 63.203 63.2 34.848 0 63.195-28.352 63.195-63.2C126.898 28.352 98.551 0 63.703 0zm0 96.395c-18.308 0-33.203-14.891-33.203-33.2C30.5 44.891 45.395 30 63.703 30c18.305 0 33.195 14.89 33.195 33.195 0 18.309-14.89 33.2-33.195 33.2zm289.207 62.148c-22.8 0-45.273 5.496-65.398 15.777-.684-7.652-7.11-13.656-14.942-13.656h-96.406c-8.281 0-15 6.719-15 15V497c0 8.285 6.719 15 15 15h96.406c8.285 0 15-6.715 15-15V320.266c0-22.735 18.5-41.23 41.235-41.23 22.734 0 41.226 18.495 41.226 41.23V497c0 8.285 6.719 15 15 15h96.403c8.285 0 15-6.715 15-15V302.066c0-79.14-64.383-143.523-143.524-143.523zM466.434 482h-66.399V320.266c0-39.278-31.953-71.23-71.226-71.23-39.282 0-71.239 31.952-71.239 71.23V482h-66.402V190.664h66.402v11.082c0 5.77 3.309 11.027 8.512 13.524a15.01 15.01 0 0 0 15.875-1.82c20.313-16.294 44.852-24.907 70.953-24.907 62.598 0 113.524 50.926 113.524 113.523zm0 0"
                                data-original="#000000" />
                        </svg>
                    </a>
                </li>
                <li class="bg-gray-800 hover:bg-gray-900 h-10 w-10 rounded-full flex items-center justify-center shrink-0">
                    <a href="javascript:void(0)">
                        <svg xmlns="http://www.w3.org/2000/svg" width="18px" height="18px" fill='#fff'
                            viewBox="0 0 24 24">
                            <path
                                d="M12 9.3a2.7 2.7 0 1 0 0 5.4 2.7 2.7 0 0 0 0-5.4Zm0-1.8a4.5 4.5 0 1 1 0 9 4.5 4.5 0 0 1 0-9Zm5.85-.225a1.125 1.125 0 1 1-2.25 0 1.125 1.125 0 0 1 2.25 0ZM12 4.8c-2.227 0-2.59.006-3.626.052-.706.034-1.18.128-1.618.299a2.59 2.59 0 0 0-.972.633 2.601 2.601 0 0 0-.634.972c-.17.44-.265.913-.298 1.618C4.805 9.367 4.8 9.714 4.8 12c0 2.227.006 2.59.052 3.626.034.705.128 1.18.298 1.617.153.392.333.674.632.972.303.303.585.484.972.633.445.172.918.267 1.62.3.993.047 1.34.052 3.626.052 2.227 0 2.59-.006 3.626-.052.704-.034 1.178-.128 1.617-.298.39-.152.674-.333.972-.632.304-.303.485-.585.634-.972.171-.444.266-.918.299-1.62.047-.993.052-1.34.052-3.626 0-2.227-.006-2.59-.052-3.626-.034-.704-.128-1.18-.299-1.618a2.619 2.619 0 0 0-.633-.972 2.595 2.595 0 0 0-.972-.634c-.44-.17-.914-.265-1.618-.298-.993-.047-1.34-.052-3.626-.052ZM12 3c2.445 0 2.75.009 3.71.054.958.045 1.61.195 2.185.419A4.388 4.388 0 0 1 19.49 4.51c.457.45.812.994 1.038 1.595.222.573.373 1.227.418 2.185.042.96.054 1.265.054 3.71 0 2.445-.009 2.75-.054 3.71-.045.958-.196 1.61-.419 2.185a4.395 4.395 0 0 1-1.037 1.595 4.44 4.44 0 0 1-1.595 1.038c-.573.222-1.227.373-2.185.418-.96.042-1.265.054-3.71.054-2.445 0-2.75-.009-3.71-.054-.958-.045-1.61-.196-2.185-.419A4.402 4.402 0 0 1 4.51 19.49a4.414 4.414 0 0 1-1.037-1.595c-.224-.573-.374-1.227-.419-2.185C3.012 14.75 3 14.445 3 12c0-2.445.009-2.75.054-3.71s.195-1.61.419-2.185A4.392 4.392 0 0 1 4.51 4.51c.45-.458.994-.812 1.595-1.037.574-.224 1.226-.374 2.185-.419C9.25 3.012 9.555 3 12 3Z">
                            </path>
                        </svg>
                    </a>
                </li>
            </ul>
        </div>

        <div class="p-4 lg:col-span-2 order-2">
            <p>{notification}</p>
            <form on:submit={updateProfile}>

                <div class="grid sm:grid-cols-2 gap-8">
                  <!-- Contact Information Group -->
                  <fieldset class="border border-gray-300 p-4 rounded-md mb-4">
                    <legend class="text-gray-600 px-2 text-sm font-bold">Contact Information</legend>
      
                    <div class="relative flex items-center mb-2">
                      <input name="preferred_name" type="text" class="text-gray-800 bg-white border border-gray-300 w-full text-sm px-4 py-3 rounded-md outline-blue-500"
                        placeholder="Enter preferred name" value={profileData.preffered_name} />
                    </div>
      
                    <div class="relative flex items-center mb-2">
                      <input name="email" type="text" class="text-gray-800 bg-white border border-gray-300 w-full text-sm px-4 py-3 rounded-md outline-blue-500"
                        placeholder="Enter email" disabled="true" value={profileData.email} />
                    </div>
      
                    <div class="relative flex items-center">
                      <input name="phone" type="text" class="text-gray-800 bg-white border border-gray-300 w-full text-sm px-4 py-3 rounded-md outline-blue-500"
                        placeholder="Enter phone" value={profileData.phone} />
                    </div>
                  </fieldset>
      
                  <!-- Personal Information Group -->
                  <fieldset class="border border-gray-300 p-4 rounded-md mb-4">
                    <legend class="text-gray-600 px-2 text-sm font-bold">Personal Information</legend>
      
                    <div class="relative flex items-center mb-2">
                      <input name="date_of_birth" type="date" class="text-gray-800 bg-white border border-gray-300 w-full text-sm px-4 py-3 rounded-md outline-blue-500"
                        placeholder="Enter date of birth" value={profileData.date_of_birth} />
                    </div>
      
                    <div class="relative flex items-center">
                      <input name="blood_type" type="text" class="text-gray-800 bg-white border border-gray-300 w-full text-sm px-4 py-3 rounded-md outline-blue-500"
                        placeholder="Enter blood type" value={profileData.blood_type} />
                    </div>
                  </fieldset>
      
                  <!-- Address Group -->
                  <fieldset class="border border-gray-300 p-4 rounded-md mb-4">
                    <legend class="text-gray-600 px-2 text-sm font-bold">Address</legend>
      
                    <div class="relative flex items-center mb-2">
                      <input name="street" type="text" class="text-gray-800 bg-white border border-gray-300 w-full text-sm px-4 py-3 rounded-md outline-blue-500"
                        placeholder="Enter street" value={profileData.street} />
                    </div>
      
                    <div class="relative flex items-center mb-2">
                      <input name="city" type="text" class="text-gray-800 bg-white border border-gray-300 w-full text-sm px-4 py-3 rounded-md outline-blue-500"
                        placeholder="Enter city" value={profileData.city} />
                    </div>
      
                    <div class="relative flex items-center mb-2">
                      <input name="state" type="text" class="text-gray-800 bg-white border border-gray-300 w-full text-sm px-4 py-3 rounded-md outline-blue-500"
                        placeholder="Enter state" value={profileData.state} />
                    </div>
      
                    <div class="relative flex items-center">
                      <input name="country" type="text" class="text-gray-800 bg-white border border-gray-300 w-full text-sm px-4 py-3 rounded-md outline-blue-500"
                        placeholder="Enter country" value={profileData.country} />
                    </div>
                  </fieldset>
      
                  <!-- Allergy Group -->
                  <fieldset class="border border-gray-300 p-4 rounded-md mb-4">
                    <legend class="text-gray-600 px-2 text-sm font-bold">Allergies</legend>
      
                    <div class="relative flex items-center mb-2">
                      <input name="penicillin" type="text" class="text-gray-800 bg-white border border-gray-300 w-full text-sm px-4 py-3 rounded-md outline-blue-500"
                        placeholder="Penicillin allergy" value={profileData.penicillin} />
                    </div>
      
                    <div class="relative flex items-center mb-2">
                      <input name="eggs" type="text" class="text-gray-800 bg-white border border-gray-300 w-full text-sm px-4 py-3 rounded-md outline-blue-500"
                        placeholder="Eggs allergy" value={profileData.eggs} />
                    </div>
      
                    <div class="relative flex items-center">
                      <input name="dust_mites" type="text" class="text-gray-800 bg-white border border-gray-300 w-full text-sm px-4 py-3 rounded-md outline-blue-500"
                        placeholder="Dust mites allergy" value={profileData.dust_mites} />
                    </div>
                  </fieldset>
                </div>
      
                <button type="submit" class="mt-12 flex items-center justify-center text-sm lg:ml-auto max-lg:w-full rounded-lg px-4 py-3 tracking-wide text-white bg-blue-600 hover:bg-blue-700">
                    Update Information
                  </button>
              </form>
        </div>
    </div>
</div>
  {:else}
    <p>{notification}</p>
  {/if}
  <FooterMother/>