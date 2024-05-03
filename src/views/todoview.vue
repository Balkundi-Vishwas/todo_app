<template>
      <div class="home">
        <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
        <TodoApp/>
      </div>
</template>
    
    <script lang="ts">
    import { Options, Vue } from 'vue-class-component';
    import TodoApp from '@/components/TodoApp.vue'; // @ is an alias to /src
    
    @Options({
      components: {
        TodoApp,
      },
    })
    export default class todoview extends Vue {}
    </script>