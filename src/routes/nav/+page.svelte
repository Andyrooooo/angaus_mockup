<script>
    import { onMount, onDestroy } from 'svelte'
    import {slide} from 'svelte/transition'
    
    let menu = false
    let menuContainer
    let reMenu = false
    let reMenuMobile = false
    let hamover = false
    let navBar = false

    function toggleMenu() {
        menu = !menu
        if (menu === false) {
            reMenuMobile = false
        }
    }

    function navLinks() {
        alert('navigation link click: nothing is hooked up')
    }

    function handleClickOutside(event) {
        if (menu && menuContainer && !menuContainer.contains(event.target)) {
            menu = false
            reMenuMobile = false
        }
    }

    function handleResize() {
        if (window.innerWidth >= 768) {
            menu = false;
            reMenuMobile = false
        }
    }

    function handleScroll() {
        if (window.scrollY > 16) { // 1rem = 16px
            navBar = true
        } else {
            navBar = false
        }
    }

    onMount(() => {
        if (typeof document !== 'undefined') {
            document.addEventListener('click', handleClickOutside);
            window.addEventListener('resize', handleResize);
            window.addEventListener('scroll', handleScroll)
        }
    });

    onDestroy(() => {
        if (typeof document !== 'undefined') {
            document.removeEventListener('click', handleClickOutside);
            window.removeEventListener('resize', handleResize);
            window.addEventListener('scroll', handleScroll)
        }
    });

    // function toggleREMenu() {
    //     reMenu = !reMenu
    // }
</script>

<div  bind:this={menuContainer}>
    <div class="w-full text-white {navBar ? 'p-0' : ' p-4'} 2xl:p-0 transition-all duration-300 2xl:bg-black">
        <div class="flex max-w-[1536px] mx-auto items-center justify-between p-2 px-4 relative border border-zinc-900 shadow-lg bg-black {navBar ? 'rounded-none' : 'rounded-2xl'} 2xl:border-none transition-all duration-300 ">
            <div>
                <a href="./">
                    <img src="./logo.png" alt="Default photography logo" class="w-24 hover:bg-zinc-900 py-1 px-2 rounded-md transition-all duration-300">
                </a>
            </div>
        
            <div on:mouseleave={() => {reMenu = false}} class=" gap-4 hidden md:flex h-full py-3">
                <div on:mouseover={() => {reMenu = false}}>
                    <!-- <a on:click={navLinks} class="cursor-pointer bg-zinc-200 px-2 py-1 rounded-lg hover:bg-zinc-300 transition-all duration-300">Home</a> -->
                    <a on:click={navLinks} class="cursor-pointer hover:text-gold transition-all duration-300 px-2 py-1 rounded-md hover:bg-zinc-900">Home</a>
                    <!-- <a on:click={navLinks} class=" md:hidden cursor-pointer bg-zinc-200 px-2 py-1 rounded-lg hover:bg-zinc-300 transition-all duration-300 fa-solid fa-house text-xl"></a> -->
                </div>
        
                <div on:mouseover={() => {reMenu = false}}>
                    <a on:click={navLinks} class="cursor-pointer px-2 py-1 rounded-md hover:text-gold transition-all duration-300 hover:bg-zinc-900">Services</a>
                    <!-- <a on:click={navLinks} class=" md:hidden cursor-pointer fa-solid fa-photo-film text-xl px-2 py-1"></a> -->
                </div>
        
                <div on:mouseover={() => {reMenu = false}} >
                    <a on:click={navLinks} class="cursor-pointer px-2 py-1 rounded-md hover:text-gold transition-all duration-300 hover:bg-zinc-900">Projects</a>
                    <!-- <a on:click={navLinks} class=" md:hidden cursor-pointer fa-solid fa-clipboard-list text-xl px-2 py-1"></a> -->
                </div>
        
                <!-- <div>
                    <a on:click={navLinks} class="cursor-pointer">Resources</a>
                </div> -->
        
                 <!------------- Real Estate Sub Menu --------------------------------->
                <div class="relative ">
                    <a on:mouseover={() => {reMenu = true}} class="cursor-pointer px-2 py-1 rounded-md hover:text-gold transition-all duration-300 hover:bg-zinc-900">Real Estate <a class="fa-solid fa-chevron-down text-sm {reMenu ? 'rotate-180' : ''} transition-all duration-300"></a></a>
    
                    {#if reMenu}
                        <div on:mouseleave={() => {reMenu = false}} class="absolute -bottom-[138px] z-10 bg-black shadow-lg rounded-md border border-zinc-900 p-4 w-[200px]">
                            <div class="mb-2">
                                <a class=" hover:text-gold cursor-pointer block" on:click={navLinks} >Real Estate Services</a>
                            </div>
    
                            <div class="mb-2">
                                <a on:click={navLinks} class="hover:text-gold cursor-pointer block">Portfolio</a>
                            </div>
    
                            <div class="mb-2">
                                <a on:click={navLinks} class="hover:text-gold cursor-pointer block">Booking</a>
                            </div>
                        </div>
                    {/if}
                </div>
        
                <div>
                    <a on:click={navLinks} class="cursor-pointer bg-gold rounded-md hover:bg-gray px-2 py-1 rounded-md transition-all duration-300">Contact Us</a>
                </div>
        
                <!-- <div>
                    <a on:click={navLinks} class="cursor-pointer bg-black text-white py-1 px-6 rounded-lg hover:bg-zinc-800 transition-all duration-300">Free Consultation</a>
                </div> -->
            </div>
    
            <!------------- Hamburger Menu --------------------------------->
            <div class="w-[3rem] h-10 md:hidden">
                <button on:mouseenter={() => {hamover = true}} on:mouseleave={() => {hamover = false}} on:click={toggleMenu} class="w-full h-full hover:bg-zinc-900 rounded-md transition-all duration-300 px-1 {menu ? 'rotate-[360deg]' : ''}">
                    <div class="{hamover ? 'bg-gold' : 'bg-white'} rounded-full h-1 w-3/4 mx-auto mb-1.5 transition-all duration-300 {menu ? 'rotate-[405deg] translate-y-2.5' : ''} "></div>
                    <div class="{hamover ? 'bg-gold' : 'bg-white'} rounded-full h-1 w-3/4 mx-auto mb-1.5 transition-all duration-300 {menu ? 'opacity-0' : ''} "></div>
                    <div class="{hamover ? 'bg-gold' : 'bg-white'} rounded-full h-1 w-3/4 mx-auto transition-all duration-300 {menu ? '-rotate-[405deg] -translate-y-2.5' : ''} "></div>
                </button>
            </div>
        </div>
    
        
    </div>
    
    
     <!------------- Mobile Menu --------------------------------->
    {#if menu}
        <div transition:slide class=" w-full absolute top-[4.8rem] -z-10 flex justify-center text-white">
            <div class="text-center w-full bg-black mx-4 py-12 border border-zinc-900 rounded-b-md">
                <div class="mb-3">
                    <a on:click={navLinks} class="cursor-pointer block hover:text-gold">Home</a>
                </div>
        
                <div class="mb-2">
                    <a on:click={navLinks} class="cursor-pointer block hover:text-gold">Services</a>
                </div>
        
                <div class="mb-2">
                    <a on:click={navLinks} class="cursor-pointer block hover:text-gold">Projects</a>
                </div>
        
                <!-- <div class="mb-2">
                    <a on:click={navLinks} class="cursor-pointer">Resources</a>
                </div> -->
        
                <div class="mb-2">
                    <a on:click={() => {reMenuMobile = !reMenuMobile}} class="cursor-pointer block hover:text-gold">Real Estate <a class="fa-solid fa-chevron-down text-sm {reMenuMobile ? 'rotate-180' : ''} transition-all duration-300"></a></a>
                </div>
    
                {#if reMenuMobile}
                    <div transition:slide class="bg-zinc-900 py-2 shadow-inner shadow-black">
                        <div class="mb-2">
                            <a class=" hover:text-gold cursor-pointer block" on:click={navLinks} >Real Estate Services</a>
                        </div>
    
                        <div class="mb-2">
                            <a on:click={navLinks} class="hover:text-gold cursor-pointer block">Portfolio</a>
                        </div>
    
                        <div class="">
                            <a href="/booking" class="hover:text-gold cursor-pointer block">Booking</a>
                        </div>
                    </div>
                {/if}
        
                <div class="mt-2">
                    <a on:click={navLinks} class="cursor-pointer block hover:text-gold">Contact Us</a>
                </div>
        
                <!-- <div class="">
                    <a on:click={navLinks} class="cursor-pointer bg-black text-white py-1 px-6 rounded-lg hover:bg-zinc-800 transition-all duration-300">Free Consultation</a>
                </div> -->
            </div>
        </div>
    {/if}
</div>