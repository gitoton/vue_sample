<template>
    <h1>Vue 3</h1>
    <!-- <p> 1 + 1 = {{ answer }}</p>
    <p v-text="message" v-bind:style="{'backgroundColor': welcomeColor, 'color': 'white' }"></p>
    お名前は: <input type="text" size="30" v-model="myname">
    <p v-html="myname"></p> -->
    <input type="text" size="30" v-model="number">
    <button @click="add()">+1</button>
    <br>
    <input type="text" size="30" v-model="newTodo">
    <button @click="addTodo()">追加</button>
    <li v-for="(todo, i) in todos" v-bind:key="i"> {{ i }}. {{ todo }}</li>
</template>

<script setup>
    // import { computed } from 'vue';
    import { ref } from 'vue';
    // const answer = computed(() => {
    //     return 1 + 3
    // })
    // // const message = ref("ようこそ <strong>ゆうき</strong>さん")
    // const welcomeColor = ref("blue")
    // const myname = ref("")
    // const message = computed(() => {
    //     return 'ようこそ<strong>' + myname.value + '</strong>さん'
    // })

    const number = ref(0)

    const add = () => {
        number.value++
    }

    const todos = ref([])
    const newTodo = ref('')

    const addTodo = () => {
        todos.value.push(newTodo.value)
    }
</script>