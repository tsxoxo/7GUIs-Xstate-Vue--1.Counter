<script setup lang="ts">
import { useMachine } from '@xstate/vue'
import { counterMachine } from './counterMachine';
import { createBrowserInspector } from '@statelyai/inspect';

const { inspect } = createBrowserInspector({
  // Comment out the line below to start the inspector
  autoStart: false
});

const {  snapshot, send } = useMachine(counterMachine, {
  inspect
})
</script>

<template>
  <main>
    <p>{{ snapshot.context.count  }}</p>
    <br />
    <button @click="send({ type: 'increase' })">
      +1<br>
      <span>Increase count</span>
    </button>
  </main>
</template>

<style scoped>
main {
  padding: 2rem;
  background: white;
  border-radius: 0.05rem;
  box-shadow: .1rem .1rem 0 .1rem #07ac9b;
  width: 75vw;
  max-width: 40rem;
  display: flex;
  flex-direction: column;
  align-items: center; 
}
p {
  font-size: 6rem;
  font-weight: 600;
  color: var(--color-primary);
  text-align: center;
  margin: 0 0;
}
button {
  width: min-content;
  text-wrap: nowrap;
  appearance: none;
  color: white;
  border: none;
  padding: 1rem 1.5rem;
  border-radius: 0.05rem;
  font-size: 2rem;
  font-weight: bold;
  background-color: var(--color-primary);
}

button span {
  font-size: .6em;
}
</style>
