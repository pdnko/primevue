<template>
    <DocSectionText v-bind="$attrs">
        <p>A simple Card is created with a <i>title</i> property along with the content as children.</p>
    </DocSectionText>
    <div class="mb-4 p-8">
        <Card>
            <template #title>Simple Card</template>
            <template #content>
                <p class="!m-0">
                    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Inventore sed consequuntur error repudiandae numquam deserunt quisquam repellat libero asperiores earum nam nobis, culpa ratione quam perferendis esse, cupiditate neque
                    quas!
                </p>
            </template>
        </Card>
    </div>
    <DocSectionCode :code="code" />
</template>

<script setup lang="ts">
import Card from '@/volt/Card.vue';
import { ref } from 'vue';

const code = ref(`
<template>
    <Card>
        <template #title>Simple Card</template>
        <template #content>
            <p>
                Lorem ipsum dolor sit amet, consectetur adipisicing elit. Inventore sed consequuntur error repudiandae numquam deserunt quisquam repellat libero asperiores earum nam nobis, culpa ratione quam perferendis esse, cupiditate neque
                quas!
            </p>
        </template>
    </Card>
</template>

<script setup lang="ts">
import Card from '@/volt/Card.vue';
<\/script>
`);
</script>
