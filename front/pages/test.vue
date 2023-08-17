<template>
  <div class="test">
    <h1>Statistiques du joueur pour CS:GO</h1>
    <div class="display">
      <cards-player v-if="isDataLoaded" :playerData="playerData" :playerStats="transformStats(playerStats.playerstats.stats)"/>
      <cards-player-faceit v-if="statsData && statsData.lifetime" :playerData="playerData" :playerStats="statsData" />
    </div>
    <!-- <button @click="fetchPlayerStatsByNickname">Obtenir les stats pour Kamikaz25</button> -->
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import axios from 'axios';

const steamid = ref('76561197992709103');  // Remplacez par la valeur de votre choix ou liez-la à un élément de votre UI
const playerStats = ref({});
const isDataLoaded = ref(false);
const statsData = ref({});

const transformStats = (statsArray) => {
  const obj = {};
  for (let stat of statsArray) {
    obj[stat.name] = stat.value;
  }
  return obj;
};

const getStats = async () => {
  
  try {
    const response = await axios.get(`http://localhost:3001/api/getStatPlayer?steamid=${steamid.value}`);
    playerStats.value = response.data;
    isDataLoaded.value = true;
  } catch (error) {
    console.error("Erreur lors de la récupération des stats du joueur:", error);
  }
};
const playerData = ref({
  pseudo: '',
  playerImage: '',
  profileUrl: ''
});

const getPlayerData = async () => {
  try {
    const response = await axios.get(`http://localhost:3001/api/steam?steamids=${steamid.value}`);
    const playerInfo = response.data.response.players[0].player[0];  // Accéder à l'information correcte du joueur
    const pseudo = playerInfo.personaname[0]; // Accéder au premier élément du tableau personaname
    const playerImage = playerInfo.avatarfull[0]; // Accéder au premier élément du tableau avatarfull
    const playerProfileurl = playerInfo.profileurl[0]; // Accéder au premier élément du tableau avatarfull


    playerData.value.pseudo = pseudo;
    playerData.value.playerImage = playerImage;
    playerData.value.profileUrl = playerProfileurl;
    
  } catch (error) {
    console.error("Erreur lors de la récupération des données du joueur:", error);
  }
};

async function getPlayerInformation(nickname) {
  try {
    // Récupérer l'ID du joueur à partir de son pseudo
    const response = await fetch(`http://localhost:3001/api/faceit?nickname=${nickname}`);
    const data = await response.json();
    console.log('data',data);    
    return data;

  } catch (error) {
    console.error("Failed to fetch player stats:", error);
    return null;
  }
}

async function getPlayerStatsByNickname(nickname) {
  try {
    const playerInfo = await getPlayerInformation(nickname);
    if (!playerInfo || !playerInfo.player_id) {
      throw new Error("Player ID not found");
    }
    const playerId = playerInfo.player_id;

    const response = await fetch(`http://localhost:3001/api/faceit/stats/${playerId}`);
    statsData.value = await response.json(); // Mettez à jour ici
    console.log('blablablablalba',statsData.value);
    
    return statsData.value;

  } catch (error) {
    console.error("Failed to fetch player stats:", error);
    return null;
  }
}


getPlayerStatsByNickname('Kamikaz25').then(stats => {
  console.log('stats', stats);
  // Utilisez les stats comme vous le souhaitez
});

// Appeler la fonction lorsque le composant est monté
onMounted(() => {
  getStats();
  getPlayerData();
});

const fetchPlayerStatsByNickname = async () => {
  const stats = await getPlayerStatsByNickname('Kamikaz25');
  console.log('stats', stats);
  // Vous pouvez traiter les stats comme vous le souhaitez
};
</script>

<style scoped lang="scss">
.test {
  margin: 300px 50px;
}

.display {
  display: flex;
  gap: 50px;
  flex-direction: column;
}
</style>