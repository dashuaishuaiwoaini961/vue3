<template>
    <!-- <h1>{{ msg }}</h1> -->
    <!-- <button @click="add">count is: {{ state.count }}</button> -->
    <p>Edit <code>components/HelloWorld.vue</code> to test hot module replacement.</p>
    <div id-="slot"></div>
    <button @click="showToast" class="btn">打开 toast</button>
    <!-- 传送门 -->
    <teleport to="#teleport-target">
        <div v-if="visible" class="toast-wrap">
            <div class="toast-msg">我是一个 Toast 文案</div>
        </div>
    </teleport>
</template>

<script lang='ts'>
import {
    ref,
    defineComponent,
    computed,
    onMounted,
    onUnmounted,
    reactive,
    onUpdated,
    watch,
    watchEffect,
    isReactive,
    toRefs,
    customRef,
    shallowRef,
    triggerRef
} from 'vue'
// interface State {
//     count: number;
//     double?: number;
// }
function useDebouncedRef(value: string, delay: number = 2000) {
    let timeout: any
    return customRef((track, trigger) => {
        return {
            get() {
                track()
                return value
            },
            set(newValue: string) {
                clearTimeout(timeout)
                timeout = setTimeout(() => {
                    value = newValue
                    trigger()
                }, delay)
            }
        }
    })
}
export default defineComponent({
    name: 'HelloWorld',
    props: {
        msg: String
    },
    setup() {
        const visible = ref(false)
        let timer: any
        const showToast = () => {
            visible.value = true
            clearTimeout(timer)
            timer = setTimeout(() => {
                visible.value = false
            }, 2000)
        }
        onMounted(() => {
            console.log('onMounted')
        })
        onUpdated(() => {
            console.log('onUpdated')
        })
        onUnmounted(() => {
            console.log('onUnmounted')
        })
        // const internalInstance = getCurrentInstance();
        // console.log(internalInstance.props);
        // const state = reactive<State>({
        //     count: 1
        // });
        // let count1 = ref(1);
        // console.log(isReactive(state));
        // const refState = toRefs(state);
        // refState.count.value = 5;
        // console.log(222, state.count);

        // const add = () => {
        //     state.count++;
        // };

        // const double = computed(() => state.count * 2);
        // console.log(double);

        // watch(
        //     () => state.count,
        //     (val, preVal) => {
        //         console.log('val, preVal', val, preVal);
        //     }
        // );

        // Runs a function immediately while reactively tracking its dependencies and re-runs it whenever the dependencies are changed.
        // watchEffect(() => {
        //     console.log('watchEffect', state.count);
        // });

        // return {
        //     state,
        //     add
        // };
        return {
            text: useDebouncedRef(''),
            showToast,
            visible
        }
    }
})
</script>
