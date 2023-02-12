<template>
    <div class="regular-button">
        {{ text }}
    </div>
</template>

<script>
export default {
    name: 'resumeButton',
    props: {
        text: String
    }
}
</script>