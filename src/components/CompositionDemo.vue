<template>
    <div class="container">
        <div>{{msg}}</div>
    </div>
</template>

<script lang="ts">
    import {createComponent, onBeforeUnmount, onMounted, reactive, SetupContext} from '@vue/composition-api'

    interface State {
        msg: number,
        intervalId?: any
    }

    const stateObj: State = {
        msg: 0,
        intervalId: 0
    };

    export default createComponent({
        setup(ctx: SetupContext) {
            // console.log('setup');
            const state = reactive(stateObj);
            onMounted(() => {
                state.intervalId = setInterval(() => state.msg++, 1000);
                // console.log('onMounted', state.intervalId)
            });

            onBeforeUnmount(()=>{
                clearInterval(state.intervalId);
            });
            return {state};
        }
    })
</script>

<style scoped>

</style>
