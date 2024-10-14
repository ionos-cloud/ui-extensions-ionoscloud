<script>
import { defineComponent } from 'vue';

import Loading from '@shell/components/Loading';
import { Banner } from '@components/Banner';
import CreateEditView from '@shell/mixins/create-edit-view';
import LabeledSelect from '@shell/components/form/LabeledSelect';
import { LabeledInput } from '@components/Form/LabeledInput';
import { Checkbox } from '@components/Form/Checkbox';
import { StringList } from '@components/StringList';
import { stringify } from '@shell/utils/error';
import { _VIEW } from '@shell/config/query-params';

import { LabeledTooltip } from '@rancher/components';

function initLocation(initialValue) {
  let select_options = [
    {
      label: 'Las Vegas, USA',
      value: {'value': 'us/las', 'name': 'Las Vegas, USA'}
    },
    {
      label:'Newark, USA',
      value: {'value': 'us/ewr', 'name':'Newark, USA'}
    },
    {
      label: 'Frankfurt, Germany',
      value: {'value': 'de/fra', 'name': 'Frankfurt, Germany'}
    },
    {
      label: 'Berlin, Germany',
      value: {'value': 'de/txl', 'name': 'Berlin, Germany'}
    },
    {
      label: 'London, UK',
      value: {'value': 'gb/lhr', 'name': 'London, UK'}
    },
    {
      label: 'Logroño, Spain',
      value: {'value': 'es/vit', 'name': 'Logroño, Spain'}
    },
    {
      label: 'Paris, France',
      value: {'value': 'fr/par', 'name': 'Paris, France'}
    },
  ]
  let selected_option = select_options[0].value

  select_options.forEach(element => {
    if (element.value.value == initialValue) {
      selected_option = element.value
    }
  }); 
  
  return {
    options: select_options,
    selected: selected_option,
    busy:     false,
    enabled:  false,
  };
}

function initServerType(initialValue) {
  let select_options = [
    {
      label: 'Enterprise',
      value: {'value': 'ENTERPRISE', 'name': 'Enterprise'}
    },
    {
      label:'Cube',
      value: {'value': 'CUBE', 'name':'Cube'}
    },
  ]
  let selected_option = select_options[0].value

  select_options.forEach(element => {
    if (element.value.value == initialValue) {
      selected_option = element.value
    }
  }); 
  
  return {
    options: select_options,
    selected: selected_option,
    busy:     false,
    enabled:  false,
  };
}

function initserverAvailabilityZone(initialValue) {
  let select_options = [
    {
      label: 'AUTO',
      value: {'value': 'AUTO', 'name': 'AUTO'}
    },
    {
      label:'ZONE_1',
      value: {'value': 'ZONE_1', 'name':'ZONE_1'}
    },
    {
      label:'ZONE_2',
      value: {'value': 'ZONE_2', 'name':'ZONE_2'}
    },
  ]
  let selected_option = select_options[0].value

  select_options.forEach(element => {
    if (element.value.value == initialValue) {
      selected_option = element.value
    }
  }); 
  
  return {
    options: select_options,
    selected: selected_option,
    busy:     false,
    enabled:  false,
  };
}

function initTemplate(initialValue) {
  let select_options = [
    {
      label: 'XS',
      value: {'value': 'CUBES XS', 'name': 'XS'}
    },
    {
      label: 'S',
      value: {'value': 'CUBES S', 'name': 'S'}
    },
    {
      label: 'M',
      value: {'value': 'CUBES M', 'name': 'M'}
    },
    {
      label: 'L',
      value: {'value': 'CUBES L', 'name': 'L'}
    },
    {
      label: 'XL',
      value: {'value': 'CUBES XL', 'name': 'XL'}
    },
    {
      label: 'XXL',
      value: {'value': 'CUBES XXL', 'name': 'XXL'}
    },
    {
      label: '3XL',
      value: {'value': 'CUBES 3XL', 'name': '3XL'}
    },
    {
      label: '4XL',
      value: {'value': 'CUBES 4XL', 'name': '4XL'}
    },
  ]
  let selected_option = select_options[0].value

  select_options.forEach(element => {
    if (element.value.value == initialValue) {
      selected_option = element.value
    }
  }); 
  
  return {
    options: select_options,
    selected: selected_option,
    busy:     false,
    enabled:  false,
  };
}

function initvolumeAvailabilityZone(initialValue) {
  let select_options = [
    {
      label: 'AUTO',
      value: {'value': 'AUTO', 'name': 'AUTO'}
    },
    {
      label:'ZONE_1',
      value: {'value': 'ZONE_1', 'name':'ZONE_1'}
    },
    {
      label:'ZONE_2',
      value: {'value': 'ZONE_2', 'name':'ZONE_2'}
    },
    {
      label:'ZONE_3',
      value: {'value': 'ZONE_3', 'name':'ZONE_3'}
    },
  ]
  let selected_option = select_options[0].value

  select_options.forEach(element => {
    if (element.value.value == initialValue) {
      selected_option = element.value
    }
  }); 
  
  return {
    options: select_options,
    selected: selected_option,
    busy:     false,
    enabled:  false,
  };
}

function initCpuFamily(initialValue) {
  let select_options = [
    {
      label: 'Intel XEON (USA)',
      value: {'value': 'INTEL_XEON', 'name': 'Intel XEON (USA)'}
    },
    {
      label: 'Intel SKYLAKE (Europe)',
      value: {'value': 'INTEL_SKYLAKE', 'name': 'Intel SKYLAKE (Europe)'}
    },
    {
      label: 'AMD OPTERON (USA)',
      value: {'value': 'AMD_OPTERON', 'name': 'AMD OPTERON (USA)'}
    },
    {
      label: 'INTEL ICELAKE (Europe)',
      value: {'value': 'INTEL_ICELAKE', 'name': 'INTEL ICELAKE (Europe)'}
    },
    {
      label: 'AMD EPYC',
      value: {'value': 'AMD_EPYC', 'name': 'AMD EPYC'}
    },
  ]
  let selected_option = select_options[0].value

  select_options.forEach(element => {
    if (element.value.value == initialValue) {
      selected_option = element.value
    }
  }); 
  
  return {
    options: select_options,
    selected: selected_option,
    busy:     false,
    enabled:  false,
  };
}

function initDiskType(initialValue) {
  let select_options = [
    {
      label: 'HDD',
      value: {'value': 'HDD', 'name': 'HDD'}
    },
    {
      label: 'SSD',
      value: {'value': 'SSD', 'name': 'SSD'}
    },
  ]
  let selected_option = select_options[0].value

  select_options.forEach(element => {
    if (element.value.value == initialValue) {
      selected_option = element.value
    }
  }); 
  
  return {
    options: select_options,
    selected: selected_option,
    busy:     false,
    enabled:  false,
  };
}

function initNatRuleProtocol() {
  let select_options = [
    {
      label: 'ALL',
      value: {'value': 'ALL', 'name': 'ALL'}
    },
    {
      label: 'TCP',
      value: {'value': 'TCP', 'name': 'TCP'}
    },
    {
      label: 'UDP',
      value: {'value': 'UDP', 'name': 'UDP'}
    },
    {
      label: 'ICMP',
      value: {'value': 'ICMP', 'name': 'ICMP'}
    },
  ]
  
  return {
    options: select_options,
    selected: select_options[0].value,
    busy:     false,
    enabled:  false,
  };
}

function validateIp(ip) {
  if (/^(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$/.test(ip)) {
    return true;
  }
  return false;
}

function validateSubnet(subnet) {
  let splitSubnet = subnet.split('/')
  return (splitSubnet.length == 2 && validateIp(splitSubnet[0]) && !(Number.isNaN(parseInt(splitSubnet[1]))));
}


export default defineComponent({
  components: {
    Banner,
    Loading,
    Checkbox,
    StringList,
    LabeledInput,
    LabeledSelect,
    LabeledTooltip
},

  mixins: [CreateEditView],

  props: {
    uuid: {
      type:     String,
      required: true,
    },

    cluster: {
      type:    Object,
      default: () => ({})
    },

    credentialId: {
      type:     String,
      required: true,
    },

    disabled: {
      type:    Boolean,
      default: false
    },

    busy: {
      type:    Boolean,
      default: false
    },

    provider: {
      type:     String,
      required: true,
    }
  },

  async fetch() {
    this.errors = [];
    if ( !this.credentialId ) {
      return;
    }

    if (this.mode === _VIEW) {
      this.initForViewMode();

      return;
    }

    this.$emit('validationChanged', true);
  },

  data() {
    const defaultNatRules = [
      'rule01:SNAT:TCP::::22:22',
      'rule02:SNAT:UDP::::53:53',
      'rule03:SNAT:TCP::::80:80',
      'rule04:SNAT:TCP::::179:179',
      'rule05:SNAT:TCP::::443:443',
      'rule06:SNAT:TCP::::2376:2376',
      'rule07:SNAT:UDP::::4789:4789',
      'rule08:SNAT:TCP::::6443:6443',
      'rule09:SNAT:TCP::::6783:6783',
      'rule10:SNAT:TCP::::8443:8443',
      'rule11:SNAT:UDP::::8472:8472',
      'rule12:SNAT:TCP::::9099:9099',
      'rule13:SNAT:TCP::::9100:9100',
      'rule14:SNAT:TCP::::9443:9443',
      'rule15:SNAT:TCP::::9796:9796',
      'rule16:SNAT:TCP::::10254:10254',
      'rule17:SNAT:TCP::::10256:10256',
      'rule18:SNAT:TCP::::2379:2380',
      'rule19:SNAT:UDP::::6783:6784',
      'rule20:SNAT:TCP::::10250:10252',
      'rule21:SNAT:TCP::::30000:32767',
      'rule22:SNAT:UDP::::30000:32767',
      'rule23:SNAT:ALL:::::',
    ]
    return {
      authenticating:              false,
      ready:                       false,
      os:                          null,
      password:                    null,
      havePassword:                false,
      location:                    initLocation(this.modelValue?.location || 'us/las'),
      serverType:                  initServerType(this.modelValue?.serverType || 'ENTERPRISE'),
      template:                    initTemplate(this.modelValue?.template || 'CUBES XS'),
      serverAvailabilityZone:      initserverAvailabilityZone(this.modelValue?.serverAvailabilityZone || 'AUTO'),
      volumeAvailabilityZone:      initvolumeAvailabilityZone(this.modelValue?.volumeAvailabilityZone || 'AUTO'),
      cpuFamily:                   initCpuFamily(this.modelValue?.cpuFamily || 'INTEL_XEON'),
      diskType:                    initDiskType(this.modelValue?.diskType || 'HDD'),
      cores:                       this.modelValue?.cores || '2',
      ram:                         this.modelValue?.ram || '2048',
      diskSize:                    this.modelValue?.diskSize || '50',
      image:                       this.modelValue?.image || 'ubuntu:20.04',
      imagePassword:               this.modelValue?.imagePassword,
      cloudInit:                   this.modelValue?.cloudInit,
      sshUser:                     this.modelValue?.sshUser || 'root',
      sshInCloudInit:              this.modelValue?.sshInCloudInit || false,
      datacenterId:                this.modelValue?.datacenterId,
      datacenterName:              this.modelValue?.datacenterName || 'docker-machine-data-center',
      lanId:                       this.modelValue?.lanId,
      lanName:                     this.modelValue?.lanName || 'docker-machine-lan',
      privateLan:                  this.modelValue?.privateLan || false,
      nicDhcp:                     this.modelValue?.nicDhcp || false,
      nicIps:                      this.modelValue?.nicIps || [],
      additionalLans:              this.modelValue?.additionalLans || [],
      waitForIpChange:             this.modelValue?.waitForIpChange || false,
      waitForIpChangeTimeout:      this.modelValue?.waitForIpChangeTimeout || '600',
      natId:                       this.modelValue?.natId,
      natName:                     this.modelValue?.natName || 'docker-machine-nat',
      createNat:                   this.modelValue?.createNat || false,
      natLansToGateways:           this.getNatLansToGateways(this.modelValue?.natLansToGateways) || [],
      natFlowlogs:                 this.modelValue?.natFlowlogs || [],
      natPublicIps:                this.modelValue?.natPublicIps || [],
      natRules:                    this.mode == 'create' ? defaultNatRules : this.modelValue?.natRules || [],
      natRuleName:                 '',
      natRuleType:                 'SNAT',
      natRuleProtocol:             initNatRuleProtocol(),
      natRuleSourceSubnet:         '',
      natRulePublicIp:             '',
      natRuleTargetSubnet:         '',
      natRuleTargetPortRangeStart: '',
      natRuleTargetPortRangeEnd:   '',
      errors:                      null,
    };
  },

  watch: {
    'credentialId'() {
      this.$fetch();
    },
  },

  methods: {
    stringify,

    initForViewMode() {
      this.fakeSelectOptions(this.Location, this.modelValue?.location);
      this.fakeSelectOptions(this.ServerType, this.modelValue?.serverType);
      this.fakeSelectOptions(this.serverAvailabilityZone, this.modelValue?.serverAvailabilityZone);
      this.fakeSelectOptions(this.volumeAvailabilityZone, this.modelValue?.volumeAvailabilityZone);
      this.fakeSelectOptions(this.CpuFamily, this.modelValue?.cpuFamily);
      this.fakeSelectOptions(this.DiskType, this.modelValue?.diskType);
    },

    fakeSelectOptions(list, value) {
      list.busy = false;
      list.enabled = false;
      list.options = [];

      if (value) {
        list.options.push({
          label: value,
          value,
        });
      }

      list.selected = value;
    },

    onChangeNicIps(event) {
      for (let ip of event) {
        if (!validateIp(ip)) {
          alert('Invalid IP detected: ' + ip );
          return;
        }
      }

      this.nicIps = event;
    },

    onChangeAdditionalLans(event) {
      this.additionalLans = event;
    },

    onChangeNatPublicIps(event) {
      for (let ip of event) {
        if (!validateIp(ip)) {
          alert('Invalid IP detected: ' + ip );
          return;
        }
      }

      this.natPublicIps = event;
    },

    onChangeNatLansToGateways(event) {

      for (let el of event) {
        let spl = el.split(':')
        if (spl.length != 2) {
          alert('Invalid entry detected: ' + el + '. The accepted format is LanId:IP!');
          return;
        }
        let lanId = spl[0]
        if (Number.isNaN(parseInt(lanId))) {
          alert('Invalid LAN ID detected: ' + lanId );
          return;
        }

        let ip = spl[1]
        if (!validateIp(ip)) {
          alert('Invalid IP detected: ' + ip );
          return;
        }
      }

      this.natLansToGateways = event.sort();
    },
    onChangeNatFlowlogs(event) {

      for (let el of event) {
        let spl = el.split(':')
        if (spl.length != 4) {
          alert('Invalid entry detected: ' + el + '. The accepted format is name:action:direction:bucket!');
          return;
        }
        let action = spl[1]
        if (!['ACCEPTED', 'REJECTED', 'ALL'].includes(action)) {
          alert('Invalid action: ' + action + '. Must be one of [\'ACCEPTED\', \'REJECTED\', \'ALL\']');
          return;
        }

        let direction = spl[2]
        if (!['INGRESS', 'EGRESS', 'BIDIRECTIONAL'].includes(direction)) {
          alert('Invalid direction: ' + direction + '. Must be one of [\'INGRESS\', \'EGRESS\', \'BIDIRECTIONAL\']');
          return;
        }
      }

      this.natFlowlogs = event.sort();
    },

    checkNatRule(rule) {
      let splitRule = rule.split(':') 
      if (splitRule.length != 8) {
        alert('Invalid entry detected: ' + rule + '. The accepted format is ' +
        'name:type:protocol:public_ip:source_subnet:target_subnet:target_port_range_start:target_port_range_end!');
        return false;
      }
      if (!['SNAT'].includes(splitRule[1])) {
        alert('Invalid rule type: ' + splitRule[1] + '. Must be one of [\'SNAT\']');
        return false;
      }
      if (!['TCP', 'UDP', 'ICMP', 'ALL'].includes(splitRule[2])) {
        alert('Invalid rule protocol: ' + splitRule[2] + '. Must be one of [\'TCP\', \'UDP\', \'ICMP\', \'ALL\']');
        return false;
      }
      if (splitRule[3] && !validateIp(splitRule[3])) {
        alert('Invalid IP detected: ' + splitRule[3] );
        return false;
      }
      if (splitRule[4] && !validateSubnet(splitRule[4])) {
        alert('Invalid Subnet detected: ' + splitRule[4] );
        return false;
      }
      if (splitRule[5] && !validateSubnet(splitRule[5])) {
        alert('Invalid Subnet detected: ' + splitRule[5] );
        return false;
      }
      if (splitRule[6] && (!Number.isInteger(Number(splitRule[6])) || Number(splitRule[6]) < 0)) {
        alert('Invalid Port detected: ' + splitRule[6] );
        return false;
      }
      if (splitRule[7] && (!Number.isInteger(Number(splitRule[7])) || Number(splitRule[7]) < 0)) {
        alert('Invalid Port detected: ' + splitRule[7] );
        return false;
      }

      return true;
    },

    onChangeNatRules(event) {
      for (let rule of event) {
        if (!this.checkNatRule(rule)) {
          return false;
        }
      }
      this.natRules = event.sort();
    },

    addNatRule() {
      let rule = [
        this.natRuleName, this.natRuleType, this.natRuleProtocol.selected.value, this.natRulePublicIp, this.natRuleSourceSubnet,
        this.natRuleTargetSubnet, this.natRuleTargetPortRangeStart, this.natRuleTargetPortRangeEnd
      ].join(':')
      if (this.natRules.includes(rule)) {
        alert('Rule is already in list!');
        return;
      }
      if (this.checkNatRule(rule)) {
        this.natRules.push(rule)
      }
    },

    onPrivateKeyFileSelected(v) {
      this.filename = v.file.name;
      this.privateKeyFile = v.data;

      // On initial load, filename is shown as a password as we don't know what the filename was that was used - we just want to indicate there is a vlue
      // When a file is chosen, change the type to text, so that the user can see the filename of the file that they chose
      this.privateKeyFieldType = 'text';

      this.$emit('validationChanged', true);
    },

    // Sets `value.natLansToGateways` to a map of LANs to Gateways interpretable by Docker Machine Driver: like 1=10.0.0.1,10.0.0.2:2=10.0.0.10
    formatNatLansToGateways() {
      let aux = {}
      for (let el of this.natLansToGateways) {
        let spl = el.split(':')
        let lanId = spl[0], ip = spl[1]

        if (!aux.hasOwnProperty(lanId)) {
          aux[lanId] = [ip]
        } else {
          aux[lanId].push(ip)
        }
      }

      let formatedValues = []
      for (let lanId in aux) {
        formatedValues.push(`${lanId}=${aux[lanId].join(',')}`)
      }

      return formatedValues.join(':');
    },

    getNatLansToGateways(stringValue) {
      if (!stringValue) {
        return undefined
      }

      let arr = [], spl

      for (let el of stringValue.split(':')) {
        spl = el.split('=')
        for (let ip of spl[1].split(',')) {
          arr.push(`${spl[0]}:${ip}`)
        }
      }

      return arr
    },

    syncValue() {
      // Note: We don't need to provide password as this is picked up via the credential

      // Copy the values from the form to the correct places on the value
      this.modelValue.location = this.location.selected?.value;
      this.modelValue.serverType = this.serverType.selected?.value;
      this.modelValue.serverAvailabilityZone = this.serverAvailabilityZone.selected?.value;
      this.modelValue.template = this.template.selected?.value;
      this.modelValue.volumeAvailabilityZone = this.volumeAvailabilityZone.selected?.value;
      this.modelValue.cpuFamily = this.cpuFamily.selected?.value;
      this.modelValue.diskType = this.diskType.selected?.value;
      this.modelValue.cores = this.cores;
      this.modelValue.ram = this.ram;
      this.modelValue.diskSize = this.diskSize;
      this.modelValue.image = this.image;
      this.modelValue.imagePassword = this.imagePassword;
      this.modelValue.cloudInit = this.cloudInit;
      this.modelValue.sshUser = this.sshUser;
      this.modelValue.sshInCloudInit = this.sshInCloudInit;
      this.modelValue.datacenterId = this.datacenterId;
      this.modelValue.datacenterName = this.datacenterName;
      this.modelValue.lanId = this.lanId;
      this.modelValue.lanName = this.lanName;
      this.modelValue.privateLan = this.privateLan;
      this.modelValue.nicDhcp = this.nicDhcp;
      this.modelValue.nicIps = this.nicIps;
      this.modelValue.additionalLans = this.additionalLans;
      this.modelValue.waitForIpChange = this.waitForIpChange;
      this.modelValue.waitForIpChangeTimeout = this.waitForIpChangeTimeout;
      this.modelValue.natId = this.natId;
      this.modelValue.natName = this.natName;
      this.modelValue.createNat = this.createNat;
      this.modelValue.natLansToGateways = this.formatNatLansToGateways();
      this.modelValue.natFlowlogs = this.natFlowlogs;
      this.modelValue.natPublicIps = this.natPublicIps;
      this.modelValue.natRules = this.natRules;
      this.modelValue.skipDefaultNatRules = true;
    },

    test() {
      this.syncValue();
    }
  },
});
</script>

<template>
  <div>
    <Loading
      v-if="$fetchState.pending"
      :delayed="true"
    />
    <div v-if="errors.length">
      <div
        v-for="(err, idx) in errors" :key="idx">
        <Banner
          color="error"
          :label="stringify(err)"
        />
      </div>
    </div>
    <div>
      <div class="ionoscloud-config">
        <div class="title">
          ionoscloud Configuration
        </div>
      </div>
      <div class="row mt-10">
        <div class="col span-3">
          <LabeledSelect
            v-model:value="location.selected"
            label="Location"
            :options="location.options"
            :loading="location.busy"
            :searchable="false"
          />
        </div>
        <div class="col span-3">
          <LabeledSelect
            v-model:value="serverType.selected"
            label="ServerType"
            :options="serverType.options"
            :loading="serverType.busy"
            :searchable="false"
          />
        </div>
        <div class="col span-3" v-if="serverType.selected.value === 'ENTERPRISE'">
          <LabeledSelect
            v-model:value="serverAvailabilityZone.selected"
            label="serverAvailabilityZone"
            :options="serverAvailabilityZone.options"
            :loading="serverAvailabilityZone.busy"
            :searchable="false"
          />
        </div>
        <div class="col span-3" v-if="serverType.selected.value === 'ENTERPRISE'">
          <LabeledSelect
            v-model:value="volumeAvailabilityZone.selected"
            label="volumeAvailabilityZone"
            :options="volumeAvailabilityZone.options"
            :loading="volumeAvailabilityZone.busy"
            :searchable="false"
          />
        </div>
        <div class="col span-3" v-if="serverType.selected.value === 'CUBE'">
          <LabeledSelect
            v-model:value="template.selected"
            label="CUBE Server Template"
            :options="template.options"
            :loading="template.busy"
            :searchable="false"
          />
        </div>
      </div>

      <div class="row mt-10" v-if="serverType.selected.value === 'ENTERPRISE'">
        <div class="col span-3">
          <LabeledSelect
            v-model:value="cpuFamily.selected"
            label="CpuFamily"
            :options="cpuFamily.options"
            :loading="cpuFamily.busy"
            :searchable="false"
          />
        </div>
        <div class="col span-3">
          <LabeledInput
            v-model:value="cores"
            :mode="mode"
            :disabled="busy"
            :required="true"
            label="CPU Core Count"
          />
        </div>
        <div class="col span-6">
          <LabeledInput
            v-model:value="ram"
            :mode="mode"
            :disabled="busy"
            :required="true"
            label="RAM size (in MiB)"
          />
          <p class="help-block">Must be a multiple of 256</p>
        </div>
      </div>

      <div class="row mt-10" v-if="serverType.selected.value === 'ENTERPRISE'">
        <div class="col span-6">
          <LabeledInput
            v-model:value="diskSize"
            :mode="mode"
            :disabled="busy"
            :required="true"
            label="Disk size (in GB)"
          />
        </div>
        <div class="col span-6">
          <LabeledSelect
            v-model:value="diskType.selected"
            label="DiskType"
            :options="diskType.options"
            :loading="diskType.busy"
            :searchable="false"
            :required="true"
          />
        </div>
      </div>

      <div class="row mt-10">
        <div class="col span-6">
          <LabeledInput
            v-model:value="image"
            :mode="mode"
            :disabled="busy"
            :required="true"
            label="Image Alias or ID"
          />
          <p class="help-block">You can use <a href="https://docs.ionos.com/cli-ionosctl" target="_blank" rel="noopener noreferrer">ionosctl image list [-F name=operatingSystem]</a></p>
        </div>
        <div class="col span-6">
          <LabeledInput
            v-model:value="imagePassword"
            :mode="mode"
            :disabled="busy"
            :required="true"
            label="Image Password"
            type="password"
          />
        </div>
      </div>

      <div class="row mt-10">
        <div class="col span-12">
          <label class="acc-label">Cloud init configuration.</label>
          <textarea
            v-model:value="cloudInit"
            :disabled="busy || mode === _VIEW"
          ></textarea>
          <p class="help-block">Optional. <a href="https://cloudinit.readthedocs.io/en/latest/topics/examples.html" target="_blank" rel="noopener noreferrer">Cloud-init Documentation</a>.</p>
        </div>
      </div>

      <div class="row mt-10">
        <div class="col span-4">
          <LabeledInput
            v-model:value="sshUser"
            :mode="mode"
            :disabled="busy"
            label="SSH User"
          />
          <p class="help-block">Optional. User to connect to via SSH.</p>
        </div>
        <div class="col span-4">
          <Checkbox
            label="Send SSH in user data."
            v-model:value="sshInCloudInit"
            :mode="mode"
            :disabled="busy"
          />
          <p class="help-block">Should the driver only add the SSH info in the user data? (required for custom images).</p>
        </div>
      </div>

      <div class="row mt-10">
        <div class="col span-4">
          <LabeledInput
            v-model:value="datacenterId"
            :mode="mode"
            :disabled="busy"
            label="Datacenter ID"
          />
          <p class="help-block">Optional, UUID-4 format. If you want to use an existing IONOS Datacenter to host this VM, you can provide its ID here.</p>
        </div>
        <div class="col span-4">
          <LabeledInput
            v-model:value="datacenterName"
            :mode="mode"
            :disabled="busy"
            label="Datacenter Name"
          />
          <p class="help-block">String. If you want to use an existing IONOS Datacenter to host this VM, you can change the name here. Please note that if the ID is set it will the prioritized.</p>
        </div>
      </div>

      <div class="row mt-10">
        <div class="col span-4">
          <LabeledInput
            v-model:value="lanId"
            :mode="mode"
            :disabled="busy"
            label="LAN ID"
          />
          <p class="help-block">Optional, integer. The LAN the VM will attach to. If blank, a default LAN will be created. Overrides "Private LAN" setting.</p>
        </div>
        <div class="col span-4">
          <LabeledInput
            v-model:value="lanName"
            :mode="mode"
            :disabled="busy"
            label="LAN Name"
          />
          <p class="help-block">String. If you want to use an existing IONOS LAN, you can change the name here. Please note that if the ID is set it will the prioritized.</p>
        </div>
        <div class="col span-4">
          <Checkbox
            label="Make Default LAN Private"
            v-model:value="privateLan"
            :mode="mode"
            :disabled="busy"
          />
          <p class="help-block">If the default LAN does not exist, create a private LAN</p>
        </div>
      </div>
      <div class="row mt-10">
        <div class="col span-4">
          <StringList
            label="Additional LANs"
            v-model:value="additionalLans"
            :items="additionalLans"
            :mode="mode"
            :disabled="busy"
            @change="onChangeAdditionalLans($event)"
          />
          <p class="help-block">Optional. Exiting Ionos LAN names. Every LAN in the datacenter which has its name in this list will be connected to the server, names which are not found will be ignored.</p>
        </div>
      </div>
      <div class="row mt-10">
        <div class="col span-4">
          <Checkbox
            label="NIC DHCP"
            v-model:value="nicDhcp"
            :mode="mode"
            :disabled="busy"
          />
          <p class="help-block">Set whether the created NIC should have dhcp set on or off</p>
        </div>
        <div class="col span-4">
          <StringList
            label="NIC Ips"
            v-model:value="nicIps"
            :items="nicIps"
            :mode="mode"
            :disabled="busy"
            @change="onChangeNicIps($event)"
          />
          <p class="help-block">Optional. IPBlock reserved IPs. If not set, the driver will reserve an IPBlock automatically or let the API set a private IP if the LAN is private</p>
        </div>
      </div>

      <div class="row mt-10">
        <div class="col span-4">
          <Checkbox
            label="Wait for NIC IP change"
            v-model:value="waitForIpChange"
            :mode="mode"
            :disabled="busy"
          />
          <p class="help-block">Should the driver wait for the NIC IP to be set by external sources?</p>
        </div>
        <div class="col span-4">
          <LabeledInput
            v-model:value="waitForIpChangeTimeout"
            :mode="mode"
            :disabled="busy"
            label="Wait for IP change timeout"
          />
        </div>
      </div>

      <div class="row mt-10">
        <div class="col span-4">
          <LabeledInput
            v-model:value="natId"
            :mode="mode"
            :disabled="busy"
            label="IONOS Nat Gateway ID"
          />
          <p class="help-block">Optional, UUID-4 format. Use a preconfigured NAT Gateway. Datacenter ID and Private LAN required. Overrides NAT Config below</p>
        </div>
        <div class="col span-4">
          <LabeledInput
            v-model:value="natName"
            :mode="mode"
            :disabled="busy"
            label="IONOS Nat Gateway Name"
          />
          <p class="help-block">String. If the "Create NAT" checkbox is checked, will try creating a NAT with this name. If one already exists, will use the existing NAT.</p>
        </div>
        <div class="col span-4">
          <Checkbox
            label="Create a configurable NAT"
            v-model:value="createNat"
            :mode="mode"
            :disabled="busy"
          />
          <p class="help-block">Requires private LAN. You can override settings of this NAT using the form below <a href="#" target="_blank" rel="noopener noreferrer">See open ports here</a>. Must set gateway IP as default route via cloud config, default: 10.0.0.1</p>
        </div>
      </div>

      <div class="row mt-10" v-if="createNat === true">
        <div class="col span-4">
          <StringList
            label="Custom NAT: map LANs to Gateway IPs"
            v-model:value="natLansToGateways"
            :items="natLansToGateways"
            :mode="mode"
            :disabled="busy"
            @change="onChangeNatLansToGateways($event)"
          />
          <p class="help-block">Optional. Maps Lan IDs to a specific Gateway IP. Gateway IP must be set manually as default route.</p>
        </div>
        <div class="col span-4">
          <StringList
            label="Custom NAT: Public IPs"
            v-model:value="natPublicIps"
            :items="natPublicIps"
            :mode="mode"
            :disabled="busy"
            @change="onChangeNatPublicIps($event)"
          />
          <p class="help-block">Optional. IPBlock reserved IPs. If not set, the driver will reserve an IPBlock automatically</p>
        </div>
        <div class="col span-4">
          <StringList
            label="Custom NAT: Flowlogs"
            v-model:value="natFlowlogs"
            :items="natFlowlogs"
            :mode="mode"
            :disabled="busy"
            @change="onChangeNatFlowlogs($event)"
          />
          <p class="help-block">Optional. NAT Flowlogs.</p>
        </div>
      </div>

      <div class="row mt-10" v-if="createNat === true">
        <div class="col span-6">
          <StringList
            label="Custom NAT: Rules"
            v-model:value="natRules"
            :items="natRules"
            :mode="mode"
            :disabled="busy"
            @change="onChangeNatRules($event)"
          />
          <p class="help-block">Optional. NAT Rules. Use the form bellow to add a new NAT rule</p>
        </div>
      </div>
      <div class="card-container create-nat" v-if="createNat">
        <div class="row mt-10">
          <div class="col span-3">
            <LabeledInput
              v-model:value="natRuleName"
              :mode="mode"
              :disabled="busy"
              label="IONOS Nat Gateway Rule Name"
            />
            <p class="help-block">String. The name of the new Nat Gateway Rule.</p>
          </div>
          <div class="col span-3">
              <LabeledInput
                v-model:value="natRuleType"
                :mode="mode"
                :disabled="busy"
                label="IONOS Nat Gateway Rule Type"
              />
            <p class="help-block">String. The type of the new Nat Gateway Rule.</p>
          </div>
          <div class="col span-3">
            <LabeledSelect
              v-model:value="natRuleProtocol.selected"
              label="natRuleProtocol"
              :options="natRuleProtocol.options"
              :loading="natRuleProtocol.busy"
              :searchable="false"
            />
          </div>
          <div class="col span-3">
            <LabeledInput
              v-model:value="natRulePublicIp"
              :mode="mode"
              :disabled="busy"
              label="IONOS Nat Gateway Rule Public IP"
            />
            <p class="help-block">String. The Public IP of the new Nat Gateway Rule, leave black and the driver will use the nat gateway IP.</p>
          </div>
        </div>
        <div class="row mt-10">
          <div class="col span-3">
            <LabeledInput
              v-model:value="natRuleSourceSubnet"
              :mode="mode"
              :disabled="busy"
              label="IONOS Nat Gateway Rule Source Subnet"
            />
            <p class="help-block">String. The Source Subnet of the new Nat Gateway Rule, leave black and the driver will use the first ip on the nic with mask 24.</p>
          </div>
          <div class="col span-3">
            <LabeledInput
              v-model:value="natRuleTargetSubnet"
              :mode="mode"
              :disabled="busy"
              label="IONOS Nat Gateway Rule Target Subnet"
            />
            <p class="help-block">String. The Target Subnet of the new Nat Gateway Rule.</p>
          </div>
          <div class="col span-3">
            <LabeledInput
              v-model:value="natRuleTargetPortRangeStart"
              :mode="mode"
              :disabled="busy"
              label="IONOS Nat Gateway Rule Port Range Start"
            />
            <p class="help-block">Integer. The Port Range Start of the new Nat Gateway Rule.</p>
          </div>
          <div class="col span-3">
            <LabeledInput
              v-model:value="natRuleTargetPortRangeEnd"
              :mode="mode"
              :disabled="busy"
              label="IONOS Nat Gateway Rule Port Range End"
            />
            <p class="help-block">Integer. The Port Range End of the new Nat Gateway Rule.</p>
          </div>
        </div>
        <div class="mt-10">
          <button @click="addNatRule()">
            Add NAT Gateway Rule +
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped lang="scss">
  .help-block {
    margin-top: .5em;
    font-size: .8em;
    margin-left: 1em;
  }

  .create-nat {
    flex-direction: column;
  }

  .ionoscloud-config {
    display: flex;
    align-items: center;

    > .title {
      font-weight: bold;
      padding: 4px 0;
    }

    > .loading {
      margin-left: 20px;
      display: flex;
      align-items: center;

      > i {
        margin-right: 4px;;
      }
    }
  }
</style>
