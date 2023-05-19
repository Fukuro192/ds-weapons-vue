<script setup>
import { RouterLink } from 'vue-router';
import { ref } from 'vue';
function clickOnRouter(router_id) {
    document.getElementById(router_id).click();
}

let weapons = ref([]);
fetch("http://localhost:3001/api/weapons")
  .then(response => response.json())
  .then(data => weapons.value = data);
console.log("in WeaponsListView: ", weapons);
let query = ref('');
function findWeapons() {
  fetch("http://localhost:3001/api/weapons?name="+query.value)
  .then(response => response.json())
  .then(data => weapons.value = data);
}
</script>

<template>
    <div class="grid grid-cols-1 gap-0 px-20" style="margin: 0 auto;" v-if="weapons">
        <input placeholder="Search, Ex: Moonlight Greatsword" class="text-black mx-max" type="text" v-model="query" @keyup="findWeapons()">
        <ul class="overflow-x-hidden overflow-y-auto h-96">
            <li
                v-for="weapon in weapons" :key="weapon.id"
                @click="clickOnRouter(`weapon_detail_${weapon.id}`)"
            >
                <span>{{ weapon.id }}</span>
                <span>{{ weapon.name }}</span>
                <span>Atk: {{ weapon.attack.physical }}</span>
                <span>Def: {{ weapon.defence.physical }}</span>
                <RouterLink :id="`weapon_detail_${weapon.id}`" :to="`/details/${weapon.id}`"></RouterLink>
            </li>
        </ul>
    </div>
</template>

<style scoped>
ul {
    position: relative;
    width: 450px;
    margin: 0px auto 0;
    padding: 10px;
    box-sizing: border-box;
    background: rgba(0, 0, 0, .1);
}
ul li {
    display: flex;
    background: rgba(255, 255, 255, .1);
    padding: 10px 20px;
    margin: 5px 0;
    transition: 0.5s;
}
ul li span:nth-child(1) {
    width: 30px;
}
ul li span:nth-child(2) {
    width: 200px;
}
ul li span:nth-child(3) {
    width: 100px;
    text-align: center;
}
ul li span:nth-child(4) {
    width: 70px;
    text-align: center;
}
ul li:hover {
    transform: scale(1.06);
}
</style>