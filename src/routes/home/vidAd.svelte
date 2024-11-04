<script>
    function freeConsult() {
        alert('Free Consultation: nothing is hooked up')
    }
</script>

<div class="flex bg-white px-4 gap-4 py-24">
    <div class="basis-1/2 w-full flex justify-center bg-zinc-300 rounded-md items-center">
        <!-- <img src="./default_vid_ad.png" alt="Default video ad" class="w-1/2 rounded-lg"> -->
         <i class="fa-solid fa-image opacity-40 text-7xl"></i>
    </div>

    <div class="basis-1/2">
        <h1 class="font-bold text-lg mb-4">Grow Your Business with Video Ads</h1>

        <p class="text-lg text-zinc-600 mb-4">Effective advertising starts with setting the right goals</p>

        <p class="mb-4">Our team conceptualizes and creates video and photography media for your business and implements it into your social media marketing strategy to drive more customers to your website and increase sales. We utilize full-funnel marketing tactics and apply them to visual media concepts to help you connect with your target markets and scale your business.</p>

        <a on:click={freeConsult} class="cursor-pointer bg-black text-white py-1 px-3 rounded-lg hover:bg-zinc-800 transition-all duration-300">Free Consultation</a>
    </div>
</div>