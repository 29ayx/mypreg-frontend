<script>
    import HeaderMother from "../../components/Header_Mother.svelte";
    import FooterMother from "../../components/Footer.svelte";
    import { onMount } from "svelte";

  
    let profileData = null;  // To store the profile data
    let notification = "";
  
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
        console.log(data)
  
        if (response.ok) {
          profileData = data;
          notification = "Profile loaded successfully!";
        } else {
          notification = data.message || "Failed to load profile!";
        }
      } catch (error) {
        console.log(error)
        notification = "Error connecting to the server!";
      }
    }
  
    // Call fetchProfile on component mount
    onMount(() => {
      fetchProfile();
    });
  </script>
  
  <HeaderMother />
  
  {#if profileData}
  <div class="max-w-4xl mx-auto font-[sans-serif] p-6">
    <div class="text-center mb-16">
      <h4 class="text-gray-800 text-base font-semibold mt-6">Welcome, {profileData.preffered_name}</h4>
    </div>

    <form>
      <div class="grid sm:grid-cols-2 gap-8">
        <div>
          <label class="text-gray-800 text-sm mb-2 block">Preffered Name</label>
          <input name="name" type="text" value={profileData.preffered_name} class="bg-gray-100 w-full text-gray-800 text-sm px-4 py-3.5 rounded-md focus:bg-transparent outline-blue-500 transition-all" placeholder="This will be public" />
        </div>
        <div>
          <label class="text-gray-800 text-sm mb-2 block">Email Id</label>
          <input name="lname" value={profileData.email} type="text" class="bg-gray-100 w-full text-gray-800 text-sm px-4 py-3.5 rounded-md focus:bg-transparent outline-blue-500 transition-all" placeholder="Enter last name" />
        </div>
        <div>
          <label class="text-gray-800 text-sm mb-2 block">Email Id</label>
          <input name="email" type="text" class="bg-gray-100 w-full text-gray-800 text-sm px-4 py-3.5 rounded-md focus:bg-transparent outline-blue-500 transition-all" placeholder="Enter email" />
        </div>
        <div>
          <label class="text-gray-800 text-sm mb-2 block">Mobile No.</label>
          <input name="number" value={profileData.blood_type} type="number" class="bg-gray-100 w-full text-gray-800 text-sm px-4 py-3.5 rounded-md focus:bg-transparent outline-blue-500 transition-all" placeholder="Enter mobile number" />
        </div>
        <div>
          <label class="text-gray-800 text-sm mb-2 block">Blood Type</label>
          <input name="password" type="password" class="bg-gray-100 w-full text-gray-800 text-sm px-4 py-3.5 rounded-md focus:bg-transparent outline-blue-500 transition-all" placeholder="Enter password" />
        </div>
        <div>
          <label class="text-gray-800 text-sm mb-2 block">Country</label>
          <input name="cpassword" type="password" class="bg-gray-100 w-full text-gray-800 text-sm px-4 py-3.5 rounded-md focus:bg-transparent outline-blue-500 transition-all" placeholder="Enter confirm password" />
        </div>
      </div>

      <div class="!mt-12">
        <button type="button" class="py-3.5 px-7 text-sm font-semibold tracking-wider rounded-md text-white bg-blue-600 hover:bg-blue-700 focus:outline-none">
          Sign up
        </button>
      </div>
    </form>
  </div>
  {:else}
    <p>{notification}</p>
  {/if}
  <FooterMother/>