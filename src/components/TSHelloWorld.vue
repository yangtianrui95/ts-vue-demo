<template>
  <div class="container">
    <p>{{msg}}</p>
  </div>
</template>

<script lang="ts">
    import Vue from 'vue';
    import Component from "vue-class-component";

    @Component
    export default class TSHelloWorld extends Vue {

        msg: number = 123;
        intervalId: any;

        incrementMsg(): void {
            this.msg++;
        }

        mounted(): void {
            this.intervalId = setInterval(this.incrementMsg, 1000);
            console.log('TSHelloWorld mounted... intervalId is ', this.intervalId);
        }

        beforeDestroy(): void {
            clearInterval(this.intervalId);
        }

    }
</script>

<style scoped>

</style>
