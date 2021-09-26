<script>
import Vue from 'vue'
import MonModal from '@/mon-modal.vue'

export default Vue.extend({
    name: 'ServeDev',
    components: {
        MonModal
    }
})
</script>

<template>
    <div id="app">
        <mon-modal label="hello" title="hello" />
    </div>
</template>
