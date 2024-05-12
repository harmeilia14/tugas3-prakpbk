<template>
  <div id="app">
    <h1>
      <b><i>Apa yang aku lakukan hari ini?</i></b>
    </h1>
    <br />
    <div class="input-container">
      <input type="text" v-model="newActivity" placeholder="Tambahkan kegiatan..." />
      <button @click="addActivity">Tambah</button>
    </div>
    <table>
      <thead>
        <tr>
          <th>Hari</th>
          <th>Waktu</th>
          <th>Kegiatan</th>
          <th>Aksi</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(activity, index) in activities" :key="index">
          <td>{{ activity.day }}</td>
          <td>{{ activity.time }}</td>
          <td>{{ activity.activity }}</td>
          <td>
            <button @click="editActivity(index)">Edit</button>
            <button @click="deleteActivity(index)">Hapus</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newActivity: '',
      activities: []
    }
  },
  methods: {
    addActivity() {
      if (this.newActivity.trim() !== '') {
        const currentTime = new Date().toLocaleTimeString()
        const currentDay = new Date().toLocaleDateString()
        this.activities.push({
          time: currentTime,
          day: currentDay,
          activity: this.newActivity.trim()
        })
        this.newActivity = ''
      }
    },
    editActivity(index) {
      const updatedActivity = prompt('Edit kegiatan:', this.activities[index].activity)
      if (updatedActivity !== null) {
        this.activities[index].activity = updatedActivity.trim()
      }
    },
    deleteActivity(index) {
      if (confirm('Anda yakin ingin menghapus kegiatan ini?')) {
        this.activities.splice(index, 1)
      }
    }
  }
}
</script>

<style scoped>
#app {
  background-image: url('./src/assets/1.jpg');
  background-repeat: no-repeat;
  background-size: cover;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.input-container {
  display: flex;
  margin-bottom: 20px;
}

.input-container input[type='text'] {
  flex: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px 0 0 5px;
}

.input-container button {
  background-color: #2d89cf;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 0 5px 5px 0;
  cursor: pointer;
}

table {
  width: 100%;
  border-collapse: collapse;
}

th,
td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

th {
  background-color: #f2f2f2;
}

button {
  background-color: #46a2e8;
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 5px;
  cursor: pointer;
}
</style>
