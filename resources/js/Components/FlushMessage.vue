<script setup>

</script>
<template>
    <div v-if="$page.props.flash.status == 'success'" class="bg-green-400 text-white">
        {{ $page.props.flash.message }}
    </div>

    <div v-if="$page.props.flash.status == 'danger'" class="bg-red-400 text-white">
        {{ $page.props.flash.message }}
    </div>
</template>
