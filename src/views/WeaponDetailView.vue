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
      .then(data => (this.weapon = data));
  }
};
</script>

<template>
    <main>
        <div style="margin: auto auto;">
            <WelcomeItem>
                <h2 class="text-2xl">{{ weapon }}</h2>
                <p>
                    Attack:
                    
                </p>
            </WelcomeItem>
        </div>
    </main>
</template>
