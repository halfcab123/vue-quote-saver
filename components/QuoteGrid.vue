<template>
        <div>
            <div style="margin-top: 1em" class="card-columns">
                <template v-for="(quote,i) in quoteArr">
                    <quote-card :index="i" :quote="quote">"{{ quote }}"<br><small style="font-size: 0.5em; font-family: arial">- anonymous</small></quote-card>
                </template>
            </div>
        </div>
</template>

<script>
    import Quote from './Quote.vue'

    export default {
        data: function() {
            return {
                quoteArr: [
                    'A champion is defined not by their wins but by how they can recover when they fall.',
                    'With the right kind of coaching and determination you can accomplish anything.'
                ]
            }
        },
        props: ['quotes'],
        components:  {
            quoteCard: Quote
        },
        mounted: function(){
            const vm = this
            this.$bus.$on('new-quote', (quote)=>vm.quoteArr.push(quote))

            this.$bus.$on('delete-quote', (quote)=>{
                const i = vm.quoteArr.findIndex((el)=>quote === el)
               vm.quoteArr.splice(i,1)
            })
        }
    }
</script>
