<template>
  <div>
    <h1>Daftar Tugas<p>&#9997;&#10071;</p></h1><hr><br>
    <form @submit.prevent="addActivity">
      <input type="text" v-model="newActivity" placeholder="Tambahkan Tugas...">
      <button>Tambah</button><p>&#128516;&#9996;</p>
    </form><br>
    <table>
    <ul>
      <li v-for="(activity, index) in filteredActivities" :key="index" :class="{ done: activity.completed }">
        <input type="checkbox" v-model="activity.completed">
        <span>{{ activity.text }}</span>
        <button @click="removeActivity(index)">Hapus</button>
      </li>
    </ul>
    </table>
    <div>
      <label>Tampilkan Tugas yang Belum Selesai:</label>
      <input type="checkbox" v-model="showUnfinished">
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newActivity: '',
      activities: [
        { text: 'Makalah DAA', completed: false }, 
        { text: 'UTS PBK', completed: true }, 
        { text: 'Makalah Jarkom', completed: false } 
      ],
      showUnfinished: false
    }
  },
  methods: {
    addActivity() {
      if (this.newActivity.trim() !== '') {
        this.activities.push({ text: this.newActivity, completed: false });
        this.newActivity = '';
      }
    },
    removeActivity(index) {
      this.activities.splice(index, 1);
    }
  },
  computed: {
    filteredActivities() {
      if (this.showUnfinished) {
        return this.activities.filter(activity => !activity.completed);
      } else {
        return this.activities;
      }
    }
  }
}
</script>

<style>
.done {
  text-decoration: line-through;
  text-decoration-color: yellow;
  font-style: italic;
}
h1 {
  color: blue;
  font-style: oblique;
  text-align: center;
}
.addActivity {
  text-decoration-color: red;
}
</style>
