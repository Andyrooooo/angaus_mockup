<script>
    let menu = false

    function toggleMenu() {
        menu = !menu
    }

    function navLinks() {
        alert('navigation link click: nothing is hooked up')
    }
</script>

<div class="w-full bg-white border-b border-zinc-300">
    <div class="flex max-w-[1536px] mx-auto items-center justify-between p-4 ">
        <div>
            <a href="./">
                <img src="./default_logo.png" alt="Default photography logo" class="w-12 h-10 hover:bg-zinc-200 py-1 px-2 rounded-md transition-all duration-300">
            </a>
        </div>
    
        <div class=" gap-4 hidden md:flex">
            <div>
                <a on:click={navLinks} class="cursor-pointer bg-zinc-200 px-2 py-1 rounded-lg hover:bg-zinc-300 transition-all duration-300">Home</a>
                <!-- <a on:click={navLinks} class=" md:hidden cursor-pointer bg-zinc-200 px-2 py-1 rounded-lg hover:bg-zinc-300 transition-all duration-300 fa-solid fa-house text-xl"></a> -->
            </div>
    
            <div>
                <a on:click={navLinks} class="cursor-pointer">Services</a>
                <!-- <a on:click={navLinks} class=" md:hidden cursor-pointer fa-solid fa-photo-film text-xl px-2 py-1"></a> -->
            </div>
    
            <div>
                <a on:click={navLinks} class="cursor-pointer">Projects</a>
                <!-- <a on:click={navLinks} class=" md:hidden cursor-pointer fa-solid fa-clipboard-list text-xl px-2 py-1"></a> -->
            </div>
    
            <div>
                <a on:click={navLinks} class="cursor-pointer">Resources</a>
            </div>
    
            <div>
                <a on:click={navLinks} class="cursor-pointer">Real Estate</a>
            </div>
    
            <div>
                <a on:click={navLinks} class="cursor-pointer">Contact Us</a>
            </div>
    
            <div>
                <a on:click={navLinks} class="cursor-pointer bg-black text-white py-1 px-6 rounded-lg hover:bg-zinc-800 transition-all duration-300">Free Consultation</a>
            </div>
        </div>

        <div class="w-[3rem] h-10 md:hidden">
            <button on:click={toggleMenu} class="w-full h-full hover:bg-zinc-200 rounded-md transition-all duration-300 px-1 ">
                <div class="bg-black rounded-full h-1 w-3/4 mx-auto mb-1.5 transition-all duration-300 {menu ? 'rotate-45 translate-y-2.5' : ''} "></div>
                <div class="bg-black rounded-full h-1 w-3/4 mx-auto mb-1.5 transition-all duration-300 {menu ? 'opacity-0' : ''} "></div>
                <div class="bg-black rounded-full h-1 w-3/4 mx-auto transition-all duration-300 {menu ? '-rotate-45 -translate-y-2.5' : ''} "></div>
            </button>
        </div>
    </div>
</div>