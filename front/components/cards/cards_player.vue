<template>
  <div class="player">
    <h2 class="player__name">{{ playerData.pseudo }}</h2>
    <img :src="playerData.playerImage" alt="Joueur" class="player__image" v-if="playerData.playerImage" />
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
</template>

<script setup lang="ts">
import { ref, computed, defineProps } from 'vue';

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

const formattedStats = computed(() => [
  { label: "Total de kills", value: props.playerStats.total_kills },
  { label: "Total de morts", value: props.playerStats.total_deaths },
  { label: "Temps total joué", value: totalTimeFormatted.value },
  { label: "Bombes plantées", value: props.playerStats.total_planted_bombs },
  { label: "Bombes désamorcées", value: props.playerStats.total_defused_bombs },
  { label: "Total de victoires", value: props.playerStats.total_wins },
  { label: "Dégâts totaux causés", value: props.playerStats.total_damage_done },
  { label: "Total de kills headshot", value: props.playerStats.total_kills_headshot },
  { label: "% de HS", value: `${headshotPercentage.value}%` },
  { label: "Ratio K/D", value: killDeathRatio.value }
]);
</script>

<style lang="scss">
.player {
  width: 400px;
  background-color: $background-color;
  border: 1px solid $medium-gray;
  padding: $spacing-m;
  border-radius: $spacing-s;
  box-shadow: 0 $spacing-s $spacing-m rgba($black, 0.1);
  text-align: center;
  font-family: $font-main;

  &__name {
    margin-top: $spacing-m;
    font-size: $font-size-xxl;
    font-family: $font-button;
    text-transform: uppercase;
    font-weight: $font-weight-medium;
    color: $secondary-color;
  }

  &__image {
    width: 100%;
    height: auto;
    border-radius: 50%;
    margin-top: $spacing-m;
    border: 2px solid $main-color;
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


