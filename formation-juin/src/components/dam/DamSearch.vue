<template>
    <div>
        Name 
        <input type="text" v-model="searchedName"/>

        Rights:
        <input type="checkbox" v-model="doShow" :value="true">
        <we-cursor-provider v-if="doShow" :path="righttypesPath">
              <template #default="{ dataEntities: righttypes }">
                  <div>
                    <span v-for="righttype in righttypes" :key="righttype.id">
                        <input type="checkbox" v-model="searchedRighttypes" :value="righttype.id"> {{ righttype.name }}
                    </span>
                  </div>
              </template>
        </we-cursor-provider>

        Channels: 
        <we-cursor-provider path="dam/data/assetchannel">
              <template #default="{ dataEntities: channels }">
                  <div>
                    <span v-for="channel in channels" :key="channel.id">
                        <input type="checkbox" v-model="searchedChannels" :value="channel.id"> {{ channel.name }}
                    </span>
                  </div>
              </template>
        </we-cursor-provider>
   </div>
</template>

<script>
export default {
  name: 'DamSearch',
  props: {
    cursor: { 
        type: Object, 
        required: true
    }
  },
  data () {
      return {
          searchedName: '',
          searchedRighttypes: [],
          searchedChannels: [],
          doShow: false
      }
  },
  computed: {
      righttypesPath() {
          return this.cursor.schema.getFieldRelatedSchema('righttype');
      }
  },
  watch: {
      searchedName(newVal) {
          this.cursor.queryHelper.putConstraint('nameconstraint', { name: { startsWith: newVal}} );
      },
      searchedRighttypes(newVal) {
        if(newVal.length === 0) {
        this.cursor.queryHelper.removeConstraint('rightconstraint');
        } else {
        this.cursor.queryHelper.putConstraint('rightconstraint', { righttype: { in: newVal }} );
        }
      },
      searchedChannels(newVal) {
        if (newVal.length === 0) {
        this.cursor.queryHelper.removeConstraint('channelconstraint');
        }
        this.cursor.queryHelper.putConstraint('channelconstraint', { authorizedchannel: { in: newVal }} );
      }
  }
}
</script>