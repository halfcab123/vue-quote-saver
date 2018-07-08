<template>
    <div>

        <label>New Quote:</label><br>
        <textarea ref="newQuote"
                  v-model="quoteArea"
                  style="width: 400px; height: 100px"
                  placeholder="Input a quote"></textarea><br>
        <input ref="newAuthor"
               v-model="authorText"
               type="text"
               style="width: 400px"
               placeholder="Input an author"><br>
        <button :disabled="buttonDisabled"
                style="margin-top: 0.5em;width: 100px"
                @click="emitQuote()"
                class="btn"
                :class="{'btn-primary':!buttonDisabled,
                        'btn-secondary':buttonDisabled}">Save</button>

    </div>
</template>

<script>
    export default {
        props: ['totalQuotes','maxQuotes'],
        data: function() {
            return {
                quoteArea: '',
                authorText: ''
            }
        },
        computed: {
          buttonDisabled: function(){
              const inputReady = this.quoteArea && this.authorText
              return !inputReady
          }
        },
        methods: {
            emitQuote: function(){
                const quote = this.$refs.newQuote.value
                const author = this.$refs.newAuthor.value

                if(this.totalQuotes < this.maxQuotes) {
                    this.$bus.$emit('new-quote', { quote:quote, author:author} )
                }else{
                    this.$bus.$emit('error','You have reached your quote limit')
                }
                this.quoteArea = ''
                this.authorText = ''
            }
        }
    }
</script>

<style>
    .btn.btn-secondary {
        opacity: 0.3;
    }
</style>