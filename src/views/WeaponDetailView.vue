<script>
import WelcomeItem from '@/components/WelcomeItem.vue'
import { useRoute } from 'vue-router';
export default {
  name: "weapon-detail-view",
  components: { WelcomeItem },
  data() {
    return {
        weapon: null
    };
  },
  created() {
    // Simple GET request using fetch
    fetch("http://localhost:3001/api/weapons/" + useRoute().params.weapon_id)
      .then(response => response.json())
      .then(data => {
        this.weapon = data
        console.log(this.weapon)
      });
  },
  computed: {
    isEffectsEmpty() {
        return Object.values(this.weapon.effects).every(x => (x === null || x === ''));
    }
  }
};
</script>

<template>
    <main>
        <div style="margin: auto auto;">
            <WelcomeItem v-if="weapon">
                <h2 class="text-2xl">{{ weapon.name }}</h2>
                <div class="grid grid-cols-2 gap-4">
                    <p>
                        Attack:
                        <ul class="list-disc pl-12">
                            <li>Physical: {{ weapon.attack.physical }}</li>
                            <li>Magic: {{ weapon.attack.magic }}</li>
                            <li>Fire: {{ weapon.attack.fire }}</li>
                            <li>Lightning: {{ weapon.attack.lightning }}</li>
                            <li>Bonus: {{ weapon.attack.bonus }}</li>
                        </ul>
                    </p>
                    <p>
                        Defence:
                        <ul class="list-disc pl-12">
                            <li>Physical: {{ weapon.defence.physical }}</li>
                            <li>Magic: {{ weapon.defence.magic }}</li>
                            <li>Fire: {{ weapon.defence.fire }}</li>
                            <li>Lightning: {{ weapon.defence.lightning }}</li>
                            <li>Bonus: {{ weapon.defence.bonus }}</li>
                        </ul>
                    </p>
                    <p v-if="!isEffectsEmpty">
                        Effects:
                        <ul class="list-disc pl-12">
                            <li v-if="weapon.effects.poison">Poison: {{ weapon.effects.poison }}</li>
                            <li v-if="weapon.effects.bleed">Bleed: {{ weapon.effects.bleed }}</li>
                            <li v-if="weapon.effects.divine">Divine: {{ weapon.effects.divine }}</li>
                            <li v-if="weapon.effects.occult">Occult: {{ weapon.effects.occult }}</li>
                        </ul>
                    </p>
                    <p>
                        Requirements:
                        <ul class="list-disc pl-12">
                            <li v-if="weapon.req.strength">Strength: {{ weapon.req.strength }}</li>
                            <li v-if="weapon.req.dexterity">Dexterity: {{ weapon.req.dexterity }}</li>
                            <li v-if="weapon.req.intelligence">Intelligence: {{ weapon.req.intelligence }}</li>
                            <li v-if="weapon.req.faith">Faith: {{ weapon.req.faith }}</li>
                        </ul>
                    </p>
                    <p>
                        Scale:
                        <ul class="list-disc pl-12">
                            <li v-if="weapon.scale.strength">Strength: {{ weapon.scale.strength }}</li>
                            <li v-if="weapon.scale.dexterity">Dexterity: {{ weapon.scale.dexterity }}</li>
                            <li v-if="weapon.scale.intelligence">Intelligence: {{ weapon.scale.intelligence }}</li>
                            <li v-if="weapon.scale.faith">Faith: {{ weapon.scale.faith }}</li>
                        </ul>
                    </p>
                </div>
            </WelcomeItem>
        </div>
    </main>
</template>
