<template>
    <div class="absolute top-1 right-16 cursor-pointer">
        <button @click="favoriteContact">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" v-if="favoritesExist === ''" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11.049 2.927c.3-.921 1.603-.921 1.902 0l1.519 4.674a1 1 0 00.95.69h4.915c.969 0 1.371 1.24.588 1.81l-3.976 2.888a1 1 0 00-.363 1.118l1.518 4.674c.3.922-.755 1.688-1.538 1.118l-3.976-2.888a1 1 0 00-1.176 0l-3.976 2.888c-.783.57-1.838-.197-1.538-1.118l1.518-4.674a1 1 0 00-.363-1.118l-3.976-2.888c-.784-.57-.38-1.81.588-1.81h4.914a1 1 0 00.951-.69l1.519-4.674z" />
            </svg>
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-yellow-500" v-else viewBox="0 0 20 20" fill="currentColor">
                <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
            </svg>
        </button>
    </div>
</template>

<script>
    export default {
        props: ['contactId', 'favorite'],
        
        data() {
            return {
                favoritesExist: this.favorite
            }
        },
        
        methods: {
            favoriteContact(){
                axios.post('/favorites/' + this.contactId)
                .then(response => {
                    const obj = response.data

                    if (obj.attached[0] == this.contactId) {
                        this.favoritesExist = 'value'
                    }
                    else if(obj.detached[0] == this.contactId){
                        this.favoritesExist = ''
                    }
                });
            }
        },
        
    }
</script>