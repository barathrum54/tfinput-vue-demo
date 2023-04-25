<template>
    <div class="input-wrapper" :class="{ [sizeClass]: true, [darkModeClass]: true }">
        <div class="input-title">
            <slot name="input-title">{{ props.title }}</slot>
        </div>
        <div :class="{ 'tf-input': true, [borderRadiusClass]: true, [stateClass]: true, [darkModeClass]: true }">
            <img class="icon pre-icon" src="../assets/search.svg" alt="">
            <input type="text" v-bind="options" />
            <img class="icon suffix-icon" :src="suffixIconSrc" alt="">
        </div>
        <div class="input-description">
            <slot name="input-description">{{ props.description }}</slot>
        </div>
    </div>
</template>
  
<script setup lang="ts">
import { ref, defineProps, defineEmits, computed } from 'vue';

const props = defineProps({
    title: {
        type: String,
    },
    description: {
        type: String,
    },
    placeholder: {
        type: String,
        default: 'Enter your text',
    },
    dark: {
        type: String,
        default: 'false'
    },
    borderRadius: {
        type: String,
        default: 'Full',
    },
    state: {
        type: String,
    },
    size: {
        type: String,
    }
});
const emit = defineEmits(['update:modelValue', 'update:modelState']);

const stateClass = computed(() => {
    return props.state as string
});
const sizeClass = computed(() => {
    return props.size as string
});
const currentState = ref('default')

const darkModeClass = computed(() => {
    return props.dark == 'true' ? 'dark' : '';
});

const borderRadiusClass = computed(() => {
    switch (props.borderRadius) {
        case 'Normal':
            return 'border-radius-normal';
        case 'Rounded':
            return 'border-radius-rounded';
        case 'Full':
            return 'border-radius-full';
        default:
            return 'border-radius-normal';
    }
});
const suffixIconSrc = computed(() => {
    let res = "";
    switch (stateClass.value) {
        case 'default':
            res = require('../assets/times.svg');
            break;
        case 'active':
            res = require('../assets/times.svg');
            break;
        case 'filled':
            res = require('../assets/times.svg');
            break;
        case 'warning':
            res = require('../assets/warning.svg');
            break;
        case 'danger':
            res = require('../assets/danger.svg');
            break;
        case 'success':
            res = require('../assets/success.svg');
            break;
        case 'disabled':
            res = require('../assets/disabled.svg');
            break;

        default:

            break;
    }
    console.log(currentState.value)
    return res;
})
const handleBlur = (event: FocusEvent) => {
    const target = event.target as HTMLInputElement;
    currentState.value = target.value ? 'filled' : 'default';
    emit('update:modelState', currentState.value);

};

const handleFocus = () => {
    currentState.value = 'active';
    emit('update:modelState', 'active');

};
const handleInput = (event: InputEvent) => {
    const target = event.target as HTMLInputElement;
    emit('update:modelValue', target.value);
};
const options = {
    placeholder: props.placeholder,
    onFocus: handleFocus,
    onBlur: handleBlur,
    onInput: handleInput,
};
</script>
  
<style lang="scss" scoped>
.input-wrapper {
    display: flex;
    flex-flow: column;
    align-items: start;
    gap: 8px;
    $t: &;

    &:not(.dark) {

        & .input-title {
            color: #4B5563;
        }


    }

    &.dark {
        & .input-title {
            color: #9CA3AF;
        }


    }

    .tf-input {
        &.border-radius-normal {
            border-radius: 0;
        }

        &.border-radius-rounded {
            border-radius: 6px;
        }

        &.border-radius-full {
            border-radius: 100px;
        }

    }

    .tf-input.default {
        &:not(.dark) {
            &+.input-description {
                color: #9CA3AF;
            }

            &,
            & * {
                color: #9CA3AF;
                background-color: #F9FAFB;
            }

        }

        &.dark {
            &+.input-description {
                color: #4B5563;
            }

            &,
            & * {
                color: #4B5563;
                background-color: #111827;
            }

        }


    }

    .tf-input.active {
        border-color: #3b82f6;
        box-shadow: 0 0 0 2px rgba(59, 130, 246, 0.4);

        &:not(.dark) {
            &+.input-description {
                color: #4B5563;
            }

            &,
            & * {

                color: #4B5563;
                background-color: #F9FAFB;
            }

        }

        &.dark {
            &+.input-description {
                color: #D1D5DB;
            }

            &,
            & * {
                color: #D1D5DB;
                background-color: #111827;
            }

        }

    }

    .tf-input.filled {
        border-color: #e5e7eb;

        &:not(.dark) {
            &+.input-description {
                color: #4B5563;
            }

            &,
            & * {

                color: #4B5563;
                background-color: #F9FAFB;
            }

        }

        &.dark {
            &+.input-description {
                color: #D1D5DB;
            }

            &,
            & * {
                color: #D1D5DB;
                background-color: #111827;
            }

        }
    }

    .tf-input.warning {
        border-color: #eab308;
        box-shadow: 0 0 0 2px rgba(234, 179, 8, 0.4);

        &:not(.dark) {
            &+.input-description {
                color: #eab308;
            }

            &,
            & * {

                color: #4B5563;
                background-color: #F9FAFB;
            }

        }

        &.dark {
            &+.input-description {
                color: #eab308;
            }

            &,
            & * {
                color: #D1D5DB;
                background-color: #111827;
            }

        }
    }

    .tf-input.danger {
        border-color: #ef4444;
        box-shadow: 0 0 0 2px rgba(239, 68, 68, 0.4);

        &:not(.dark) {
            &+.input-description {
                color: #ef4444;
            }

            &,
            & * {

                color: #4B5563;
                background-color: #F9FAFB;
            }

        }

        &.dark {
            &+.input-description {
                color: #ef4444;
            }

            &,
            & * {
                color: #D1D5DB;
                background-color: #111827;
            }

        }
    }

    .tf-input.success {
        border-color: #22c55e;
        box-shadow: 0 0 0 2px rgba(34, 197, 94, 0.4);

        &:not(.dark) {
            &+.input-description {
                color: #22c55e;
            }

            &,
            & * {

                color: #4B5563;
                background-color: #F9FAFB;
            }

        }

        &.dark {
            &+.input-description {
                color: #22c55e;
            }

            &,
            & * {
                color: #D1D5DB;
                background-color: #111827;
            }

        }
    }

    .tf-input.disabled {
        border-color: #e5e7eb;
        cursor: not-allowed;
        background-color: #f3f4f6;

        &:not(.dark) {
            &+.input-description {
                color: #D1D5DB;
            }

            &,
            & * {

                color: #D1D5DB;
                background-color: #F3F4F6;
            }

        }

        &.dark {
            &+.input-description {
                color: #374151;
            }

            &,
            & * {
                color: #374151;
                background-color: #1F2937;
            }

        }
    }




    &.XSM {
        .tf-input {
            padding: 7px;
            gap: 6px;

            input {
                font-size: 12px;
                line-height: 16px;
            }
        }

        .input-title,
        .input-description {
            font-size: 12px;
            line-height: 16px;
        }

    }

    &.SM {
        .tf-input {
            padding: 9px;
            gap: 9px;

            .pre-icon,
            .suffix-icon {
                height: 10px;
                width: 10px;
            }

            input {
                font-size: 14px;
                line-height: 20px;
            }
        }


        .input-title,
        .input-description {
            font-size: 12px;
            line-height: 16px;
        }
    }

    &.MD {
        .tf-input {
            padding: 11px;
            gap: 12px;

            .pre-icon,
            .suffix-icon {
                height: 17px;
                width: 17px;
            }

            input {
                font-size: 16px;
                line-height: 24px;

            }
        }


        .input-title,
        .input-description {
            font-size: 14px;
            line-height: 20px;
        }
    }

    &.LG {
        .tf-input {
            padding: 11px;
            gap: 12px;

            .pre-icon,
            .suffix-icon {
                height: 17px;
                width: 17px;
            }

            input {
                font-size: 18px;
                line-height: 28px;
            }
        }


        .input-title,
        .input-description {
            font-size: 14px;
            line-height: 20px;
        }
    }

    &.XLG {
        .tf-input {
            padding: 14px;
            gap: 14px;

            .pre-icon,
            .suffix-icon {
                height: 20px;
                width: 20px;
            }

            input {
                font-size: 20px;
                line-height: 32px;

            }
        }



        .input-title,
        .input-description {
            font-size: 16px;
            line-height: 24px;
        }
    }

    .tf-input {

        min-width: 302px;
        display: flex;
        align-items: center;
        border: 1px solid #e5e7eb;
        position: relative;

        .icon {
            height: 10px;
            width: 10px;
        }

        input {
            width: 100%;
            font-size: 14px;
            line-height: 24px;
            background-color: transparent;
            border: none;
            outline: none;
        }

    }
}
</style>
  