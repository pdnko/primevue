<template>
    <DocSectionText v-bind="$attrs">
        <p>Icons and Labels can be customized using <i>onLabel</i>, <i>offLabel</i>, <i>onIcon</i> and <i>offIcon</i> properties.</p>
    </DocSectionText>
    <div class="card flex justify-center">
        <ToggleButton v-model="checked" onLabel="Locked" offLabel="Unlocked" onIcon="pi pi-lock" offIcon="pi pi-lock-open" class="w-36" aria-label="Do you confirm" />
    </div>
    <DocSectionCode :code="code" />
</template>

<script setup lang="ts">
import ToggleButton from '@/volt/ToggleButton.vue';
import { ref } from 'vue';

const checked = ref(false);

const code = ref(`
<template>
    <div class="card flex justify-center">
        <ToggleButton v-model="checked" onLabel="Locked" offLabel="Unlocked" onIcon="pi pi-lock" offIcon="pi pi-lock-open" class="w-36" aria-label="Do you confirm" />
    </div>
</template>

<script setup lang="ts">
import ToggleButton from '@/volt/ToggleButton.vue';
import { ref } from 'vue';

const checked = ref(false);
<\/script>
`);
</script>
