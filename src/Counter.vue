<script setup lang="ts">
import { useMachine } from '@xstate/vue'
import { counterMachine } from './counterMachine';
import { createBrowserInspector } from '@statelyai/inspect';

const { inspect } = createBrowserInspector({
  // Comment out the line below to start the inspector
  // autoStart: false
});

const {  snapshot, send } = useMachine(counterMachine, {
  inspect
})
</script>

<template>
  <div>
    <em>{{ snapshot.context.count  }}</em>
    <br />
    <button @click="send({ type: 'increase' })">
      + Increase counter
    </button>
  </div>
</template>

<style scoped>
.step {
  padding: 2rem;
  background: white;
  border-radius: 1rem;
  box-shadow: 0 .5rem 1rem #0001;
  width: 75vw;
  max-width: 40rem;
}

.feedback>.close-button {
  position: absolute;
  top: 0;
  right: 0;
  z-index: 1;
}

.button {
  appearance: none;
  color: white;
  border: none;
  padding: 1rem 1.5rem;
  border-radius: 0.25rem;
  font-size: inherit;
  font-weight: bold;
  margin-right: 1rem;
  background-color: var(--color-primary);
}

.button:disabled {
  cursor: not-allowed;
  opacity: 0.5;
}

.close-button {
  appearance: none;
  background: transparent;
  border: none;
  padding: 1rem;
}
</style>
