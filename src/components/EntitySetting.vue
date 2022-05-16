<template>
<div class="card-ele">
 <b-card
    class="card-width"
  >

  <div class="title-head">
  <p class="setting-title">Setting</p>
  </div>
  <!--name field -->
    <b-form-group
      id="fieldset-horizontal"
      label-cols-sm="4"
      label-cols-lg="4"
      content-cols-sm
      label="Name"
      label-size="sm"
      label-for="input-horizontal"
      style="text-align:start"
    >
      <b-form-input id="input-horizontal" v-model="name"  :state="nameState" placeholder="Entity_1" size="sm"></b-form-input>
    </b-form-group>
  
<!-- comment field-->
<div>
<b-form-group
      id="fieldset-horizontal"
      label-cols-sm="4"
      label-cols-lg="4"
      content-cols-sm
      label="Comment"
      label-size="sm"
      label-for="input-horizontal"
      style="text-align:start"
    >
  <b-form-textarea
    id="textarea-rows"
    placeholder="Entity Comment"
    rows="6"
    size="sm"
    v-model="comment"
  ></b-form-textarea>
  </b-form-group>
</div>

<!--group field-->

<div>
<b-form-group
      id="fieldset-horizontal"
      label-cols-sm="4"
      label-cols-lg="4"
      content-cols-sm
      label="Group"
      label-size="sm"
      label-for="input-horizontal"
      style="text-align:start"
    >
    <b-form-select v-model="group" :options="options" size="sm"></b-form-select>
    </b-form-group>
  </div>

  <!--inheritance field-->

<div>
<b-form-group
      id="fieldset-horizontal"
      label-cols-sm="4"
      label-cols-lg="4"
      content-cols-sm
      label="Inheritance"
      label-size="sm"
      label-for="input-horizontal"
      style="text-align:start"
    >
    <b-form-select v-model="inheritance" :options="items" size="sm"></b-form-select>
    </b-form-group>
  </div>

    <div style="text-align:start;">
    <b-button variant="outline-primary" @click="submit">Submit</b-button>
    </div>
  </b-card>
</div>
</template>

<script>
//import axios from 'axios';
  export default {
    data() {
      return {
        name:null,
        comment:null,
        group: null,
        inheritance:null,
        options: [
          { value: null, text: 'Select' },
          { value: 'a', text: 'First option' },
          { value: 'b', text: 'Second Option' },
          { value: 'c', text: 'Third option' },
        ],
        items: [
          { value: null, text: 'Select' },
          { value: 'a', text: 'First option' },
          { value: 'b', text: 'Second Option' },
          { value: 'c', text: 'Third option' },
        ]
      }
    },
    computed: {
      nameState() {
        return this.name == null ? false : true
      }
    },
    methods:{
        submit(){
           
            const entity_setting = { name: this.name,
                                     comment: this.comment,
                                     group: this.group,
                                     inheritance:this.inheritance
                                    };
            console.log(entity_setting);
            // axios.post("https://modelling-tool/post/entity-setting", entity_setting)
            //     .then(response => {
            //         const entity_data = response.data
            //         console.log(entity_data);
            //     })
            //     .catch(error => {
            //     this.errorMessage = error.message;
            //     console.error("There was an error!", error);
            //     });
        }
    }
  }
</script>


<style>
p.setting-title {
    font-weight: 600;
}
.title-head {
    text-align: start;
}
.close-icon{
    text-align:end;
    font-size:12px;
}
</style>