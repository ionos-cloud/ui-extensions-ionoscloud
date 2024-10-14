<script>
import { defineComponent } from 'vue';

import Banner from '@components/Banner/Banner.vue';
import { LabeledInput } from '@components/Form/LabeledInput';
import LabeledSelect from '@shell/components/form/LabeledSelect';
import { _CREATE } from '@shell/config/query-params';

export default defineComponent({
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

    modelValue: {
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
      this.modelValue.decodedData.username = this.modelValue.annotations['ionoscloud.cattle.io/username'];
      this.modelValue.decodedData.password = this.modelValue.annotations['ionoscloud.cattle.io/password'];
      this.modelValue.decodedData.token = this.modelValue.annotations['ionoscloud.cattle.io/token'];
      this.modelValue.decodedData.endpoint = this.modelValue.annotations['ionoscloud.cattle.io/endpoint'] || 'https://api.ionos.com/cloudapi/v6';
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
      return !!this.modelValue?.decodedData?.token ||
        !!this.modelValue?.decodedData?.username &&
        !!this.modelValue?.decodedData?.password;
    }
  },

  created() {
    this.$emit('validationChanged', false);
  },

  methods: {
    test() {
      this.modelValue.annotations['ionoscloud.cattle.io/username'] = this.modelValue.decodedData.username;
      this.modelValue.annotations['ionoscloud.cattle.io/password'] = this.modelValue.decodedData.password;
      this.modelValue.annotations['ionoscloud.cattle.io/token'] = this.modelValue.decodedData.token;
      this.modelValue.annotations['ionoscloud.cattle.io/endpoint'] = this.modelValue.decodedData.endpoint;

      this.modelValue.username = this.modelValue.decodedData.username;
      this.modelValue.password = this.modelValue.decodedData.password;
      this.modelValue.token = this.modelValue.decodedData.token;
      this.modelValue.endpoint = this.modelValue.decodedData.endpoint;
      return true;
    },

    clear() {
      // Tell parent that the form is not invalid
      this.$emit('validationChanged', false);
    },
  },
});
</script>

<template>
  <div>
    <div class="row">
      <div class="col span-6">
        <LabeledInput
          :modelValue="modelValue.decodedData.username"
          class="mt-20"
          label-key="driver.ionoscloud.auth.fields.username"
          placeholder-key="driver.ionoscloud.auth.placeholders.username"
          type="text"
          :mode="mode"
          @update:value="modelValue.setData('username', $event);"
        />
      </div>
      <div class="col span-6">
        <LabeledInput
          :modelValue="modelValue.decodedData.password"
          class="mt-20"
          label-key="driver.ionoscloud.auth.fields.password"
          placeholder-key="driver.ionoscloud.auth.placeholders.password"
          type="password"
          :mode="mode"
          @update:value="modelValue.setData('password', $event);"
        />
      </div>
    </div>
    <div class="row">
      <div class="col span-12">
        <LabeledInput
          :modelValue="modelValue.decodedData.token"
          class="mt-20"
          label-key="driver.ionoscloud.auth.fields.token"
          placeholder-key="driver.ionoscloud.auth.placeholders.token"
          type="text"
          :mode="mode"
          @update:value="modelValue.setData('token', $event);"
        />
      </div>
    </div>
    <div class="row">
      <div class="col span-12">
        <LabeledInput
          :modelValue="modelValue.decodedData.endpoint || 'https://api.ionos.com/cloudapi/v6'"
          class="mt-20"
          label-key="driver.ionoscloud.auth.fields.endpoint"
          placeholder-key="driver.ionoscloud.auth.placeholders.endpoint"
          type="text"
          :mode="mode"
          @update:value="modelValue.setData('endpoint', $event);"
        />
      </div>
    </div>
  </div>
</template>
