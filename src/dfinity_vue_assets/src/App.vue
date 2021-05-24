<template>
  <v-app>
    <nav>
      <v-toolbar app max-height=55>
	<v-toolbar-title><span class="font-weight-light">Code</span><span>Name</span></v-toolbar-title>
	<v-spacer/>
	<Ident/>
	<v-btn flat color="grey">
          <span>Sign Out</span>
	  <v-icon right>exit_to_app</v-icon>
	</v-btn>
      </v-toolbar>
    </nav>
    <v-content>{{ internetComputerGreeting || 'Loading message from Internet Computer...' }}</v-content>
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
