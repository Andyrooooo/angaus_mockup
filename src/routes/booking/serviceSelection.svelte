<script>

    import {slide, fly} from 'svelte/transition'
    import { booking } from './booking.js'
    let services = false
    let currentSelection
    let servicesSelection = false
    let servicesMobile = false

    /* custom photography price variables */
    let basePhotoAmount = 32
    let baseSquareFootage = 4000
    let basePrice = 225
    let photoAmount = basePhotoAmount
    let squareFootage = baseSquareFootage
    let customPhotoPrice = basePrice

    /* custom cineTour price variables */
    let baseCinePrice = 425
    let baseCineSquareFootage = 4000
    let cineSquareFootage = baseCineSquareFootage
    let customCinePrice = baseCinePrice

    function selectService() {
        services = !services

        if (!services) {
            servicesSelection = false
            currentSelection = undefined
            console.log(currentSelection)
        }

        // if (!servicesMobile) {
        //     servicesSelection = false
        //     currentSelection = undefined
        // }

        // servicesMobile = !servicesMobile
    }

    let aerialSelected = {
        title: "Aerial Photos",
        data: booking.aerial,
        type: "aerial"
    }

    let photoSelected = {
        title: "Photography",
        data: booking.photography,
        type: "photography"
    }

    let cineTourSelected = {
        title: "CineTours",
        data: booking.CineTours,
        type: "cineTours"
    }

    let addOnsSelected = {
        title: "Add-ons",
        data: booking.addOns,
        type: "addOns"
    }

    function currentCategory(selection) {
        if (selection === "photography") {
            servicesSelection = true
            currentSelection = photoSelected
        } else if (selection === "Aerial") {
            servicesSelection = true
            currentSelection = aerialSelected
        } else if (selection === "cineTours") {
            servicesSelection = true
            currentSelection = cineTourSelected
            console.log(currentSelection)
        } else if (selection === "addOns") {
            servicesSelection = true
            currentSelection = addOnsSelected
        }
    }

    function updateCustomPhotoPrice() {
        let additionalPhotos = photoAmount - basePhotoAmount;
        let additionalSquareFootage = (squareFootage - baseSquareFootage) / 100;
        customPhotoPrice = basePrice + Math.floor(additionalPhotos * 2.0833) + Math.floor(additionalSquareFootage * 1.25);
    }

    function photoAmountChange(event) {
        photoAmount = event.target.value;
        updateCustomPhotoPrice();
    }

    function squareFootageChange(event) {
        squareFootage = event.target.value;
        updateCustomPhotoPrice();
    }

    function updateCustomCinePrice() {
        let additionalSquareFootage = (cineSquareFootage - baseCineSquareFootage) / 100;
        customCinePrice = baseCinePrice + Math.floor(additionalSquareFootage * 5);
    }

    function cineSquareFootageChange(event) {
        cineSquareFootage = event.target.value;
        updateCustomCinePrice();
    }
</script>






<div class="w-full h-full px-4 flex items-start">
    <!-- <div bind:this={serviceContainer} class="pt-4 w-full"> for some reason this was closing the scheduling stuff -->
    <div class="pt-4 w-full">
        <label class="text-black font-bold pb-1" for="service">Service:</label>

        <button on:click={selectService} class="{services ? 'border-gold' : 'border-zinc-300'} text-black w-full rounded-md shadow-md border flex justify-between px-4 py-2 items-center">
            <p>{currentSelection ? currentSelection.title : (currentSelection === undefined ? 'Select Service' : 'Select Service')}</p>
            <i class="fa-solid fa-chevron-down {services ? 'rotate-180' : ''} transition-all duration-300"></i>
        </button>

        {#if services}
<!------------------------------------------------ medium and large Screen service component  ------------------------------------------------------------------------->
            <div class="hidden md:flex text-black w-full rounded-md shadow-md border border-gold mt-2 h-full ">
                <div transition:slide class=" flex flex-col gap-1 {servicesSelection ? 'w-1/3 ' : 'w-full'} h-full">
                <!-- <div transition:slide class=" flex flex-col w-1/3 h-full gap-1 pt-2"> -->
                    <label for="categories" class=" text-xs font-bold px-4 py-1">Categories</label>
                    <button on:click={(e) => currentCategory("photography")} class="{currentSelection === undefined ? 'text-black' : (currentSelection.type === 'photography' ? 'text-gold font-semibold' : 'text-black')} px-4 hover:bg-gold hover:bg-opacity-20 py-1 text-start py-1">Photography</button>
                    <button on:click={(e) => currentCategory("Aerial")} class="{currentSelection === undefined ? 'text-black' : (currentSelection.type === 'aerial' ? 'text-gold font-semibold' : 'text-black')} px-4 hover:bg-gold hover:bg-opacity-20 text-start py-1">Aerial Photos</button>
                    <button on:click={(e) => currentCategory("cineTours")} class="{currentSelection === undefined ? 'text-black' : (currentSelection.type === 'cineTours' ? 'text-gold font-semibold' : 'text-black')} px-4 hover:bg-gold hover:bg-opacity-20 text-start py-1">CineTours</button>
                    <button on:click={(e) => currentCategory("addOns")} class="{currentSelection === undefined ? 'text-black' : (currentSelection.type === 'addOns' ? 'text-gold font-semibold' : 'text-black')} px-4 hover:bg-gold hover:bg-opacity-20 text-start py-1">Add-ons</button>
                </div>

                
                {#if servicesSelection}
                    <div transition:slide class=" w-full bg-zinc-100 rounded-r-md ">
                        <label for="photography" class=" text-xs font-bold px-4 py-1.5 bg-gold rounded-tr-md text-white shadow-md">{currentSelection.title}</label>

                        <!--------------------------------------- If you select the "photography" or aerial category  ------------------------------>
                        {#if currentSelection.type === "photography" || currentSelection.type === "aerial" || currentSelection.type === "addOns"}
                            
                            <div class="w-full px-4 py-4 h-[292px] overflow-y-scroll">
                            {#each currentSelection.data as photo}
                                <div class="bg-white rounded-md shadow-md px-4 pt-4 text-xs border border-zinc-200 mb-4">
                                    <div class="bg-zinc-300 w-full h-[200px] mb-4 rounded-sm flex justify-center items-center">
                                        <i class="fa-solid fa-image text-6xl text-zinc-400"></i>
                                    </div>

                                    <div class="flex justify-between mb-4 items-center">
                                        <p class="text-zinc-700 font-semibold">{photo.title}</p>
                                        <p class="rounded-full px-1.5 py-0.5 bg-zinc-700 text-white shadow-md text-[8px]">{photo.photoAmount} Photos</p>
                                    </div>

                                    <p class="mb-4 text-sm">{photo.description}</p>

                                    {#if photo.customType === true}
                                        <div class="mb-2">
                                            <div class="flex justify-between">
                                                <p class="mb-1">Number of photos: </p>
                                                <p>{photoAmount}</p>
                                            </div>
                                            <input bind:value={photoAmount} on:input={photoAmountChange} type="range" min="32" max="120" step="1" />
                                        </div>

                                        <div class="mb-4">
                                            <div class="flex justify-between">
                                                <p class="mb-1">Square Footage: </p>
                                                <p>{squareFootage}</p>
                                            </div>
                                            <input bind:value={squareFootage} on:input={squareFootageChange} type="range" min="4000" max="8000" step="100" />
                                        </div>
                                    {/if}

                                    <div class="flex justify-between border-t border-zinc-200 pt-2 pb-2 items-center">
                                        {#if photo.customType === true}
                                            <p class="font-semibold">${customPhotoPrice}</p>
                                        {:else}
                                            <p class="font-semibold">${photo.price}</p>
                                        {/if}
                                        <button class="bg-gold text-white rounded-md px-2 py-1">Add to Cart</button>
                                    </div>
                                </div>
                            {/each}
                            </div>

                        <!--------------------------------------- If you select the "photography" or aerial category  ------------------------------>
                        {:else if currentSelection.type === "cineTours"}
                            
                            <div class="w-full px-4 py-4 h-[292px] overflow-y-scroll">
                                {#each currentSelection.data as cine}
                                    <div class="bg-white rounded-md shadow-md px-4 pt-4 text-xs border border-zinc-200 mb-4">
                                        <div class="bg-zinc-300 w-full h-[200px] mb-4 rounded-sm flex justify-center items-center relative">
                                            <i class="fa-solid fa-image text-6xl text-zinc-400"></i>

                                            {#if cine.includesAerials === true}
                                                <div class="absolute z-10 top-2 left-2 bg-gold text-white px-1.5 py-0.5 rounded-md shadow-lg">Includes Aerials</div>
                                            {/if}
                                        </div>

                                        <div class="flex justify-between mb-4 items-center">
                                            <p class="text-zinc-700 font-semibold">{cine.title}</p>
                                            {#if cine.propertySize}
                                                <p class="rounded-full px-1.5 py-0.5 bg-zinc-700 text-white shadow-md text-[8px]">{cine.propertySize}</p>
                                            {/if}
                                        </div>

                                        <p class="mb-4 text-sm">{cine.description}</p>

                                        {#if cine.customType === true}
                                            <div class="mb-4">
                                                <div class="flex justify-between">
                                                    <p class="mb-1">Square Footage: </p>
                                                    <p>{cineSquareFootage}</p>
                                                </div>
                                                <input bind:value={cineSquareFootage} on:input={cineSquareFootageChange} type="range" min="4000" max="8000" step="100" />
                                            </div>
                                        {/if}

                                        <div class="flex justify-between border-t border-zinc-200 pt-2 pb-2 items-center">
                                            {#if cine.customType === true}
                                                <p class="font-semibold">${customCinePrice}</p>
                                            {:else}
                                                <p class="font-semibold">${cine.price}</p>
                                            {/if}
                                            <button class="bg-gold text-white rounded-md px-2 py-1">Add to Cart</button>
                                        </div>
                                    </div>
                                {/each}
                            </div>    

                        {/if}

                    </div>
                {/if} <!-- end of servicesSelection -->
            </div>
        {/if}<!-- end of service modal -->


<!------------------------------------------------ Small Screen service component  ---------------------------------------------------------------------------->
        {#if services}
            <div class="flex md:hidden text-black w-full rounded-md shadow-md border border-gold mt-2 h-full ">
                <div transition:slide class=" flex flex-col gap-1 w-full h-full">
                <!-- <div transition:slide class=" flex flex-col w-1/3 h-full gap-1 pt-2"> -->
                    <label for="categories" class=" text-xs font-bold px-4 py-1">Categories</label>
                    <button on:click={(e) => currentCategory("photography")} class="{currentSelection === undefined ? 'text-black' : (currentSelection.type === 'photography' ? 'text-gold font-semibold' : 'text-black')} px-4 hover:bg-gold hover:bg-opacity-20 py-1 text-start py-1">Photography</button>
                    <button on:click={(e) => currentCategory("Aerial")} class="{currentSelection === undefined ? 'text-black' : (currentSelection.type === 'aerial' ? 'text-gold font-semibold' : 'text-black')} px-4 hover:bg-gold hover:bg-opacity-20 text-start py-1">Aerial Photos</button>
                    <button on:click={(e) => currentCategory("cineTours")} class="{currentSelection === undefined ? 'text-black' : (currentSelection.type === 'cineTours' ? 'text-gold font-semibold' : 'text-black')} px-4 hover:bg-gold hover:bg-opacity-20 text-start py-1">CineTours</button>
                    <button on:click={(e) => currentCategory("addOns")} class="{currentSelection === undefined ? 'text-black' : (currentSelection.type === 'addOns' ? 'text-gold font-semibold' : 'text-black')} px-4 hover:bg-gold hover:bg-opacity-20 text-start py-1">Add-ons</button>
                </div>
            </div>
        {/if}
                
        {#if servicesSelection}
            <div transition:slide class="block md:hidden w-full bg-zinc-100 rounded-md mt-2 shadow-lg border border-zinc-300">
                <label for="photography" class=" text-xs font-bold px-4 py-1.5 bg-gold rounded-t-md text-white shadow-md">{currentSelection.title}</label>

                <!--------------------------------------- If you select the "photography" or aerial category  ------------------------------>
                {#if currentSelection.type === "photography" || currentSelection.type === "aerial" || currentSelection.type === "addOns"}
                    
                    <div class="w-full px-4 py-4 h-[292px] overflow-y-scroll">
                    {#each currentSelection.data as photo}
                        <div class="bg-white rounded-md shadow-md px-4 pt-4 text-xs border border-zinc-200 mb-4">
                            <div class="bg-zinc-300 w-full h-[200px] mb-4 rounded-sm flex justify-center items-center">
                                <i class="fa-solid fa-image text-6xl text-zinc-400"></i>
                            </div>

                            <div class="flex justify-between mb-4 items-center">
                                <p class="text-zinc-700 font-semibold">{photo.title}</p>
                                <p class="rounded-full px-1.5 py-0.5 bg-zinc-700 text-white shadow-md text-[8px]">{photo.photoAmount} Photos</p>
                            </div>

                            <p class="mb-4 text-sm">{photo.description}</p>

                            {#if photo.customType === true}
                                <div class="mb-2">
                                    <div class="flex justify-between">
                                        <p class="mb-1">Number of photos: </p>
                                        <p>{photoAmount}</p>
                                    </div>
                                    <input bind:value={photoAmount} on:input={photoAmountChange} type="range" min="32" max="120" step="1" />
                                </div>

                                <div class="mb-4">
                                    <div class="flex justify-between">
                                        <p class="mb-1">Square Footage: </p>
                                        <p>{squareFootage}</p>
                                    </div>
                                    <input bind:value={squareFootage} on:input={squareFootageChange} type="range" min="4000" max="8000" step="100" />
                                </div>
                            {/if}

                            <div class="flex justify-between border-t border-zinc-200 pt-2 pb-2 items-center">
                                {#if photo.customType === true}
                                    <p class="font-semibold">${customPhotoPrice}</p>
                                {:else}
                                    <p class="font-semibold">${photo.price}</p>
                                {/if}
                                <button class="bg-gold text-white rounded-md px-2 py-1">Add to Cart</button>
                            </div>
                        </div>
                    {/each}
                    </div>

                <!--------------------------------------- If you select the "photography" or aerial category  ------------------------------>
                {:else if currentSelection.type === "cineTours"}
                    
                    <div class="w-full px-4 py-4 h-[292px] overflow-y-scroll">
                        {#each currentSelection.data as cine}
                            <div class="bg-white rounded-md shadow-md px-4 pt-4 text-xs border border-zinc-200 mb-4">
                                <div class="bg-zinc-300 w-full h-[200px] mb-4 rounded-sm flex justify-center items-center relative">
                                    <i class="fa-solid fa-image text-6xl text-zinc-400"></i>

                                    {#if cine.includesAerials === true}
                                        <div class="absolute z-10 top-2 left-2 bg-gold text-white px-1.5 py-0.5 rounded-md shadow-lg">Includes Aerials</div>
                                    {/if}
                                </div>

                                <div class="flex justify-between mb-4 items-center">
                                    <p class="text-zinc-700 font-semibold">{cine.title}</p>
                                    {#if cine.propertySize}
                                        <p class="rounded-full px-1.5 py-0.5 bg-zinc-700 text-white shadow-md text-[8px]">{cine.propertySize}</p>
                                    {/if}
                                </div>

                                <p class="mb-4 text-sm">{cine.description}</p>

                                {#if cine.customType === true}
                                    <div class="mb-4">
                                        <div class="flex justify-between">
                                            <p class="mb-1">Square Footage: </p>
                                            <p>{cineSquareFootage}</p>
                                        </div>
                                        <input bind:value={cineSquareFootage} on:input={cineSquareFootageChange} type="range" min="4000" max="8000" step="100" />
                                    </div>
                                {/if}

                                <div class="flex justify-between border-t border-zinc-200 pt-2 pb-2 items-center">
                                    {#if cine.customType === true}
                                        <p class="font-semibold">${customCinePrice}</p>
                                    {:else}
                                        <p class="font-semibold">${cine.price}</p>
                                    {/if}
                                    <button class="bg-gold text-white rounded-md px-2 py-1">Add to Cart</button>
                                </div>
                            </div>
                        {/each}
                    </div>    

                {/if}

            </div>
        {/if} <!-- end of servicesSelection -->
            
    </div>
</div>

    
