<template>
  <div class="card">
    <img :src="player.avatar" alt="Avatar" class="avatar" />
    <div class="info">
      <h3>{{ player.personaname }}</h3>
      <a :href="player.profileurl" target="_blank" rel="noopener noreferrer">
        <button>Voir profil Steam</button>
      </a>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  player: {
    type: Object,
    required: true,
  },
});

console.log('props.player',props.player);
</script>


<style>
.card {
  width: 300px;
  border: 1px solid #ccc;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 15px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  margin: 10px;
}
.avatar {
  width: 100px;
  height: 100px;
  border-radius: 50%;
}
.info {
  text-align: center;
}
button {
  background-color: #1b2838;
  color: white;
  border: none;
  padding: 10px 20px;
  cursor: pointer;
  font-size: 16px;
  transition: background-color 0.3s;
}
button:hover {
  background-color: #406281;
}
</style>
