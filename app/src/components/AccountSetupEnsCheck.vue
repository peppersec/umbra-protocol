<template>
  <div>
    <!-- Instructions -->
    <p>
      Make sure you are logged in with an account that has an associated ENS domain.
    </p>
    <!-- ENS Check -->
    <div class="q-mt-xl">
      <div v-if="userEnsDomain === undefined">
        <q-spinner
          color="primary"
          size="3rem"
        />
        <div>
          Loading...
        </div>
      </div>
      <div v-else-if="userEnsDomain">
        <q-icon
          left
          color="positive"
          name="fas fa-check"
        />
        You're all set!
        <br>
        <span class="text-caption">The ENS domain
          <span class="text-bold">{{ userEnsDomain }}</span>
          resolves to this address. Please continue to the next step.
        </span>
      </div>
      <div v-else>
        <q-icon
          left
          color="negative"
          name="fas fa-exclamation-triangle"
        />
        An ENS domain was not found for this address. If you do have an address, make
        sure the reverse record is set.
        <br>
        <span class="text-caption">
          Either login with a different address and refresh the page,
          or follow
          <a
            class="hyperlink"
            href="https://medium.com/@eric.conner/the-ultimate-guide-to-ens-names-aa541586067a"
            target="_blank"
          >this guide</a>
          to learn how to purchase a domain and configure it to resolve to
          your Ethereum address. Be sure to use the Public Resolver and set the reverse record
        </span>
      </div>
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex';

export default {
  name: 'AccountSetupEnsCheck',

  computed: {
    ...mapState({
      userAddress: (state) => state.user.userAddress,
      userEnsDomain: (state) => state.user.userEnsDomain,
      provider: (state) => state.user.ethersProvider,
    }),
  },
};
</script>
