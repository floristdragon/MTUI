<template>
    <li
        v-if="noTouch"
        v-text="value"
        :class="[active ? 'active' : '']"
        @click.stop.prevent="$_onFocus">

    </li>
    <li v-else
        v-text="value"
        :class="[active ? 'active' : '']"
        @touchstart.stop.prevent="$_onFocus"
        @touchmove="$_onBlur"
        @touchend="$_onBlur"
        @touchcanel="$_onBlur"
        @click.stop.prevent="$_onFocus">
    </li>
</template>

<script>
const COMPONENT_NAME = 'mt-number-key'
export default {
    name: COMPONENT_NAME,
    props: {
        value: {
            type: [String, Number],
            default: ''
        },
        noTouch: {
            type: Boolean,
            default: false
        }
    },
    data() {
        return {
            active: false
        }
    },
    methods: {
        $_onFocus() {
            if (!this.noTouch) {
                this.active = true
            }
            this.$emit('press', this.value)
        },
        $_onBlur() {
            this.active = false
        }
    }
}
</script>

