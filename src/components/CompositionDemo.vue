<template>
  <div class="container">
    <h1>{{title}}</h1>
    <div>{{state.msg}}</div>
  </div>
</template>

<script lang="ts">
    import {
        computed,
        createComponent,
        onBeforeUnmount,
        onMounted,
        reactive, Ref,
        SetupContext,
        toRefs,
        watch
    } from '@vue/composition-api'

    interface State2 {
        title: string,
        subtitle: string,
        date: string,
    }

    function changeTitleRandom(ctx: SetupContext): any {
        const state2 = reactive({title: 'mytitle', subtitle: 'subtitle', date: String(Date.now())});

        watch(() => {
            console.log('watch date is ' + state2.date)
        });

        let isInitial: Ref<Readonly<boolean>> = computed(() => {
            return state2.title === 'mytitle';
        });
        onMounted(() => {
            console.log('isInitial ' + isInitial.value);
            setInterval(() => {
                state2.date = String(Date.now());
                state2.title = state2.date;
            }, 3000);
        });
        return {state2, isInitial};
    }

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

            onBeforeUnmount(() => {
                clearInterval(state.intervalId);
            });
            const {state2, isInitial} = changeTitleRandom(ctx);
            // @ts-ignore
            return {state, ...toRefs(state2), isInitial};
        }
    })
</script>

<style scoped>

</style>
