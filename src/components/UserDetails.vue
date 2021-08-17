<template>
  <div class="q-pa-lg">
    <q-btn label="back" color="orange" to="/" size="sm"/>
    <q-card class="q-mt-md">
      <q-card-section>
        <div class="text-h6">{{user.name}}</div>
      </q-card-section>
      <q-card-section>
        <div><b>Organization :</b> {{userOrganization.name}}</div>
      </q-card-section>
      
      <q-card-section>
        <div><b>Ticktes</b></div>
        <q-card v-for="ticket in userTickets" :key="ticket._id" class="q-pa-md q-my-sm">
          <div class="row">
            <div class="col-lg-2 col-md-2 col-sm-6 col-xs-12"><b>Subject:</b></div>
            <div class="col-lg-10 col-md-10 col-sm-6 col-xs-12">{{ticket.subject}}</div>
          </div>
          <div class="row">
            <div class="col-lg-2 col-md-2 col-sm-6 col-xs-12"><b>Description:</b></div>
            <div class="col-lg-10 col-md-10 col-sm-6 col-xs-12">{{ticket.description}}</div>
          </div>
          <div class="row">
            <div class="col-lg-2 col-md-2 col-sm-6 col-xs-12"><b>type:</b></div>
            <div class="col-lg-10 col-md-10 col-sm-6 col-xs-12">{{ticket.type}}</div>
          </div>
          <div class="row">
            <div class="col-lg-2 col-md-2 col-sm-6 col-xs-12"><b>priority:</b></div>
            <div class="col-lg-10 col-md-10 col-sm-6 col-xs-12">{{ticket.priority}}</div>
          </div>
          <div class="row">
            <div class="col-lg-2 col-md-2 col-sm-6 col-xs-12"><b>status:</b></div>
            <div class="col-lg-10 col-md-10 col-sm-6 col-xs-12">{{ticket.status}}</div>
          </div>
          <div class="row">
            <div class="col-lg-2 col-md-2 col-sm-6 col-xs-12"><b>Created Date:</b></div>
            <div class="col-lg-10 col-md-10 col-sm-6 col-xs-12">{{ticket.created_at}}</div>
          </div>
          <div class="row">
            <div class="col-lg-2 col-md-2 col-sm-6 col-xs-12"><b>Due Date:</b></div>
            <div class="col-lg-10 col-md-10 col-sm-6 col-xs-12">{{ticket.due_at}}</div>
          </div>
        </q-card>
        
      </q-card-section>
      
    </q-card>
    
  </div>
</template>

<script>
import usersJson from '../JsonStore/users.json'
import ticketsJson from '../JsonStore/tickets.json'
import organizationsJson from '../JsonStore/organizations.json'
export default {
  data(){
    return{
      userId:localStorage.getItem('userId')
    }
  },
  computed:{
    user(){
      return usersJson.find(obj=>{
        return obj._id == this.userId
      })
    },
    userTickets(){
      return ticketsJson.filter(obj=>{
        return obj.assignee_id == this.userId
      })
    },
    userOrganization(){
      return organizationsJson.find(obj=>{
        return obj._id == this.user.organization_id
      }) 
    }
  }

}
</script>

<style>

</style>