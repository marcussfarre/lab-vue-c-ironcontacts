<template>
  <h1>IronContacts</h1>
  
  <button @click.prevent="addRandomContact()">Add Random Contact</button>
  <button @click.prevent="sortByPopularity()">Sort by popularity</button>
  <button @click.prevent="sortByName()">Sort by name</button>
  <table>
    <thead>
      <tr>
        <th>Picture</th>
        <th>Name</th>
        <th>Popularity</th>
        <th>Won Oscar</th>
        <th>Won Emmy</th>
        <th>Actions</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="element in contacts">
        <td> <img :src="element.pictureUrl" alt=""></td>
        <td>{{ element.name }}</td>
        <td>{{ element.popularity.toFixed(2) }}</td>
        <td><img v-if="element.wonOscar" src="./assets/oscar.png" alt=""></td>
        <td><img v-if="element.wonEmmy" src="./assets/emmy.png" alt=""></td>
        <td><button @click.prevent="deleteItem(element.id)">Delete</button></td>
      </tr>
    </tbody>
  </table>
</template>

<script>
  import ContactsJson from './contacts.json';
  export default {
    data() {
      return {
        contacts: ContactsJson.slice(0, 5),
      }
    },
    methods: {
      addRandomContact() {
        let currentIds = this.contacts.map((c) => c.id);
        let excludedContacts = ContactsJson.filter(contact => !currentIds.includes(contact.id));
        this.contacts.push(excludedContacts[Math.floor(Math.random() * excludedContacts.length)]);
      },
      sortByPopularity() {
        this.contacts.sort((a, b) => b.popularity - a.popularity);
      },
      sortByName() {
        this.contacts.sort((a, b) => {
          if (a.name < b.name) return -1;
          if (a.name > b.name) return 1;
          return 0;
        });
      },
      deleteItem(idToRemove) {
        const indexToRemove = this.contacts.findIndex((element) => element.id === idToRemove);
        this.contacts.splice(indexToRemove, 1);
      }
    }
  }
</script>

<style>
  body {
    margin: 0 20%;
    text-align: center;
  }
  img {
    width: 30%;
    height: 30%;
  }
  table {
    margin-top: 2%;
    table-layout: fixed;
    width: 100%;
  }
  td {
    width: 33.33%;
    text-align: center;
    padding: 10px;
    border: 1px solid #ccc;
    background-color: #CDCDCD;
  }
  td:hover {
    transform: scale(1.5); 
  }
  th {
    background-color: #5D5D5D;
  }
</style>
