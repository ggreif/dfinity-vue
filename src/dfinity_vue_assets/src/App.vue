<template>
  <v-app>
    <nav>
      <v-app-bar app max-height=55>
	<v-app-bar-title shrink-on-scroll>
	  <span class="font-weight-light">Code</span><span>Name</span>
	</v-app-bar-title>
	<v-menu offset-y>
          <template v-slot:activator="{ on }">
	    <v-btn text slot="activator" color="primary" dark v-on="on">
	      <span>Locations</span>
	    </v-btn>
	  </template>

	  <v-list>
	    <v-list-item :key="'xxx'" :to="{name: 'App', query: { canisterId: 'ryjl3-tyaaa-aaaaa-aaaba-cai' }}">
              <v-list-item-content>
	        <v-list-item-title>item</v-list-item-title>
              </v-list-item-content>
	    </v-list-item>
	  </v-list>
	</v-menu>
	<v-spacer/>
	<Ident/>
      </v-app-bar>
    </nav>
    <v-main>{{ internetComputerGreeting || 'Loading message from Internet Computer...' }}</v-main>
  </v-app>
</template>

<script>
import { Actor, HttpAgent } from '@dfinity/agent';
import { idlFactory as dfinity_vue_idl, canisterId as dfinity_vue_id } from 'dfx-generated/dfinity_vue';
import Ident from './components/Ident.vue';
import 'material-design-icons-iconfont/dist/material-design-icons.css'

export default {
  name: "CodeName",
  components: { Ident },
  data: () => {
    return {
      internetComputerGreeting: ''
    };
  },
  created() {
    const agent = new HttpAgent();
    const dfinity_vue = Actor.createActor(dfinity_vue_idl, { agent, canisterId: dfinity_vue_id });

    dfinity_vue.greet(window.prompt("Enter your name:")).then(greeting => {
      this.internetComputerGreeting = greeting
    })
  }
}
</script>
