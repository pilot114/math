<template>
    <h3>Math</h3>
    <div>
        <Plane :data="data"/>
    </div>
    <div>
        <div v-for="fn of fns" :key="fn">
            <input v-model="fn[1]" type="number">
            <input v-model="fn[0]" type="text">
        </div>
    </div>
</template>

<script>

import Plane from "./components/Plane";
import { evaluate } from 'mathjs';


export default {
    name: 'App',
    components: {
        Plane
    },
    created() {
        const fps = 24;
        setInterval(() => {
            this.tick = this.tick + 1
        }, 1000 / fps)
    },
    computed: {
        data() {
            return this.fns.map(f => {
                return {
                    name: f[0],
                    data: {...this.sequence(f[0], f[1])}
                }
            });
        },
    },
    data() {
        return {
            tick: 0,
            fns: [
                ['sin(x + t/5)', 100],
                ['cos(x)', 100],
                ['sin(x + t/4) + cos(x)', 100],
                ['sin(t/5)', 100],
            ],
        }
    },
    methods: {
        sequence(f, count) {
            const range = Array.from(Array(count).keys())
            return range.map((x,y) => {
                let r = 0
                try {
                    r = evaluate(f, {x, y, t: this.tick})
                } catch (e) {
                    console.log(e)
                }
                return r
            })
        },
    }
}
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
.row {
    display: flex;
}

.column {
    flex: 50%;
}
</style>
