<template>
    <div>
        <div class="dashboard">
        <v-subheader class="py-0 d-flex justify-space-between rounded-lg">
            <h2>Admin Dashboard</h2>
            <v-spacer></v-spacer>
                    <v-text-field
                    v-model="search"
                    append-icon="mdi-magnify"
                    label="Search"
                    single-line
                    hide-details
                    ></v-text-field>
                <v-spacer></v-spacer>
        </v-subheader>
        <br>
        <v-row dense>
            <v-col md="2">
            <div style="position: sticky; top: 92px">
              <!-- <v-text-field
                prepend-inner-icon="mdi-magnify"
                outlined
                v-model="search"
                clearable
                placeholder="Search"
                class="ml-2"
              ></v-text-field> -->
              <v-list
                v-if="$vuetify.breakpoint.mdAndUp"
                color="transparent"
                subheader
                class="ml-5"
              >
                <v-btn class="text-h6 mb-2">Products Manager</v-btn><br/>
                <v-btn class="text-h6 mb-2">Orders Manager</v-btn>
                <v-btn class="text-h6">Users Manager</v-btn>
              </v-list>
            </div>
          </v-col>
            <!-- <v-col lg="7" cols="12">
                <v-alert dense text type="success">
                    Login Successfully! Welcome to <strong>V-mart Admin Page</strong>
                </v-alert>
                <v-row>
                    <v-col lg="6" cols="12" v-for="(item,index) in activityLog" :key="index">
                        <v-card elevation="2" class="rounded-lg">
                            <v-card-text class="d-flex justify-space-between align-center">
                                <div>
                                    <strong>{{ item.title }}</strong> <br>
                                    <span>Last 3 weeks</span>
                                </div>
                                <v-avatar size="60" :color="item.color" style="border: 3px solid #444">
                                    <span style="color: white">{{item.amount}} +</span>
                                </v-avatar>
                            </v-card-text>
                            <v-card-actions class="d-flex justify-space-between">


                            </v-card-actions>
                        </v-card>
                    </v-col>
                </v-row>
            </v-col>
            <v-col cols="12" lg="5">
                <v-card>
                    <v-card-title>Activities</v-card-title>
                    <v-card-text class="py-0">
                        <v-timeline align-top dense>
                            <v-timeline-item color="indigo" small>
                                <strong>5 Minuts ago</strong>
                                <div class="text-caption">
                                   You have new order please check this out
                                </div>
                            </v-timeline-item>
                            <v-timeline-item color="green" small>
                                <strong>35 Minuts ago</strong>
                                <div class="text-caption mb-2">
                                    A Product has delivered!
                                </div>
                            </v-timeline-item>

                            <v-timeline-item color="indigo" small>
                                <strong>44 Minuts ago</strong>
                                <div class="text-caption">
                                    You have new order please check this out
                                </div>
                            </v-timeline-item>
                        </v-timeline>
                    </v-card-text>
                </v-card>
            </v-col> -->
            <v-col md="10">
                <v-card>
                    <v-data-table
                            caption="Recent Products List"
                            :headers="headers"
                            :items="desserts"
                            :items-per-page="5"
                            :search="search"
                            class="elevation-1"
                    >
                        <!-- <template v-slot:item.action="{ item }">
                            <v-icon
                                small
                                class="mr-2"
                                @click="editItem(item)"
                            >
                            mdi-pencil
                            </v-icon>
                            <v-icon
                                small
                                @click="handleSubmit(item.id)"
                            >
                                mdi-delete
                            </v-icon>
                        </template> -->
                        <template v-slot:top>
      <v-toolbar
        flat
      >
        <v-toolbar-title>Admin CRUD</v-toolbar-title>
        <v-divider
          class="mx-4"
          inset
          vertical
        ></v-divider>
        <v-spacer></v-spacer>
        <v-dialog
          v-model="dialog"
          max-width="500px"
        >
          <template v-slot:activator="{ on, attrs }">
            <v-btn
              color="primary"
              dark
              class="mb-2"
              v-bind="attrs"
              v-on="on"
            >
              Add New Product
            </v-btn>
          </template>
          <v-card>
            <v-card-title>
              <span class="text-h5">{{ formTitle }}</span>
            </v-card-title>

            <v-card-text width="800px">
              <v-container>
                <v-row>
                  <v-col
                    cols="12"
                    sm="6"
                    md="6"
                  >
                    <v-text-field
                      v-model="editedItem.id"
                      label="Id"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="6"
                  >
                    <v-text-field
                      v-model="editedItem.name"
                      label="Name"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="6"
                  >
                    <v-text-field
                      v-model="editedItem.onSale"
                      label="Onsale"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="6"
                  >
                    <v-text-field
                      v-model="editedItem.tags"
                      label="Tags"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="6"
                  >
                    <v-text-field
                      v-model="editedItem.image"
                      label="Image"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="6"
                  >
                    <v-text-field
                      v-model="editedItem.description"
                      label="Description"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="6"
                  >
                    <v-text-field
                      v-model="editedItem.price"
                      label="Price"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="6"
                  >
                    <v-text-field
                      v-model="editedItem.salePrice"
                      label="SalePrice"
                    ></v-text-field>
                  </v-col>
                </v-row>
              </v-container>
            </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                color="blue darken-1"
                text
                @click="close"
              >
                Cancel
              </v-btn>
              <v-btn
                color="blue darken-1"
                text
                @click="save"
              >
                Save
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <v-dialog v-model="dialogDelete" max-width="500px">
          <v-card>
            <v-card-title class="text-h5">Are you sure you want to delete this item?</v-card-title>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="closeDelete">Cancel</v-btn>
              <v-btn color="blue darken-1" text @click="deleteItemConfirm">OK</v-btn>
              <v-spacer></v-spacer>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-toolbar>
    </template>
    <template v-slot:item.image="{ item }">
      <v-img :src="item.image" height="150" width="150">
          <template #placeholder>
            <v-row
              class="fill-height"
              justify="center"
              align="center"
            >
              <v-progress-circular
                width="2"
                size="100"
                color="primary"
                indeterminate
              ></v-progress-circular>
            </v-row>
          </template>
        </v-img>
    </template>
    <template v-slot:item.action="{ item }">
      <v-icon
        small
        class="mr-2"
        @click="editItem(item)"
      >
        mdi-pencil
      </v-icon>
      <v-icon
        small
        @click="handleDelete(item.id)"
      >
        mdi-delete
      </v-icon>
    </template>
    <template v-slot:no-data>
      <v-btn
        color="primary"
        @click="initialize"
      >
        Reset
      </v-btn>
    </template>
                    </v-data-table>
                </v-card>
            </v-col>
        </v-row>
    </div>
    </div>
</template>

<script>
    export default {
        name: "Dashboard",
        async created() {
            this.desserts = await this.$axios.$get('http://localhost:3001/products')
            let data = this.desserts.map((obj) => obj.id)
            console.log('data', data);
            console.log('desserts', this.desserts);
        },
        data() {
            return {
                dialog: false,
                dialogDelete: false,
                search: '',
                headers: [
                    {
                        text: 'Id',
                        align: 'start',
                        sortable: false,
                        value: 'id',
                    },
                    {text: 'Name',align: 'center', value: 'name'},
                    {text: 'Onsale',align: 'center', value: 'onSale'},
                    {text: 'Tags',align: 'center', value: 'tags'},
                    {text: 'Image',align: 'center', value: 'image'},
                    {text: 'Description',align: 'center', value: 'description'},
                    {text: 'Price',align: 'center', value: 'price'},
                    {text: 'SalePrice',align: 'center', value: 'salePrice'},
                    {text: 'Actions', align: 'center', value: 'action'},
                ],
                desserts: [],
                editedIndex: -1,
                editedItem: {
                  name: '',
                  onSale: '',
                  tags: '',
                  image: '',
                  description: '',
                  price: '',
                  salePrice: '',
                },
                defaultItem: {
                  name: '',
                  onSale: '',
                  tags: '',
                  image: '',
                  description: '',
                  price: '',
                  salePrice: '',
                },
            }
        },
        computed: {
          formTitle () {
            return this.editedIndex === -1 ? 'New Item' : 'Edit Item'
          },
        },

        watch: {
          dialog (val) {
            val || this.close()
          },
          dialogDelete (val) {
            val || this.closeDelete()
          },
        },
        methods: {
            onButtonClick(item) {
                console.log('click on ' + item.no)
            },

            handleDelete(id) {
                console.log('id', this.id);
                const conf = window.confirm("Do you want to delete ?")
                if(conf) {
                    this.$axios.delete('http://localhost:3001/products/'+id)
                    .then(res => {
                        alert("delete success!")
                    }).catch(err => console.log(err))
                }
            },

        editItem (item) {
        this.editedIndex = this.desserts.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialog = true
      },

      // deleteItem (item) {
      //   this.editedIndex = this.desserts.indexOf(item)
      //   this.editedItem = Object.assign({}, item)
      //   this.dialogDelete = true
      // },

      // deleteItemConfirm () {
      //   this.desserts.splice(this.editedIndex, 1)
      //   this.closeDelete()
      // },

      close () {
        this.dialog = false
        this.$nextTick(() => {
          this.editedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        })
      },

      closeDelete () {
        this.dialogDelete = false
        this.$nextTick(() => {
          this.editedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        })
      },

      save () {
        if (this.editedIndex > -1) {
          Object.assign(this.desserts[this.editedIndex], this.editedItem)
        } else {
          this.desserts.push(this.editedItem)
        }
        this.close()
      },
        }
    }
</script>

<style scoped>
    .overlap-icon {
        position: absolute;
        top: -33px;
        text-align: center;
        padding-top: 12px;
    }
</style>