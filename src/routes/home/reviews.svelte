<script>
    import { Ratings } from '@skeletonlabs/skeleton'

    let value = {max: 5}

    let reviews = [
        {
            id: 1,
            name: 'John Doe',
            title: 'Review Title',
            reviewBody: 'Review Body',
            rating: 2,
            reviewDate: '2022-01-01',
        },
        {
            id: 2,
            name: 'John Doe',
            title: 'Review Title',
            reviewBody: 'Review Body',
            rating: 4,
            reviewDate: '2022-01-01',
        },
        {
            id: 3,
            name: 'John Doe',
            title: 'Review Title',
            reviewBody: 'Review Body',
            rating: 5,
            reviewDate: '2022-01-01',
        },
    ]
</script>


<div class="bg-white px-4 py-24">
    <h1  class="font-bold text-lg mb-4">Latest Reviews</h1>

    <div class="grid grid-cols-3 gap-4">
        {#each reviews as review}
            <div class="border border-zinc-300 rounded-lg shadow-md p-4">
                <div class="flex justify-start mb-4">
                    <div>
                        <Ratings bind:value={review.rating} max={value.max} >
                            <svelte:fragment slot="empty"><i class="fa-regular fa-star"></i></svelte:fragment>
                            <svelte:fragment slot="full"><i class="fa-solid fa-star"></i></svelte:fragment>
                        </Ratings>
                    </div>
                </div>
    
                <h1 class="text-lg font-bold">{review.title}</h1>
    
                <p class="mb-4">{review.reviewBody}</p>
    
                <div class="flex gap-2">
                    <div class="rounded-full bg-zinc-200 w-10 h-10 flex justify-center items-center">
                        <i class="fa-solid fa-image opacity-40"></i>
                    </div>
    
                    <div>
                        <p class="">{review.name}</p>
                        <p class="text-xs text-zinc-400">{review.reviewDate}</p>
                    </div>
                </div>
            </div>
        {/each}
    </div>
</div>