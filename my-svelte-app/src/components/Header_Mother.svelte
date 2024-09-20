<script>
  import {goto} from "$app/navigation"
    let isMenuOpen = false;
  
    function toggleMenu() {
      isMenuOpen = !isMenuOpen;
    }

     // Function to clear all cookies
  function clearAllCookies() {
    const cookies = document.cookie.split("; ");
    for (let cookie of cookies) {
      const cookieName = cookie.split("=")[0];
      document.cookie = `${cookieName}=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/;`;
    }



    goto("/")
  }

  function gotoExplore(){
    goto('/explore')
  }
  function gotoConsultation(){
    goto('/consultation')
  }
  function gotoResources(){
    goto('/resources')
  }
  function gotoJournal(){
    goto('/journal')
  }
  function gotoForums(){
    goto('/forums')
  }
  function gotoFitness(){
    goto('/fitness')
  }
  function gotoAccount(){
    goto('/account')
  }
  

  </script>
  
  <header class='flex border-b mt-5 border-1 bg-white font-sans min-h-[70px] tracking-wide relative z-50'>
    <div class='w-full flex flex-wrap items-center justify-center gap-6 px-10 py-3 relative'>
      <!-- <a href="javascript:void(0)">
        <img src="https://readymadeui.com/readymadeui.svg" alt="logo" class='w-36' />
      </a> -->
  
      <div class:!block={isMenuOpen} id="collapseMenu"
        class='max-lg:hidden lg:!block max-lg:before:fixed max-lg:before:bg-black max-lg:before:opacity-40 max-lg:before:inset-0 max-lg:before:z-50'>
        <button on:click={toggleMenu} id="toggleClose" class='lg:hidden fixed top-2 right-4 z-[100] rounded-full bg-white p-3'>
          <svg xmlns="http://www.w3.org/2000/svg" class="w-4 fill-black" viewBox="0 0 320.591 320.591">
            <path
              d="M30.391 318.583a30.37 30.37 0 0 1-21.56-7.288c-11.774-11.844-11.774-30.973 0-42.817L266.643 10.665c12.246-11.459 31.462-10.822 42.921 1.424 10.362 11.074 10.966 28.095 1.414 39.875L51.647 311.295a30.366 30.366 0 0 1-21.256 7.288z"
              data-original="#000000"></path>
            <path
              d="M287.9 318.583a30.37 30.37 0 0 1-21.257-8.806L8.83 51.963C-2.078 39.225-.595 20.055 12.143 9.146c11.369-9.736 28.136-9.736 39.504 0l259.331 257.813c12.243 11.462 12.876 30.679 1.414 42.922-.456.487-.927.958-1.414 1.414a30.368 30.368 0 0 1-23.078 7.288z"
              data-original="#000000"></path>
          </svg>
        </button>
  
        <ul class='lg:flex lg:ml-10 lg:gap-x-10 max-lg:space-y-3 max-lg:fixed max-lg:bg-white max-lg:w-2/3 max-lg:min-w-[300px] max-lg:top-0 max-lg:left-0 max-lg:p-4 max-lg:h-full max-lg:shadow-md max-lg:overflow-auto z-50'>
          <li class='max-lg:border-b max-lg:pb-4 px-3 lg:hidden'>
            <a href="javascript:void(0)">
              <img src="https://readymadeui.com/readymadeui.svg" alt="logo" class='w-36' />
            </a>
          </li>
          <li class='max-lg:border-b max-lg:px-3 max-lg:py-2'><a on:click={gotoExplore} href='javascript:void(0)' class='hover:text-[#007bff] text-[#007bff] font-bold text-sm block'>Explore</a></li>
          <li class='max-lg:border-b max-lg:px-3 max-lg:py-2'><a on:click={gotoConsultation} href='javascript:void(0)' class='hover:text-[#007bff] text-[#007bff] font-bold text-sm block'>Consultation</a></li>
          <li class='max-lg:border-b max-lg:px-3 max-lg:py-2'><a on:click={gotoResources} href='javascript:void(0)' class='hover:text-[#007bff] text-[#007bff] font-bold text-sm block'>Resources</a></li>
          <li class='max-lg:border-b max-lg:px-3 max-lg:py-2'><a on:click={gotoJournal} href='javascript:void(0)' class='hover:text-[#007bff] text-[#007bff] font-bold text-sm block'>Journal</a></li>
          <li class='max-lg:border-b max-lg:px-3 max-lg:py-2'><a on:click={gotoForums} href='javascript:void(0)' class='hover:text-[#007bff] text-[#007bff] font-bold text-sm block'>Forums</a></li>
          <li class='max-lg:border-b max-lg:px-3 max-lg:py-2'><a on:click={gotoFitness} href='javascript:void(0)' class='hover:text-[#007bff] text-[#007bff] font-bold text-sm block'>Fitness</a></li>
          <li class='max-lg:border-b max-lg:px-3 max-lg:py-2'><a on:click={gotoAccount} class='hover:text-[#007bff] text-[#007bff] font-bold text-sm block'>Account</a></li>
          <!-- <li class='group text-[14px] max-lg:border-b max-lg:px-3 max-lg:py-2 relative'>
            <a href='javascript:void(0)' class='hover:text-[#007bff] hover:fill-[#007bff] text-gray-500 font-bold text-[15px] block'>
              Agencies
              <svg xmlns="http://www.w3.org/2000/svg" width="16px" height="16px" class="ml-1 inline-block" viewBox="0 0 24 24">
                <path d="M12 16a1 1 0 0 1-.71-.29l-6-6a1 1 0 0 1 1.42-1.42l5.29 5.3 5.29-5.29a1 1 0 0 1 1.41 1.41l-6 6a1 1 0 0 1-.7.29z" />
              </svg>
            </a>
            <div class='absolute lg:top-5 max-lg:top-8 -left-6 z-50 flex shadow-lg bg-white max-h-0 overflow-hidden group-hover:opacity-100 group-hover:max-h-[700px] px-8 group-hover:pb-8 group-hover:pt-6 transition-all duration-500'>
              <div class="lg:min-w-[180px] max-lg:min-w-[140px]">
                <h6 class="text-base text-[#007bff] font-bold">USA</h6>
                <ul class='mt-3 pt-3 border-t border-1 space-y-3'>
                  <li class='max-lg:border-b py-1 rounded'><a href='javascript:void(0)' class='hover:text-[#007bff] text-gray-500 font-bold text-sm block'>New York</a></li>
                  <li class='max-lg:border-b py-1 rounded'><a href='javascript:void(0)' class='hover:text-[#007bff] text-gray-500 font-bold text-sm block'>San Francisco</a></li>
                  <li class='max-lg:border-b py-1 rounded'><a href='javascript:void(0)' class='hover:text-[#007bff] text-gray-500 font-bold text-sm block'>Houston</a></li>
                </ul>
              </div>
            </div>
          </li> -->
           </ul>
      </div>
  
      <div class='flex items-center ml-auto lg:hidden'>
        <button on:click={toggleMenu} id="toggleOpen">
          <svg class="w-7 h-7" fill="#000" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
            <path fill-rule="evenodd" d="M3 5a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 10a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 15a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1z" clip-rule="evenodd"></path>
          </svg>
        </button>
      </div>
      <button type="button" on:click={clearAllCookies} 
      class="ml-auto py-2 px-7 text-sm font-semibold tracking-wider rounded-md text-white bg-blue-600 hover:bg-blue-700 focus:outline-none h-full">
      Log Out
    </button>

    </div>

  </header>
  