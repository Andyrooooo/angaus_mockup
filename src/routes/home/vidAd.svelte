<script>
    import { onMount } from 'svelte'

    let counter
    let yearCount = 0
    let projCount = 0
    let animationTriggered = false; // Flag to track if the animation has been triggered

    function animateCount(target, setCount, duration) {
        let start = 0;
        const increment = target / (duration / 10); // Calculate increment based on duration

        const interval = setInterval(() => {
            start += increment;
            if (start >= target) {
                start = target;
                clearInterval(interval);
            }
            setCount(Math.floor(start));
        }, 10);
    }

    onMount(() => {
        const observer = new IntersectionObserver(entries => {
                entries.forEach(entry => {
                    if (entry.isIntersecting && !animationTriggered) {
                        animationTriggered = true; // Set the flag to true
                        if (entry.target === counter) {
                            animateCount(10, value => yearCount = value, 2000); // 2 seconds duration
                            animateCount(375, value => projCount = value, 2000); // 2 seconds duration
                        }
                    }
                })
            }, {
                rootMargin: '0px',
                threshold: 0.1 // Adjust this value based on when you want the animation to trigger
            })

            observer.observe(counter)

            return () => {
                observer.disconnect()
            }
    })

    function freeConsult() {
        alert('Free Consultation: nothing is hooked up')
    }
</script>



<div class="relative h-screen flex items-center justify-center w-full">

    <div class="absolute z-10 top-0 w-full bg-background h-12 "></div>
    <div class="absolute z-10 bottom-0 w-full bg-background h-12 "></div>

    <!-- <div class="h-3/4 w-full relative flex lg:px-4  "> -->
    <div class="h-full w-full relative flex lg:px-4 lg:pb-4 ">
        <!-- <div class="h-full w-full absolute top-0 left-0 lg:px-4"> -->
        <div class="h-full w-full absolute top-0 left-0 lg:px-4 lg:pb-4">
            <div class="h-full bg-black lg:rounded-md"></div>
        </div>

        <img src="vid_ad.jpg"  alt="default ad background" class=" opacity-80 h-full w-full object-cover lg:rounded-md"/>
    </div>

    
    <div class="absolute z-10 top-0 h-full flex px-4 gap-4 justify-end items-center">
        <div class="basis-full lg:basis-1/2">
            <h1 class="text-white text-2xl mb-4">Grow Your Business with Video Advertising.</h1>
    
            <p class="text-lg text-zinc-300 mb-4">Effective advertising starts with setting the right goals.</p>
    
            <p class="mb-4 text-white">Our team conceptualizes and creates video and photography media for your business and implements it into your social media marketing strategy to drive more customers to your website and increase sales. We utilize full-funnel marketing tactics and apply them to visual media concepts to help you connect with your target markets and scale your business.</p>
    
            <div class="flex gap-12 w-full mb-8">
                <div class="text-white font-bold text-xl">
                    <p>{yearCount} +</p>
                    <p>Years Experience</p>
                </div>
    
                <div class="text-white font-bold text-xl">
                    <p>{projCount} +</p>
                    <p>Completed Projects</p>
                </div>
            </div>

            <a on:click={freeConsult} class="cursor-pointer bg-gold text-white py-1 px-3 rounded-lg hover:bg-zinc-800 transition-all duration-300">Free Consultation</a>
        </div>
    </div>

    <div bind:this={counter}></div>
</div>