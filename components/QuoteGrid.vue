<template>
        <div>
            <div style="margin-top: 1em" class="card-columns">
                <transition-group name="list" tag="quote-card">
                    <quote-card :key="i" v-for="(quote,i) in quoteArr" :index="i" :quote="quote.quote">"{{ quote.quote }}"<br><small style="font-size: 0.5em; font-family: arial">- {{quote.author}}</small></quote-card>
                </transition-group>
            </div>
        </div>
</template>

<script>
    import Quote from './Quote.vue'

    export default {
        data: function() {
            return {
                quoteArr: [
                    {quote:'A champion is defined not by their wins but by how they can recover when they fall.',author:'Serena Williams'},
                    {quote:'A human being is a part of the whole called by us universe, a part limited in time and space. He experiences himself, his thoughts and feeling as something separated from the rest, a kind of optical delusion of his consciousness. This delusion is a kind of prison for us, restricting us to our personal desires and to affection for a few persons nearest to us.',author:'Albert Einstein'}
                ]
            }
        },
        methods: {
          updateQuoteCount: function(){
              const newTotal = this.quoteArr.length
              this.$bus.$emit('quote-count-changed', newTotal)
          }
        },
        props: ['quotes','maxQuotes'],
        components:  {
            quoteCard: Quote
        },
        mounted: function(){
            const vm = this
            this.$bus.$on('new-quote', (quote)=>{
                vm.quoteArr.push(quote)
                vm.updateQuoteCount()
                vm.$bus.$emit('success','Quote Successfully added')
            })

            this.$bus.$on('delete-quote', (quote)=>{
               const i = vm.quoteArr.findIndex((el)=>el.quote === quote)
               vm.quoteArr.splice(i,1)
               vm.updateQuoteCount()
                vm.$bus.$emit('success','Quote Successfully deleted')
            })
        }
    }
</script>

<style>
</style>
