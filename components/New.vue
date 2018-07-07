<template>
    <div>
                <label>New Quote:</label><br>
        <textarea style="width: 400px; height: 100px" @keydown.enter="$bus.$emit('new-quote', $event.target.value)"></textarea>
    </div>
</template>

