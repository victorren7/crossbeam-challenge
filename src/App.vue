<template>
  <div id="app">
    <h1>Phonebook</h1> 
    <form class='container' >
      <label>
        Name:
        <input v-model="items.name" />
      </label>
      <label>
        phone #:
      <input v-model="items.phone" @keypress="isNumber($event)"/>
      </label>
      <button class='add-button' @click.prevent='addItem'>Add Phone Number</button>
    </form>
    <div class='table'>
      <ul class='label'>
        <li class='child'>
          <p>Name</p>
        </li>
        <li class='child'>
          <p>Phone</p>
        </li>
      </ul>
      <ul class='information'>
        <li class='people' v-for="user in items" v-bind:key="user.name">
          <p class='name'>{{ user.name }}</p>
          <p class='phone'>{{ user.phone }}</p>
          <button class='remove-button' v-on:click="removeRow">x</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
// import Vue from 'vue'
  export default {
    name: 'App',
    components: {
    },
    data() {
      return {
        newContact: [],
        items: [
          { name: 'Foo', phone: '123-456-7890' },
          { name: 'Bar', phone: '098-765-4321' }
        ],
      }
    },
    methods: {

      addItem () {
        // this.items.push({name: '', phone: ''})
        if (this.items.name === '' || this.items.phone === '') {
          console.log('empty');
        }
        this.newContact.push({...this.items})
        this.items.push({...this.newContact, ...this.items})
        console.log('items', this.items.name)
      },

      isNumber: function(evt) {
        evt = (evt) ? evt : window.event;
        var charCode = (evt.which) ? evt.which : evt.keyCode;
        if ((charCode > 31 && (charCode < 48 || charCode > 57)) && charCode !== 46) {
          evt.preventDefault();
        } else {
          return true;
        }
      },

      removeRow(){
        this.items.splice(this.item, 1)
      }


    }
  }

 </script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }

  .container {
    display: flex;
    width: 31.5rem;
    height: 2rem;
    margin: auto;
    grid-gap: 22px;
    align-items: flex-end;
  }

  label {
    display: grid;
  }

  .add-button {
    border: 1px solid transparent;
    height: 1.5rem;
    border-radius: .2rem;
    background-color: cornflowerblue;
    color: #fff;
  }

  .table {
    margin: 10rem 15rem;
  }

  .label {
    display: grid;
    grid-auto-flow: column;
    list-style-type: none;
    border-bottom: 2px solid grey;
    margin-bottom: 0;
    padding-left: 0;
    font-size: 26px;
    color: cornflowerblue;
  }

  .information {
    width: 49rem;
    list-style-type: none;
    margin: auto;
    padding-left: 0;
  }

  .people {
    display: grid;
    grid-auto-flow: column;
    grid-template-columns: 24rem 23rem 9rem;
    justify-content: start;
    height: 4rem;
  }

  .name {
    width: 24rem;
    margin: 0 auto;
    border-right: 1px solid black;
    border-bottom: 1px solid black;
    padding-top: 1rem;
  }

  .phone {
    width: 24rem;
    border-bottom: 1px solid black;
    margin: 0 auto;
    padding: 1rem 0 0 1rem;
  }

  .remove-button {
    background-color: transparent;
    border: none;
    color: red;
    height: 25px;
    width: 25px;
    align-self: center;
    border: 1px solid black;
    border-radius: 12px;
  }

</style> 


