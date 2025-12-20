<template>
    <section id="jdpost">
        <div class="col-md-12 col-sm-12">
            <form id="appointment-form" role="form" method="post" action="#">
                <div class="col-md-6 col-sm-6">
                    <b-message type="is-info" has-icon style="font-size: 12px;  max-width: 600px;">
                        <h5>Welcome to Securo JOBZ!!..</h5>
                        <h4>Profile Email-ID :
  <span class="highlight">{{ profileEmail }}</span>
  <!-- &nbsp; --  Name :
  <span class="highlight">{{ profileNm }}</span> -->
</h4>
                        <!-- <h4 >Profile ID : {{ profileId }} Name : {{profileNm}}</h4> -->
                        <h5>Select the Opportunity Code to view the interview detail</h5>
                    </b-message>
                     <h4 >List Of Interviews</h4>
                    <div class="heading" style="background-color: SeaShell;" >
                        <div class="div-table-row" style="background-color: #ccc;">
                            <div class="div-table-col3"><b>Opportunity.Code</b></div>
                            <div class="div-table-col6"><b>Designation</b></div>
                            <div class="div-table-col1"><b>Last date</b></div>
                           
  
                        </div>
<div
  class="div-table-row"
  v-for="d in allpostData"
  :key="d.interviewId"
  v-if="allpostData && allpostData.length">
                        <div class="div-table-row" v-for="d in allpostData" :key="d.id">
                            <div class="div-table-col3">
                                <a @click="viewJd(d)"><span style="color: blueviolet">{{ d.oppurtunityCode }}</span></a>
                            </div>
                            <div class="div-table-col6">{{ d.oppurtunityDesignation}}</div>
                            <div class="div-table-col1">{{ toUI(d.oppurtunityLastDate)}}</div>
  </div>
                        </div>
                        <!-- ❌ NO DATA -->
<div
  class="div-table-row no-data"
  v-else
>
  <div class="no-data-text">
    🚫 No interviews available
  </div>
</div>

                    </div>
                    
                </div>

                <div class="col-md-6 col-sm-6" v-if="visible">
                    <h4 >Opportunity.Code :  {{ opCode }}</h4>
                    <div class="row">
                    <div class="div-table">
                        <div class="col-md-12 col-sm-12">
                            <div class="col-md-4 col-sm-4">
                                <b-label class="flright item">Designation</b-label>
                            </div>
                            <div class="col-md-1 col-sm-1">
                                <b-label class="flright item">:</b-label>
                            </div>
                            <div class="col-md-7 col-sm-7">
                                {{ designation }}
                            </div>
                        </div>
                        <div class="col-md-12 col-sm-12">
                            <div class="col-md-4 col-sm-4">
                                <b-label class="flright item">Location</b-label>
                            </div>
                            <div class="col-md-1 col-sm-1">
                                <b-label class="flright item">:</b-label>
                            </div>
                            <div class="col-md-7 col-sm-7">
                                {{ location }}
                            </div>
                        </div>
                        
                        <div class="col-md-12 col-sm-12">
                            <div class="col-md-4 col-sm-4">
                                <b-label class="flright item">Interview Date</b-label>
                            </div>
                            <div class="col-md-1 col-sm-1">
                                <b-label class="flright item">:</b-label>
                            </div>
                            <div class="col-md-7 col-sm-7">
                                {{ intvDt }}
                            </div>
                            <!-- <div class="col-md-7 col-sm-7"> -->
                                <!-- //  {{ intvDt }} -->
                                <!-- <b-field>
                                    <b-datepicker ref="datepicker" expanded placeholder="Select a date">
                                    </b-datepicker>
                                    <b-button @click="$refs.datepicker.toggle()" icon-left="calendar-today"
                                        type="is-primary" />
                                </b-field> -->

                            <!-- </div> -->
                        </div>
                        
                        <div class="col-md-12 col-sm-12">
                            <div class="col-md-4 col-sm-4">
                                <b-label class="flright item">Interview Time</b-label>
                            </div>
                            <div class="col-md-1 col-sm-1">
                                <b-label class="flright item">:</b-label>
                            </div>
                            <div class="col-md-7 col-sm-7">
                                {{ intvTime }}
                            </div>
                            <!-- <div class="col-md-7 col-sm-7"> -->
                                <!-- {{ jdmsg }} -->
                                <!-- <b-input placeholder="Enter Interview Details..." maxlength="2000"
                                    v-model="name"></b-input> -->

                            <!-- </div> -->
                        </div>
                        <!-- <div class="col-md-12 col-sm-12">
                            <div class="col-md-4 col-sm-4">
                                <b-label class="flright item">Confirmed on</b-label>
                            </div>
                            <div class="col-md-1 col-sm-1">
                                <b-label class="flright item">:</b-label>
                            </div>
                            <div class="col-md-7 col-sm-7">
                                {{ confDt }}
                            </div>
                        </div> -->
                                
                        <div class="col-md-12 col-sm-12">
                            <div class="col-md-4 col-sm-4">
                                <b-label class="flright item">Interview Details</b-label>
                            </div>
                            <div class="col-md-1 col-sm-1">
                                <b-label class="flright item">:</b-label>
                            </div>
                            <div class="col-md-7 col-sm-7">
                                {{ intvDetails }}
                            </div>
                            <!-- <div class="col-md-7 col-sm-7"> -->
                                <!-- {{ jdmsg }} -->
                                <!-- <b-input placeholder="Enter Interview Details..." maxlength="2000"
                                    v-model="name"></b-input> -->

                            <!-- </div> -->
                        </div>
                        <div class="col-md-12 col-sm-12">
                            <div class="col-md-4 col-sm-4">
                                <b-label class="flright item padding8">Confirm</b-label>
                            </div>
                            <div class="col-md-1 col-sm-1">
                                <b-label class="flright item">:</b-label>
                            </div>
                            <div class="col-md-2 col-sm-2">
                                <b-field>
                                    <b-checkbox v-model="cbConfirm" true-value="Yes" false-value="No">
                                        {{ cbConfirm }}
                                    </b-checkbox>
                                </b-field>
                            </div>
                            <div class="col-md-5 col-sm-5">
                                <b-button  class="flright" type="is-success" @click="doSubmit">
                                    Submit
                                </b-button>
                            </div>
                             <div class="row">
                                <a style=" font-size:15px"><b>Important: </b>Confirmation on or before the final date by clicking the "Check box"</a>
                            </div>
                            </div>
                        </div>
                    </div>
                </div>
            </form>
        </div>
    </section>
</template>

<script>
import axios from 'axios'
export default {
    data() {
        return {
            visible: false,
            disabledFlag: true,
            canApprove: false,
            profileId:"",
            interviewId:"",
            employerId:"",
            oppurtunityLastDate:"",
            intvDetails:"",
            intvDt:"",
            intvTime:"",
            interviewVenue:"",
            profileNm:"",
      profilesData: {},
     profileeee_data:null,
            cbConfirm: "No",
            allpostData:[],
             profileEmail: JSON.parse(sessionStorage.getItem("loggedUser") || "{}").userEmail || "",
      profileId: JSON.parse(sessionStorage.getItem("loggedUser") || "{}").profileId || "",
      profileNm:JSON.parse(sessionStorage.getItem("loggedUser") || "{}").profileNm || "",
        }
    },
    mounted() {
    this.setLoggedUserData();
  },

  methods: {
    toUI(dateStr) {
  if (!dateStr) return "";
  const d = new Date(dateStr);
  return (
    ("0" + d.getDate()).slice(-2) + "/" +
    ("0" + (d.getMonth() + 1)).slice(-2) + "/" +
    d.getFullYear()
  );
},
    async fetchProfileBasedOnUserIdd(id) {
      console.log("fetchProfileBasedOnUserId", id);
      const url = this.$hostName + "/api/v1/jobseekers/user/" + id;

      try {
        const res = await axios.get(url);
        this.profileeee_data = res.data;
        this.profileId = res.data.profileId;
        this.profileNm=res.data.profileNm
        this.fetchInterviews(this.profileId);
      } catch (err) {
        console.error("Error fetching profile:", err);
      }
    },

    setLoggedUserData() {
      const storedLoggedUser = sessionStorage.getItem("loggedUser");

      if (storedLoggedUser) {
        let loggedUserObject = JSON.parse(storedLoggedUser);
        this.profileEmail = loggedUserObject.userEmail || "";
        this.userId = loggedUserObject.userId;

        // Load Jobseeker Profile
        this.fetchProfileBasedOnUserIdd(this.userId);

       // this.fetchOpp();
      } else {
        setTimeout(() => this.setLoggedUserData(), 300);
      }
    },

    async fetchEmployerById(id) {
      if (!id) return;
      console.log("fetchEmpBasedOnUserId", id);
      const url = `${this.$hostName}/api/v1/employers/${id}`;
      try {
        const res = await axios.get(url);
        console.log("-----------------",employees);
        
        this.empNm = res.data.empNm;
        this.employerId = res.data.employerId;
      } catch (err) {
        console.error("Error fetching employer:", err);
        this.empNm = "";
      }
    },

async fetchInterviews(profileId) {
      //const url = this.$hostName + "/api/v1/interview/interviews-not-in-select-tab?" + profileId;
    //   const url = this.$hostName + `/api/v1/interview/interviews-not-in-select-tab?`+profileId={profileId};
const url = `${this.$hostName}/api/v1/interview/interviews-not-in-select-tab?profileId=${profileId}`;

      try {
        const res = await axios.get(url);
console.log("resssssssss,",res)
        this.allpostData = res.data;
       // this.interviewId=res.data.interviewId
        console.log("res",res.data);
      } catch (err) {
        console.error("Error fetching intervies:", err);
      }
    },
         populateFormFields(d) {
      if (!d) return;
      this.employerId=d.employerId;
      this.interviewId = d.interviewId;
      this.opCode = d.oppurtunityCode || "";
      this.designation=d.oppurtunityDesignation,
      this.oppurtunityLastDate=d.oppurtunityLastDate,
      this.intvDt=d.interviewDate,
      this.intvDetails=d.interviewInstruction,
      this.intvTime=d.interviewTime,
      this.location=d.interviewVenue
      
    },

    viewJd(d) {
      this.visible = true;
      this.oppurtunityId = d.oppurtunityId;
      
  
//this.interviewId = d.interviewId;
      this.populateFormFields(d);

     
    },
        async doSubmit() {
      this.modData = {
            interviewId: this.interviewId,
         employerId: this.employerId,
        profileId: this.profileId,
        status: this.cbConfirm
      };

      try {
        const url = `${this.$hostName}/api/v1/interview-selection`;
        await axios.post(url, this.modData);

        if (this.cbConfirm === "Yes") {
          this.$buefy.toast.open({
            message: "✅ You applied successfully!",
            type: "is-success",
            duration: 2500
          });
        } else {
          this.$buefy.toast.open({
            message: "❌ You declined this opportunity.",
            type: "is-danger",
            duration: 2500
          });
        }

        this.visible = false;

      } catch (err) {
        console.error("Error saving record:", err);
        this.$buefy.toast.open({
          message: "❌ Error saving. Please try again.",
          type: "is-danger",
          duration: 3000
        });
      }
    }
    }
}
</script>

<style scoped>
.padding8 {
    padding-top: 8px;
}

.flright {
    float: left;
}

.item {
    font-weight: 700;
    display: flex;
}
.heading{
  display: flex;
  flex-direction: column;
  width: 100%;
  max-width: 700px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: seashell;
  font-family: Arial, sans-serif;
}

.div-table-row {
  display: flex;
  width: 100%;
  border-bottom: 1px solid #ddd;
  padding: 6px 10px;
  box-sizing: border-box;
  align-items: center;
}

.div-table-row:last-child {
  border-bottom: none;
}

.div-table-row.header {
  background-color: #ccc;
  font-weight: bold;
}

.div-table-col3 {
  width: 30%;  /* Opportunity Code */
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  cursor: pointer;
}

.div-table-col6 {
  width: 50%;  /* Designation */
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.div-table-col5 {
  width: auto;  /* Last Date */
  text-align: right;
  white-space: nowrap;
   overflow: hidden;
   text-overflow: ellipsis;
}
.opp-code-value {
  color: blueviolet;
  cursor: pointer;
}
.highlight {
  color: #6a1b9a;   /* violet / blue */
  font-weight: 600;
}
.highlight:hover {
  color: #8e24aa;     /* hover color */
  text-decoration: underline;
}
.no-data {
  justify-content: center;
  padding: 16px;
}

.no-data-text {
  color: #161414; 
  font-style: italic;
}
</style>