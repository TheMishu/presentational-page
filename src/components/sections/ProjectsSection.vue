<script lang="ts">
import type { PrismicDocument } from '@prismicio/types'
import { from } from 'rxjs'
import { defineComponent } from 'vue'
import ArrowStraightVue from '../iconWrappers/ArrowStraight.vue'


export default defineComponent({
    components: {
      ArrowStraightVue,
    },
    data() {
        return {
            document: null as null | PrismicDocument<any>
        };
    },
    created() {
        from(this.$prismic.client.getByUID("repo", "lorem-ipsum")).subscribe({
            next: (v) => this.document = v
        });
    },
})
</script>

<template>
    <ArrowStraightVue label="About Me" pointing="up"/>
    <section>
        <h2>projekciki</h2>
        <PrismicRichText :field="document?.data.project_name"></PrismicRichText>
    </section>
    <section>
        <h2>Tech stack</h2>
        <ul>
            <li>Typescript</li>
            <li>Angular</li>
            <li>RxJs</li>
            <li>LESS/Sass</li>
            <li>Vue3</li>
            <li>Python</li>
        </ul>
    </section>
    <ArrowStraightVue label="Contact" pointing="down"/>
</template>
