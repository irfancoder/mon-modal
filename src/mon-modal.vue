<script>
export default /*#__PURE__*/ {
    name: 'MonModal', // vue component name
    props: {
        title: { type: String, default: 'Modal title' },
        label: { type: String, default: 'Button text' },
        labelClass: { type: String, required: false, default: '' },
        containerClass: { type: String, required: false, default: 'mon-modal-container' },
        headerClass: { type: String, required: false, default: 'mon-modal-header' },
        bodyClass: { type: String, required: false, default: 'mon-modal-body' },
        footerClass: { type: String, required: false, default: 'mon-modal-footer' },
        persistent: { type: Boolean, required: false, default: false },
        disableClickAway: { type: Boolean, required: false, default: false },
        disableEsc: { type: Boolean, required: false, default: false },
        openOnMount: { type: Boolean, required: false, default: false }
    },
    data() {
        return {
            show: false
        }
    },
    mounted() {
        if (this.openOnMount) this.openModal()
        if (!this.disableEsc) document.addEventListener('keydown', this.bindEscKey)
    },

    beforeDestroy() {
        if (!this.disableEsc) document.removeEventListener('keydown', this.bindEscKey)
    },

    methods: {
        openModal() {
            this.$emit('before-open')
            this.show = true
            this.$emit('after-open')
        },
        closeModal() {
            this.$emit('before-close')
            this.show = false
            this.$emit('after-close')
        },
        bindEscKey: function(event) {
            if (this.show === true && event.keyCode === 27) this.closeModal()
        }
    }
}
</script>

<template>
    <div>
        <!-- Button / Trigger Slot -->
        <slot name="trigger" :open="openModal"></slot>
        <button v-if="!$slots.trigger" :class="labelClass" @click="openModal">{{ label }}</button>

        <!-- Non-Persistent Modal -->
        <transition name="mon-modal" v-if="!persistent">
            <div class="mon-modal" v-if="show" @click.self="!disableClickAway ? closeModal() : null">
                <div :class="containerClass">
                    <div :class="headerClass">
                        <h4 class="mon-modal-title">{{ title }}</h4>
                        <button @click="closeModal">X</button>
                        <slot name="header"></slot>
                    </div>

                    <slot v-if="!!$slots.content" name="content" :open="openModal" :close="closeModal"></slot>
                    <template v-else>
                        <div :class="bodyClass">
                            <slot name="body"></slot>
                        </div>
                        <div :class="footerClass">
                            <slot name="footer" :close="closeModal">
                                <button class="btn btn-default" @click="closeModal">Close</button>
                            </slot>
                        </div>
                    </template>
                </div>
            </div>
        </transition>

        <!-- Persistent Modal -->
        <transition name="mon-modal" v-else>
            <div class="mon-modal" v-show="show" @click.self="!disableClickAway ? closeModal() : null">
                <div :class="containerClass">
                    <div :class="headerClass">
                        <h4 class="mon-modal-title">{{ title }}</h4>
                        <button @click="closeModal">X</button>
                        <slot name="header"></slot>
                    </div>

                    <slot v-if="!!$slots.content" name="content" :open="openModal" :close="closeModal"></slot>
                    <template v-else>
                        <div :class="bodyClass">
                            <slot name="body"></slot>
                        </div>
                        <div :class="footerClass">
                            <slot name="footer" :close="closeModal">
                                <button class="btn btn-default" @click="closeModal">Close</button>
                            </slot>
                        </div>
                    </template>
                </div>
            </div>
        </transition>
    </div>
</template>

<style scoped>
.mon-modal {
    position: fixed;
    background: rgba(0, 0, 0, 0.4);
    width: 100%;
    height: 100%;
    z-index: 10;
    top: 0;
    left: 0;
    display: flex;
    justify-content: center;
}

.mon-modal-container {
    position: absolute;
    top: 20%;
    background: white;
    width: 90%;
    max-width: 32rem;
    max-height: 60%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}

.mon-modal-header {
    padding: 1rem 1.25rem;
    border-bottom-width: 1px;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
}

.mon-modal-title {
    margin: 0;
}

.mon-modal-body {
    padding: 1rem 1.25rem;
    overflow: auto;
}

.mon-modal-footer {
    display: flex;
    flex-direction: row;
    justify-content: flex-end;
    padding: 1rem 1.25rem;
}
</style>
