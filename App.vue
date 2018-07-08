<template>
        <div style="margin-top: 1em" class="container">
            <meter-bar :total-quotes="total" :max-quotes="max"></meter-bar>
            <div id="hero" class="card card-primary text-dark bg-light">
                <div class="card-header">
                    Vue / Bootstrap 4
                </div>
                <div class="card-body">
                    <h3 style="margin-bottom: 0 !important" class="card-title">QuoteSaver v0.1</h3>
                    <p style="font-size: 0.9em; font-family: Arial" class="card-text">By: C.R.</p>
                    <new-quote-input :total-quotes="total" :max-quotes="max"></new-quote-input>
                    <transition-group name="list" tag="alert-bar">
                        <template v-for="(msg,i) in msgs">
                            <alert-bar :key="i" :type="msg.type">{{msg.message}}</alert-bar>
                        </template>
                    </transition-group>
                </div>
            </div>
                <quote-grid></quote-grid>
        </div>
</template>

<script>
    import meterBar from './components/Header.vue'
    import quoteGrid from './components/QuoteGrid.vue'
    import newQuote from './components/New.vue'
    import alert from './components/Alert.vue'

    export default {
        data: function(){
            return {
                total: 2,
                max: 10,
                msgs: [],
                msgsLength: 0,
                blockPop: false
            }
        },
        components: {
            quoteGrid: quoteGrid,
            newQuoteInput: newQuote,
            meterBar: meterBar,
            alertBar: alert
        },
        methods: {
          msgPop: function(){
              const vm = this
              setTimeout(()=>vm.msgs.pop(),3000)
          }
        },
        mounted: function(){
            const vm = this
            this.$bus.$on('error',(msg)=>{
                vm.msgs.unshift({type: 'error',message: msg})
                this.msgPop()
            })
            this.$bus.$on('success',(msg)=>{
                vm.msgs.unshift({type: 'success',message: msg})
                this.msgPop()
            })
            this.$bus.$on('quote-count-changed',(count)=>{
                vm.total = count
            })
        }
    }
</script>

<style>
    #hero {
        overflow: hidden;
    }

    alert-bar {
        position: absolute;
        top: 100px;
        right: 50px;
        display: inline-block;
        margin-right: 10px;
    }
    .list-enter-active, .list-leave-active {
        transition: all 1s;
    }
    .list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
        opacity: 0;
        transform: translateY(30px);
    }
</style>
