<template>
    <div class="xr-input" :class="[error ? 'xr-input--error' : '']">
        <!-- change 是原生事件，$event 是浏览器给的原生事件值 -->
        <input
            type="text"
            :value="value"
            :disabled="disabled"
            :readonly="readonly"
            @change="$emit('change', $event.target.value)"
            @input="$emit('input', $event.target.value)"
            @focus="$emit('focus', $event.target.value)"
            @blur="$emit('blur', $event.target.value)">
        <template v-if="error">
            <xr-icon name="error" class="xr-input__erricon"></xr-icon>
            <span class="xr-input__errmsg">{{error}}</span> 
        </template>
    </div>
</template>
<script>
import XrIcon from './icon';
export default {
    name: 'XrInput',
    components: {
        XrIcon
    },
    props: {
        value: {
            type: String,
            default: ''
        },
        disabled: {
            type: Boolean,
            default: false
        },
        readonly: {
            type: Boolean,
            default: false
        },
        error: {
            type: String,
            default: ''
        },

    }
}
</script>
<style lang="scss" scoped>
@import "./style/var.scss";
.xr-input {
    display: inline-flex;
    align-items: center;
    font-size: $font-size;
    > input {
        padding: 0 8px;
        height: $default-height;
        border: 1px solid $border-color;
        border-radius: $border-radius;
        font-size: inherit;
        &:hover {
            border: 1px solid $border-color-hover;
        }
        &:focus {
            outline: none;
            box-shadow: inset 0 1px 3px $box-shadow-color;
        }
        &[disabled], &[readonly]{
            border-color: #bbb;
            color: #bbb;
            cursor: not-allowed;
        }
    }
    &--error {
        > input {
            border-color: $red;
            color: $red;
        }
        .xr-input__erricon {
            fill: $red;
        }
        .xr-input__errmsg {
            color: $red;
        }
    }
    > :not(:last-child) {
        margin-right: .5em;
    }
}
</style>