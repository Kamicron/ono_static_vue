<template>
  <div class="player">
    <div class="player__inner">
      <CardsHeaderCards :playerData="playerData"/>
      <div class="player__stats">
        <div class="player__stats-row" v-for="index in Math.ceil(formattedStats.length / 2)" :key="index">
          <div v-for="n in 2" :key="n" class="player__stat">
            <strong>{{ formattedStats[(index - 1) * 2 + n - 1].label }}:</strong> {{ formattedStats[(index - 1) * 2 + n -
              1].value
            }}
          </div>
        </div>
      </div>
      <a :href="playerData.profileUrl" target="_blank" rel="noopener noreferrer" class="player__profile-link">
        <border-text text="Voir profil steam" :fontSize="24" :borderWidth="3" color="white" hoverColor="white" />
      </a>
    </div>
  </div>
</template>

<script setup lang="ts">
const props = defineProps({
  playerData: {
    type: Object,
    required: true,
    default: () => ({
      pseudo: '',
      playerImage: ''
    })
  },
  playerStats: {
    type: Object,
    required: true
  }
});

console.log('props.playerStats:', props.playerStats)

const headshotPercentage = computed(() =>
  ((props.playerStats.total_kills_headshot / props.playerStats.total_kills) * 100).toFixed(2)
);
const killDeathRatio = computed(() =>
  (props.playerStats.total_kills / props.playerStats.total_deaths).toFixed(2)
);

const totalTimeFormatted = computed(() => {
  let hours = Math.floor(props.playerStats.total_time_played / 3600);
  let minutes = Math.floor((props.playerStats.total_time_played % 3600) / 60);
  let seconds = props.playerStats.total_time_played % 60;
  return `${hours}h ${minutes}m ${seconds}s`;
});

const formatNumber = (number) => {
  return number.toLocaleString('fr-FR');
}


const formattedStats = computed(() => [
  { label: "Total de kills", value: formatNumber(props.playerStats.total_kills) },
  { label: "Total de morts", value: formatNumber(props.playerStats.total_deaths) },
  { label: "Temps total joué", value: totalTimeFormatted.value },
  { label: "Bombes plantées", value: formatNumber(props.playerStats.total_planted_bombs) },
  { label: "Bombes désamorcées", value: formatNumber(props.playerStats.total_defused_bombs) },
  { label: "Total de victoires", value: formatNumber(props.playerStats.total_wins) },
  { label: "Dégâts totaux causés", value: formatNumber(props.playerStats.total_damage_done) },
  { label: "Total de kills headshot", value: formatNumber(props.playerStats.total_kills_headshot) },
  { label: "% de HS", value: `${headshotPercentage.value}%` },
  { label: "Ratio K/D", value: killDeathRatio.value }
]);

</script>

<style lang="scss" scoped>
.player {
  width: 550px;
  background-color: $background-color;
  padding: $spacing-m;
  box-shadow: 0 $spacing-s $spacing-m rgba($black, 0.1);
  text-align: center;
  font-family: $font-main;
  position: relative;

  // Bordure en haut
  &::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0; // Pour commencer du coin gauche
    right: 0;
    height: 5px;
    background: linear-gradient(135deg, transparent calc(15% - 5px), white calc(15% - 5px), white 100%);
  }

  // Bordure à gauche
  &::after {
    content: "";
    position: absolute;
    top: 1%;
    left: 0;
    bottom: 0;
    width: 5px;
    background: linear-gradient(135deg, transparent calc(15% - 2.5px), white calc(15% - 2.5px), white 100%);
  }

  &__inner {

    // Bordure à droite
    &::before {
      content: "";
      position: absolute;
      top: 0;
      right: 0;
      bottom: 10%;
      width: 5px;
      background: linear-gradient(135deg, white 0%, white calc(94% - 5px), transparent calc(94% - 5px));
    }

    // Bordure en bas
    &::after {
      content: "";
      position: absolute;
      bottom: 0;
      left: 0;
      right: 10%;
      height: 5px;
      background: linear-gradient(135deg, white 0%, white calc(94% - 5px), transparent calc(94% - 5px));
    }
  }

  &__information {
    display: flex;
    justify-content: space-around;
    align-items: center;
  }



  &__stats {
    margin-top: $spacing-m;

    &-row {
      display: flex;
      justify-content: space-between;
    }
  }

  &__stat {
    flex: 1;
    padding: 0 $spacing-s;
    color: $main-color;
    display: flex;
    justify-content: space-between;

    strong {
      color: $white;
    }
  }

  &__stat-label {
    font-weight: $font-weight-medium;
    letter-spacing: $letter-spacing-wide;
  }

  &__profile-link {
    display: inline-block;
    margin-top: $spacing-m;
    padding: $spacing-s $spacing-m;
    text-decoration: none;
    font-weight: $font-weight-bold;
    font-family: $font-button;
    color: $white;
    background-color: $main-color;
    border-radius: $spacing-s;
    transition: background-color 0.3s;

    &:hover {
      background-color: $secondary-color;
    }
  }
}
</style>
