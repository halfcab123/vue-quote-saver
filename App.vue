<template>
        <div style="margin-top: 1em" class="container">

            <div class="card card-primary text-dark bg-light">
                <div class="card-header">
                    Vue / Bootstrap 4
                </div>
                <div class="card-body">
                    <h3 style="margin-bottom: 0 !important" class="card-title">QuoteSaver v0.1</h3>
                    <p style="font-size: 0.9em; font-family: Arial" class="card-text">By: C.R.</p>
                    <new-quote></new-quote>
                </div>
            </div>
                <quote-grid></quote-grid>
        </div>
</template>

<script>
    import quoteGrid from './components/QuoteGrid.vue'
    import newQuote from './components/New.vue'

    export default {
        components: {
            quoteGrid: quoteGrid,
            newQuote: newQuote
        }
    }
</script>
