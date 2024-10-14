<script>

import Banner from '@components/Banner/Banner.vue';
import { LabeledInput } from '@components/Form/LabeledInput';
import LabeledSelect from '@shell/components/form/LabeledSelect';
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
  },

  data() {
    if (this.mode !== _CREATE) {
      this.value.decodedData.username = this.value.annotations['ionoscloud.cattle.io/username'];
      this.value.decodedData.password = this.value.annotations['ionoscloud.cattle.io/password'];
      this.value.decodedData.token = this.value.annotations['ionoscloud.cattle.io/token'];
      this.value.decodedData.endpoint = this.value.annotations['ionoscloud.cattle.io/endpoint'] || 'https://api.ionos.com/cloudapi/v6';
    }

    return {
      busy:           false,
      driver:         {},
      allowBusy:      false,
      error:          '',
    };
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
      this.value.annotations['ionoscloud.cattle.io/username'] = this.value.decodedData.username;
      this.value.annotations['ionoscloud.cattle.io/password'] = this.value.decodedData.password;
      this.value.annotations['ionoscloud.cattle.io/token'] = this.value.decodedData.token;
      this.value.annotations['ionoscloud.cattle.io/endpoint'] = this.value.decodedData.endpoint;

      this.value.username = this.value.decodedData.username;
      this.value.password = this.value.decodedData.password;
      this.value.token = this.value.decodedData.token;
      this.value.endpoint = this.value.decodedData.endpoint;
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
