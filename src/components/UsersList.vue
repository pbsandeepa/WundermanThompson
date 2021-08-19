<template>
  <div class="q-pa-lg">
    <q-table
      :grid="$q.screen.xs"
      title="Users"
      :data="users"
      :columns="columns"
      row-key="name"
      :filter="filter"
      :pagination.sync="pagination"
      table-header-class="bg-grey-7 text-white column-heading"
      dense
      >
      <template v-slot:top-right>
        <q-input dense debounce="300" v-model="filter" placeholder="Search">
          <template v-slot:append>
            <q-icon name="search" />
          </template>
        </q-input>
      </template>
      <template v-slot:body="props">
        <q-tr :props="props">
          <q-td key="name" :props="props">
            {{ props.row.name }}
          </q-td>
          <q-td key="created_at" :props="props">
            {{ props.row.created_at }}
          </q-td>
          <q-td key="email" :props="props">
            {{ props.row.email }}
          </q-td>
          <q-td key="phone" :props="props">
            {{ props.row.phone }}
          </q-td>
          <q-td key="role" :props="props">
            {{ props.row.role }}
          </q-td>
          <q-td key="signature" :props="props">
            {{ props.row.signature }}
          </q-td>
          <q-td key="details" :props="props">
            <q-btn size="xs" color="orange" label="Details" class="button" @click="getDetails(props.row)" />
          </q-td>
        </q-tr>
      </template>
    </q-table>
  </div>
</template>

<script>
import usersJson from '../JsonStore/users.json'
import moment from "moment";
export default {
  data(){
    return{
      users:usersJson.map(obj=>{
        obj.created_at = obj.created_at.split(' -')[0]
        obj.created_at = moment(obj.created_at).format('YYYY-MM-DD HH:mm')
        return obj
      }).sort((a,b)=>{
        return a.name.localeCompare(b.name);
      }),
      filter:'',
      columns: [
        { name: "name", label: "Name", align: "left", field: "name", sortable: true},
        { name: "created_at", label: "Created at", align: "left", field: "created_at", sortable: true},
        { name: "email", label: "Email", align: "left", field: "email", sortable: true},
        { name: "phone", label: "Phone", align: "left", field: "phone", sortable: true},
        { name: "role", label: "Role", align: "left", field: "role", sortable: true},
        { name: "signature", label: "Signature", align: "left", field: "signature", sortable: false},
        { name: "details", label: "Details", align: "left", sortable: false}
      ],
      pagination: {
        sortBy: "desc",
        descending: false,
        page: 1,
        rowsPerPage: 10,
      }
    }
  },
  methods:{
    getDetails(user){
      console.log("USER",user)
      localStorage.setItem('userId',user._id)
      this.$router.push({ name: "UserDetails" });
    }
  }

}
</script>

<style>

</style>