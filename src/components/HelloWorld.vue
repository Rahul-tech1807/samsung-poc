<template>
  <div>
    <b class="bv-example-row">
      <b-breadcrumb>
        <b-col cols="5">
          <b-button-toolbar>
            <b-button-group class="mr-1">
              <b-button title="Save file">
                <b-icon icon="unlock-fill" aria-hidden="true"></b-icon>
              </b-button>
              <b-button title="New document">
                <b-icon
                  icon="arrows-angle-contract"
                  aria-hidden="true"
                ></b-icon>
              </b-button>
              <b-button title="Load file">
                <b-icon icon="arrows-angle-expand" aria-hidden="true"></b-icon>
              </b-button>
            </b-button-group>
            <b-button-group class="mr-1">
              <b-button title="Align left">
                <b-icon icon="arrow-return-left" aria-hidden="true"></b-icon>
              </b-button>
              <b-button title="Align center">
                <b-icon icon="arrow-return-right" aria-hidden="true"></b-icon>
              </b-button>
            </b-button-group>
            <b-button-group>
              <b-button title="Bold">
                <b-icon icon="zoom-in" aria-hidden="true"></b-icon>
              </b-button>
              <b-button title="Italic">
                <b-icon icon="zoom-out" aria-hidden="true"></b-icon>
              </b-button>
            </b-button-group>
          </b-button-toolbar>
        </b-col>
        <b-col cols="5" class="bt-right">
          <b-button-group>
            <b-input-group>
              <b-input-group-prepend is-text
                ><b>Auto Save</b>
                <b-form-checkbox switch>
                  <span class="sr-only">Switch for following text input</span>
                </b-form-checkbox>
              </b-input-group-prepend>
            </b-input-group>
          </b-button-group>
        </b-col>

        <b-col cols="2" class="bt-right">
          <b-button-group>
            <b-button variant="info">Save</b-button>
            <b-dropdown variant="primary" right text="Commit">
              <b-dropdown-item>Item 1</b-dropdown-item>
              <b-dropdown-item>Item 2</b-dropdown-item>
              <b-dropdown-divider></b-dropdown-divider>
              <b-dropdown-item>Item 3</b-dropdown-item>
            </b-dropdown>
          </b-button-group>
        </b-col>
      </b-breadcrumb>
      <b-row>
        <b-col cols="2">
          <div>
            <b-button v-b-toggle.sidebar-1
              ><b-icon icon="align-start"></b-icon
            ></b-button>
            <b-sidebar id="sidebar-1" title="Entities" shadow>
              <div class="sidebarIcons">
                <b-icon
                  icon="arrows-angle-expand"
                  class="rounded-circle bg-secondary p-2"
                  variant="light"
                ></b-icon>
                <b-icon
                  icon="arrows-angle-contract"
                  class="rounded-circle bg-secondary p-2"
                  variant="light"
                ></b-icon>
                <b-icon
                  icon="plus-lg"
                  class="rounded-circle bg-info p-2"
                  variant="light"
                ></b-icon>
              </div>
              <div class="px-3 py-2">
                <div>
                  <b-input-group size="sm" class="mb-2">
                    <b-input-group-prepend is-text>
                      <b-icon icon="search"></b-icon>
                    </b-input-group-prepend>
                    <b-form-input
                      type="search"
                      placeholder="Search Entities"
                    ></b-form-input>
                  </b-input-group>
                </div>
                <div>
                  <b-dropdown
                    split
                    split-variant="outline-primary"
                    variant="primary"
                    text="No Name Yet"
                    class="m-1 sidebarDropdown"
                  >
                    <b-dropdown-item href="#">Action</b-dropdown-item>
                    <b-dropdown-item href="#">Another action</b-dropdown-item>
                    <b-dropdown-item href="#"
                      >Something else here...</b-dropdown-item
                    >
                  </b-dropdown>
                </div>
              </div>
            </b-sidebar>
          </div>
        </b-col>
        <b-col cols="10"></b-col>
      </b-row>
    </b>
    <div class="bgback" @contextmenu.prevent="mousedown">
      <b-col cols="4"
        ><b-toast
          variant="info"
          id="example-toast"
          title="Entity"
          static
          no-auto-hide
        >
          <b-list-group>
            <b-list-group-item @click="showEntityCard=true">Create New Entity</b-list-group-item>
            <b-list-group-item href="#">Create New Group</b-list-group-item>
          </b-list-group>
        </b-toast>
      </b-col>
      <b-col
        cols="4"
        style="display: flex; flex-direction: column; justify-content: center"
        ><h3>Right Click to Add Entity</h3></b-col
      >
      <b-col cols="4">
        <Card-Entity :showEntityCard="showEntityCard" @hideEntity="showEntityCard = false"/>
      </b-col>
    </div> 
  </div>
</template>

<script>
import CardEntity from './CardEntity.vue'
export default {
  
  name: "HelloWorld",
  data() {
    return {
      text: "",
      showEntityCard: false
    };
  },
  components:{
    CardEntity
  },
  methods: {
    mousedown() {
      //alert("Right Click Down");
      this.$bvToast.show("example-toast");
    },
  },
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.bt-right {
  display: flex;
  justify-content: flex-end;
}
.bgback {
  height: 80vh;
  width: 85vw;
  margin: 10px 11%;
  display: flex;
  background-color: lightgray;
}
.sidebarDropdown {
  padding-top: 20px;
  display: flex;
}
.sidebarIcons {
  font-size: 2rem;
  float: right;
}
</style>
