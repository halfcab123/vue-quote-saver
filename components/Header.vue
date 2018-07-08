<template>
    <div class="progress">
        <div class="progress-bar"
             :class="[{'bg-success': totalQuotes < (0.7 * maxQuotes)},
                       {'bg-warning': totalQuotes > (0.7 * maxQuotes)
                                && totalQuotes < (0.9 * maxQuotes)},
                       {'bg-danger': totalQuotes >= (0.9 * maxQuotes)}]"
             role="progressbar"
             :style="{'width': progress + '%'}"
             :aria-valuenow="progress"
             aria-valuemin="0"
             aria-valuemax="100">
            <span :class="{'text-dark':(progress <= 8)}">{{ totalQuotes }} of {{ maxQuotes }} Quotes Used</span></div>
    </div>
</template>

<script>
    export default {
        props: ['totalQuotes','maxQuotes'],
        computed: {
            progress: function(){
                return this.totalQuotes/this.maxQuotes * 100
            }
        }
    }
</script>