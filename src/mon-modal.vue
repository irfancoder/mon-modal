<script>
export default /*#__PURE__*/ {
    name: 'MonModal', // vue component name
    props: {
        title: { type: String, required: false },
        titleClass: { type: String, required: false, default: 'mon-modal-title' },
        label: { type: String, required: false },
        labelClass: { type: String, required: false, default: '' },
        backdropClass: { type: String, required: false, default: 'mon-modal' },
        modalClass: { type: String, required: false, default: 'mon-modal-container' },
        headerClass: { type: String, required: false, default: 'mon-modal-header' },
        bodyClass: { type: String, required: false, default: 'mon-modal-body' },
        footerClass: { type: String, required: false, default: 'mon-modal-footer' },

        persistent: { type: Boolean, required: false, default: false },
        disableClickAway: { type: Boolean, required: false, default: false },
        disableEsc: { type: Boolean, required: false, default: false },
        openOnMount: { type: Boolean, required: false, default: false },

        enter: { type: String, required: false, default: 'mon-modal-enter' },
        enterActive: { type: String, required: false, default: 'mon-modal-enter-active' },
        enterTo: { type: String, required: false, default: 'mon-modal-enter-to' },
        leave: { type: String, required: false, default: 'mon-modal-leave' },
        leaveActive: { type: String, required: false, default: 'mon-modal-leave-active' },
        leaveTo: { type: String, required: false, default: 'mon-modal-leave-to' },
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
        <button v-if="label" :class="labelClass" @click="openModal">{{ label }}</button>

        <!-- Non-Persistent Modal -->
        <transition 
            v-if="!persistent"
            name="mon-modal" 
            :enter-class="enter"
            :enter-active-class="enterActive"
            :enter-to-class="enterTo"
            :leave-class="leave"
            :leave-active-class="leaveActive"
            :leave-to-class="leaveTo">
            <div :class="backdropClass" v-if="show" @click.self="!disableClickAway ? closeModal() : null">
                <div :class="modalClass">
                    <div>
                        <div v-if="!$scopedSlots.header" :class="headerClass">
                            <h4 :class="titleClass">{{ title }}</h4>
                            <button @click="closeModal">X</button>
                        </div>
                        <slot v-else name="header" :close="closeModal"></slot>
                    </div>

                    <slot v-if="!!$scopedSlots.custom" name="custom" :open="openModal" :close="closeModal"></slot>
                    <template v-else>
                        <div class="modal-mon-wrapper">
                            <div :class="bodyClass">
                                <slot name="body"></slot>
                            </div>
                            <div :class="footerClass">
                                <slot name="footer" :close="closeModal">
                                    <button class="btn btn-default" @click="closeModal">Close</button>
                                </slot>
                            </div>
                        </div>
                    </template>
                </div>
            </div>
        </transition>

        <!-- Persistent Modal -->
        <transition 
            v-else
            name="mon-modal"
            :enter-class="enter"
            :enter-active-class="enterActive"
            :enter-to-class="enterTo"
            :leave-class="leave"
            :leave-active-class="leaveActive"
            :leave-to-class="leaveTo">
            <div :class="backdropClass" v-show="show" @click.self="!disableClickAway ? closeModal() : null">
                <div :class="modalClass">
                    <div>
                        <div v-if="!$scopedSlots.header" :class="headerClass">
                            <h4 :class="titleClass">{{ title }}</h4>
                            <button @click="closeModal">X</button>
                        </div>
                        <slot v-else name="header" :close="closeModal"></slot>
                    </div>
                    <slot v-if="!!$scopedSlots.custom" name="custom" :open="openModal" :close="closeModal"></slot>
                    <template v-else>
                        <div class="modal-mon-wrapper">
                            <div :class="bodyClass">
                                <slot name="body"></slot>
                            </div>
                            <div :class="footerClass">
                                <slot name="footer" :close="closeModal">
                                    <button class="btn btn-default" @click="closeModal">Close</button>
                                </slot>
                            </div>
                        </div>
                    </template>
                </div>
            </div>
        </transition>
    </div>
</template>

<style scoped>
/* BASE */
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
    top: 15%;
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

.mon-modal-wrapper {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
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

/* TRANSITIONS */
.mon-modal-enter-active, .mon-modal-leave-active {
    transition: all;
    transition-timing-function: cubic-bezier(0, 0, 0.2, 1);
    transition-duration: 100ms;
}
.mon-modal-enter, .mon-modal-leave-to {
    opacity: 0;
    transform: translateY(-8px)
}
.mon-modal-enter-to, .mon-modal-leave {
    opacity: 1;
}
</style>
