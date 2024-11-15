<script>

    import {onMount, onDestroy} from 'svelte'
    import Nav from '../nav/+page.svelte'
    import Footer from '../footer/+page.svelte'
    import ServiceSelection from './serviceSelection.svelte'
    import DateTime from './dateTime.svelte'
    import { service, dateTime } from './bookingStorage'

    // let serviceContainer
    let sideMenu = true


    // function handleClickOutside(event) {
    //     if (services && serviceContainer && !serviceContainer.contains(event.target)) {
    //         services = false
    //         currentSelection = undefined
    //     }
    // }

    function toggleSideMenu() {
        sideMenu = !sideMenu
    }

    // onMount(() => {
    //     if (typeof document !== 'undefined') {
    //         document.addEventListener('click', handleClickOutside);
    //     }
    // });

    // onDestroy(() => {
    //     if (typeof document !== 'undefined') {
    //         document.removeEventListener('click', handleClickOutside);
    //     }
    // });

    function nextStep() {
        if ($service === true) {
            service.set(false)
            dateTime.set(true)
        }
    }

    function goBack() {
        if ($dateTime === true) {
            service.set(true)
            dateTime.set(false)
        }
    }
</script>




<div class="fixed top-0 z-40 w-full">
    <Nav />
</div>

<div class="mt-[6.5rem] mb-4 w-full flex justify-center">
    <!-- <div class="flex justify-center gap-4">
        <p>Services</p>

        <p>Scheduling</p>

        <p>My Information</p>

        <p>Confirm</p>
    </div> -->
    <div class=" text-white h-[550px] max-w-[800px] w-full shadow-md border rounded-md border-zinc-300 mx-4 flex">

        <!-- Step tab -->
        <div class="bg-gold rounded-l-md {sideMenu ? 'w-[20rem]' : 'w-[4rem]'} hidden md:flex flex-col justify-between transition-all duration-300">
            {#if sideMenu}
                <div class="px-4 pt-4">
                    <div class="flex items-center justify-between mb-4 bg-white bg-opacity-10 rounded-md p-2">
                        <div class="flex items-center gap-2">
                            <div class="fa-solid fa-cubes"></div>
                            <p class="">Service Selection</p>
                        </div>

                        <div class="bg-gold h-5 w-5 rounded-full border-4"></div>
                    </div>

                    <div class="flex items-center justify-between mb-4 bg-white bg-opacity-10 rounded-md p-2">
                        <div class="flex items-center gap-2">
                            <div class="fa-solid fa-calendar"></div>
                            <p class="">Date & Time</p>
                        </div>

                        <!-- <div class="bg-gold h-5 w-5 rounded-full border-4"></div> -->
                        <div class="bg-gold h-5 w-5 rounded-full"></div> 
                    </div>

                    <div class="flex items-center justify-between mb-4 bg-white bg-opacity-10 rounded-md p-2">
                        <div class="flex items-center gap-2">
                            <div class="fa-solid fa-circle-user"></div>
                            <p class="">My Information</p>
                        </div>

                        <!-- <div class="bg-gold h-5 w-5 rounded-full border-4"></div> -->
                        <div class="bg-gold h-5 w-5 rounded-full"></div> 
                    </div>
        
                    <div class="flex items-center justify-between mb-4 bg-white bg-opacity-10 rounded-md p-2">
                        <div class="flex items-center gap-2">
                            <div class="fa-solid fa-credit-card"></div>
                            <p class="">Payment</p>
                        </div>

                        <!-- <div class="bg-gold h-5 w-5 rounded-full border-4"></div> -->
                        <div class="bg-gold h-5 w-5 rounded-full"></div> 
                    </div>
                </div>

                <div class="px-4 pb-2">
                    <div class="border-y border-white border-opacity-20 py-2 text-center text-sm mb-2">
                        <p>Questions?</p>
                        <p>(801)-123-4567</p>
                        <p>support@ameliatms.com</p>
                    </div>
                    <div class="flex justify-between items-center">
                        <p>Collapse Menu</p>
                        <button on:click={toggleSideMenu} class="fa-solid fa-chevron-left bg-white text-gold px-[5px] py-[3px] rounded-full text-[12px]"></button>
                    </div>
                </div>
            {:else if !sideMenu}
            <!-- step tab closed -->
                <div class="flex flex-wrap gap-8 pt-6">
                    <div class="basis-full flex justify-center relative">
                        <div class="fa-solid fa-cubes"></div>
                        <div class="absolute top-4 right-3 bg-gold h-3 w-3 rounded-full border-2"></div>
                    </div>

                    <div class="basis-full flex justify-center">
                        <div class="fa-solid fa-calendar"></div>
                        <!-- <div class="absolute top-4 right-3 bg-gold h-3 w-3 rounded-full border-2"></div>-->
                    </div>

                    <div class="basis-full flex justify-center">
                        <div class="fa-solid fa-circle-user"></div>
                        <!-- <div class="absolute top-4 right-3 bg-gold h-3 w-3 rounded-full border-2"></div> -->
                    </div>

                    <div class="basis-full flex justify-center">
                        <div class="fa-solid fa-credit-card"></div>
                        <!-- <div class="absolute top-4 right-3 bg-gold h-3 w-3 rounded-full border-2"></div> -->
                    </div>
                </div>

                <div class="flex justify-center pb-2">
                    <button on:click={toggleSideMenu} class="fa-solid fa-chevron-right bg-white text-gold px-[5px] py-[3px] rounded-full text-[12px]"></button>
                </div>
            {/if}
        </div>

        <!-- content steps -->
        <div class="bg-white w-full rounded-md md:rounded-r-md pt-4 pb-2 flex flex-col justify-between">
            <div>
                {#if $service}
                    <h1 class="px-4 pb-4 md:shadow-md w-full text-black font-bold">Service Selection</h1>
                {:else if $dateTime}
                    <div class="flex gap-2 items-center px-4 pb-4 md:shadow-md ">
                        <button on:click={goBack} class="fa-solid fa-chevron-left text-white bg-black text-xs px-3 py-1 rounded-lg"></button>
                        <h1 class="w-full text-black font-bold">Date & Time</h1>
                    </div>
                {/if}

                <!-- On small screens this is the progress bar for the different steps of the booking -->
                <div class="md:hidden text-black flex justify-between gap-1">
                    <div class="h-1 bg-gold bg-gold w-full border-gold"></div>
                    <div class="h-1 bg-gold  bg-gold w-full border-gold {$dateTime ? '' : 'opacity-40'}"></div>
                    <div class="h-1 bg-gold opacity-40 bg-gold w-full border-gold"></div>
                    <div class="h-1 bg-gold opacity-40 bg-gold w-full border-gold"></div>
                </div>
            </div>

            {#if $service}
                <ServiceSelection />
            {:else if $dateTime}
                <DateTime />
            {/if}

            <div class="w-full flex justify-end px-4 pt-2 shadow-[0px_-4px_4px_0px_rgba(0,0,0,0.1)]">
                <button on:click={nextStep} class="bg-gold py-1 px-4 rounded-md">Continue</button>
            </div>

        </div>

    </div>
</div>

<Footer />

<!-- 
<style>
    .custom-select:focus {
        outline: none;
        box-shadow: none;
    }
</style> -->