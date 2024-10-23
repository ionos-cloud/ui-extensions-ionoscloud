<script>

import Banner from '@components/Banner/Banner.vue';
import { LabeledInput } from '@components/Form/LabeledInput';
import LabeledSelect from '@shell/components/form/LabeledSelect';
import SECRET from '@shell/config/types';
import { _CREATE } from '@shell/config/query-params';

export default {
  components: {
    Banner,
    LabeledInput,
    LabeledSelect,
  },

  props: {
    mode: {
      type:     String,
      required: true,
    },

    value: {
      type:     Object,
      required: true,
    },
  },

  async fetch() {
    this.driver = await this.$store.dispatch('rancher/find', {
      type: 'nodedriver',
      id:   'ionoscloud'
    });
    const secret = await this.$store.dispatch('management/find', { type: SECRET, id: this.value.id.replace(':', '/') });
    this.value.setData('username', atob(secret.data['ionoscloudcredentialConfig-username']));
    this.value.setData('endpoint', atob(secret.data['ionoscloudcredentialConfig-endpoint']));
  },

  data() {
    return {
      busy:           false,
      driver:         {},
      allowBusy:      false,
      error:          '',
    };
  },

  watch: {
    'value.decodedData.username'(neu) {
      this.$emit('validationChanged', !!neu);
    },

    'value.decodedData.password'(neu) {
      this.$emit('validationChanged', !!neu);
    },

    'value.decodedData.token'(neu) {
      this.$emit('validationChanged', !!neu);
    },

    'value.decodedData.endpoint'(neu) {
      this.$emit('validationChanged', !!neu);
    },
  },

  computed: {

    canAuthenticate() {
      return !!this.value?.decodedData?.token ||
        !!this.value?.decodedData?.username &&
        !!this.value?.decodedData?.password;
    }
  },

  created() {
    this.$emit('validationChanged', false);
  },

  methods: {
    test() {
      return true;
    },

    clear() {
      // Tell parent that the form is not invalid
      this.$emit('validationChanged', false);
    },
  },
};
</script>

<template>
  <div>
    <div class="row">
      <div class="col span-6">
        <LabeledInput
          :value="value.decodedData.username"
          class="mt-20"
          label-key="driver.ionoscloud.auth.fields.username"
          placeholder-key="driver.ionoscloud.auth.placeholders.username"
          type="text"
          :mode="mode"
          @input="value.setData('username', $event);"
        />
      </div>
      <div class="col span-6">
        <LabeledInput
          :value="value.decodedData.password"
          class="mt-20"
          label-key="driver.ionoscloud.auth.fields.password"
          placeholder-key="driver.ionoscloud.auth.placeholders.password"
          type="password"
          :mode="mode"
          @input="value.setData('password', $event);"
        />
      </div>
    </div>
    <div class="row">
      <div class="col span-12">
        <LabeledInput
          :value="value.decodedData.token"
          class="mt-20"
          label-key="driver.ionoscloud.auth.fields.token"
          placeholder-key="driver.ionoscloud.auth.placeholders.token"
          type="text"
          :mode="mode"
          @input="value.setData('token', $event);"
        />
      </div>
    </div>
    <div class="row">
      <div class="col span-12">
        <LabeledInput
          :value="value.decodedData.endpoint || 'https://api.ionos.com/cloudapi/v6'"
          class="mt-20"
          label-key="driver.ionoscloud.auth.fields.endpoint"
          placeholder-key="driver.ionoscloud.auth.placeholders.endpoint"
          type="text"
          :mode="mode"
          @input="value.setData('endpoint', $event);"
        />
      </div>
    </div>
  </div>
</template>
