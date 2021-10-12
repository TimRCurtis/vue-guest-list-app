/* eslint-disable vue/require-v-for-key */
<template>
  <div id="app">
    <div class="container mx-auto">
      <div class="text-center my-10">
        <h1 class="text-4xl">Guest List</h1>
      </div>

      <div class="max-w-2xl px-8 py-4 mx-auto bg-white rounded-lg shadow-lg dark:bg-gray-800">
        <div class="flex items-center justify-between">
            <span class="text-sm font-light text-gray-800 dark:text-gray-400">{{ event.eventDate }}</span>
        </div>

        <div class="" :styles="appStyles">
            <h4 class="text-2xl font-bold text-gray-700 dark:text-white" v-text="event.eventTitle"></h4>
            <p class="mt-2 text-gray-600 dark:text-gray-300">{{ event.eventDescription }}</p>
            <p class="mt-2 text-gray-600 dark:text-gray-300" v-html="event.signUpText"></p>

            <div class="flex items-center justify-center pb-6 md:py-0 md:w-1/2 mt-2">
              <form @submit.prevent="formSubmitted">
                <div class="flex flex-col overflow-hidden border rounded-lg dark:border-gray-600 lg:flex-row">
                  <input class="px-6 py-3 text-gray-700 placeholder-gray-500 bg-white outline-none dark:bg-gray-800 dark:placeholder-gray-400 focus:placeholder-transparent dark:focus:placeholder-transparent" type="text" placeholder="Jane Doe" v-model="newNameText">
                  
                  <button class="px-4 py-3 text-sm font-medium tracking-wider text-gray-100 transition-colors duration-200 transform bg-gray-700 hover:bg-gray-600 focus:bg-gray-600 focus:outline-none" >Submit</button>
                </div>
              </form>
            </div>
        </div>
      </div>

      <div class="mt-10 max-w-2xl px-8 py-4 mx-auto bg-white rounded-lg shadow-lg dark:bg-gray-800">
        <div class="flex items-center justify-between">
            <span class="text-sm font-light text-gray-800 dark:text-gray-400">Attending ({{ guestName.length }} / {{ eventCapacity }})</span>
        </div>
        <br>
        <div class="relative pt-1">
          <div class="overflow-hidden h-2 mb-4 text-xs flex rounded bg-green-200">
            <div :style="{width: eventCapacityPercentage + '%'}" class="shadow-none flex flex-col text-center whitespace-nowrap text-white justify-center bg-green-500"></div>
          </div>
        </div>

        <div v-if="guestName.length > 0">
          <!-- eslint-disable-next-line -->
          <div class="mt-2 mr-2 inline-flex items-center justify-center text-base border-2 border-green-200 text-green-800 dark:text-white bg-green-400 rounded-md px-4 py-2" v-for="name in sortNames">{{ name.toLowerCase() }}</div>
        </div>

        <div class="mt-2" v-else>
          <h4 class="text-2xl font-bold text-gray-700 dark:text-white">No names added yet...</h4>
        </div>
      </div>

    </div>
    <img class="mx-auto" alt="Vue logo" src="./assets/logo.png">
  </div>
</template>

<script>

export default {
  name: 'App',
  data: function(){
    return {
      event: {
          eventDate: 'August 14th- 16th',
          eventTitle: 'Summer Festival!',
          signUpText: 'Add your name to the guest list for <em>exclusive</em> offers:',
          eventDescription: "It's back! This years summer festival will be in the beautiful countryside featuring our best line up ever!"
        },
        newNameText: '',
        guestName: [],
        appStyles: {
          marginTop: '0.5rem'
        },
        eventCapacity: 25,
        eventCapacityPercentage: 0
    }
  },
  methods: {
    formSubmitted: function() {
      if(this.newNameText.length > 0 && this.eventCapacityPercentage < 100) {
        this.guestName.push(this.newNameText)
        this.newNameText = ''
        this.eventCapacityPercentage = this.guestName.length / (this.eventCapacity / 100)
      }
    }
  },
  computed: {
    sortNames: function() {
      // eslint-disable-next-line vue/no-side-effects-in-computed-properties
      return this.guestName.sort()
    }
  }
}
</script>

<style lang="scss">
  @import "./assets/scss/app.scss"
</style>
