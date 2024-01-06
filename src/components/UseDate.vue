<template>
  <div class="date-display">
    Today's date is: {{ formattedDateTime }}
  </div>
</template>

<script>
import { useDateNow } from 'vue-composable';
import { ref, watchEffect } from 'vue';

export default {
  setup() {
    // useDateNow provides a reactive timestamp
    const { now } = useDateNow();

    // Use a ref to store the formatted date
    const formattedDateTime = ref('');

    // Use watchEffect to reactively update the formatted date when 'now' changes
    watchEffect(() => {
      const date = new Date(now.value);
      formattedDateTime.value = date.toLocaleDateString(undefined, {
        year: 'numeric', month: 'long', day: 'numeric',
        hour: 'numeric', minute: 'numeric', second: 'numeric', hour12: true
      });
    });

    return { formattedDateTime };
  }
}
</script>


<style>
:root {
  --color-white: #ffffff;
  --color-purple-light: #713FF2;
  --color-purple-dark: #535099;
}

.date-display {
  background-color: var(--color-purple-light);
  display: flex;
  justify-content: center;
  align-items: center;
  color: var(--color-white);
  height: 100vh;
  font-size: 1.5em;
  font-weight: bold;
  text-align: center;
}

@media (max-width: 768px) {
  .date-display {
    font-size: 1.2em;
    padding: 15px;
  }
}
</style>