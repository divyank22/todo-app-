<script setup>
import { ref } from 'vue';
import Importants from './Importants.vue';
import todoapp from './todoapp.vue';
const currentTab = ref('todoapp')
const navstart = "Todoapp"
const tabs = {
    todoapp: todoapp,
    Importants: Importants
}
</script>
<template>
    <nav>
        <ul>
            <h2 class="navst" >{{ navstart }}</h2>
            <li class="navsty" @click="currentTab = 'todoapp'">Todo</li>
            <li class="navsty"  @click="currentTab = 'Importants'">Importants</li>
        </ul>
    </nav>
    <component :is="tabs[currentTab]" />
</template>
<style scoped>
ul{
    margin: 0%;
    padding: 0%;
}
.navsty {
    display: inline;
    list-style: none;
    padding: 0vw 1vw;
    color: aliceblue;
}
.navst {
    font-size: 4ch;
    display: inline;
    list-style: none;
    padding: 0vw 1vw;
    color: aliceblue;
}
nav{
    background-color: black;
}

</style>