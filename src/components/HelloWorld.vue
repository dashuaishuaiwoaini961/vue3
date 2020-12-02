<template>
    <h1>{{ msg }}</h1>
    <button @click="add">count is: {{ state.count }}</button>
    <p>Edit <code>components/HelloWorld.vue</code> to test hot module replacement.</p>
    <div id-="slot"></div>
</template>

<script lang='ts'>
import {
    ref,
    defineComponent,
    computed,
    onMounted,
    getCurrentInstance,
    onUnmounted,
    createApp,
    h,
    reactive,
    render,
    onUpdated
} from 'vue';
export default {
    name: 'HelloWorld',
    props: {
        msg: String
    },
    setup() {
        onMounted(() => {
            console.log('onMounted');
        });
        onUpdated(() => {
            console.log('onUpdated');
        });
        onUnmounted(() => {
            console.log('onUnmounted');
        });
        const state = reactive({
            count: 1
        });
        // let count = ref(1);
        const add = () => {
            state.count++;
        };
        return {
            state,
            add
        };
    }
};
</script>
