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
        <mon-modal title="hello" ref="helloworld">
            <template #trigger="{ open }">
                <button @click="open">jhasgdjhkasbdkjasbdkj</button>
            </template>
            <template #custom="{ open, close }">
                <div>
                    Lorem ipsum dolor sit amet consectet ur adipisicing elit. Praesentium qui ullam voluptates. Suscipit, corrupti odit obcaecati voluptatibus, non quisquam doloribus aut ut temporibus
                    ipsum quod repudiandae ducimus molestias iusto rerum! asdnjksadbnsakjnd
                </div>
                <div class="mon-modal-footer">
                    <button @click="close">close</button>
                    <button @click="open">open</button>
                </div>
            </template>
        </mon-modal>
        <button @click="$refs.helloworld.openModal()">hehehe</button>
    </div>
</template>
