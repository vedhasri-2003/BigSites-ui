<template>
  <section id="jobseeker">
    <form id="appointment-form" role="form" method="post" action="#">
      <div class="col-md-12 col-sm-12">
        <div class="col-md-6 col-sm-6">
         <b-message type="is-info" has-icon style="font-size: 12px; max-width: 600px;">
                <h5>Welcome to Securo JOBZ!!..</h5>
                <h4>
                  Employeer Email-ID :
                  <a @click="viewJd()">{{ employerEmail }}</a>
                </h4>
                <h5>Click the above "Email-ID" to update</h5>
              </b-message>
          <h4>Interview on Process</h4>

         <div class="interview-box">
           <div class="opp-header">
  <div class="col-code-header"><b>Opportunity Code</b></div>
  <div class="col-desig-header"><b>Designation</b></div>
</div>

            <div v-for="(collapse, index) in postdata" :key="index">
             <div class="jd-header" @click="toggleCollapse(index)">
  <div class="col-code">{{ collapse.oppurtunityCode }}</div>
  <div class="col-desig">{{ collapse.oppurtunityDesignation }}</div>
</div>

              <transition name="slide-fade">
                <div v-if="collapseStates[index]" >
                  <div class="div-table "  style="background-color: darksalmon;">
                    <div class="div-table-row1" style="background-color: #ccc ">
                      <div class="div-table-col5"><b>Profile ID</b></div>
                      <div class="div-table-col6"><b>Name</b></div>
                    </div>
                   <div>
                    <div class="div-table-row" v-for="(prof, ndx) in collapse.profiles" :key="ndx">
                      <div class="div-table-col5">
                        <a @click="viewProfile(prof)" class="profile-link"> {{ prof.profileId }}</a>
                      </div>
                      <div class="div-table-col6">
                        {{ prof.profileName }}
                      </div>
                    </div>
                    </div>
                  </div>
                </div>
              </transition>
            </div>
          </div>
        </div>

        <div class="col-md-6 col-sm-6" v-if="visible">
          <h4 style="color: slateblue;">Profile Code - {{ profId }} </h4>

          <div class="div-table">
            <div class="div-table-row">

              <div class="col-md-12 col-sm-12">
                <div class="col-md-4 col-sm-4">
                  <b-label class="flright item">Name</b-label>
                </div>
                <div class="col-md-1 col-sm-1">
                  <b-label class="flright item">:</b-label>
                </div>
                <div class="col-md-7 col-sm-7">
                  {{ profName }}
                </div>
              </div>
              <div class="col-md-12 col-sm-12">
                <div class="col-md-4 col-sm-4">
                  <b-label class="flright item">Date of birth</b-label>
                </div>
                <div class="col-md-1 col-sm-1">
                  <b-label class="flright item">:</b-label>
                </div>
                <div class="col-md-7 col-sm-7">
                  {{ toUI(profdob) }}
                </div>
              </div>
              <div class="col-md-12 col-sm-12">
                <div class="col-md-4 col-sm-4">
                  <b-label class="flright item">Gender</b-label>
                </div>
                <div class="col-md-1 col-sm-1">
                  <b-label class="flright item">:</b-label>
                </div>
                <div class="col-md-7 col-sm-7">
                  {{ profGender }}
                </div>
              </div>
              <div class="col-md-12 col-sm-12">
                <div class="col-md-4 col-sm-4">
                  <b-label class="flright item">Mobile</b-label>
                </div>
                <div class="col-md-1 col-sm-1">
                  <b-label class="flright item">:</b-label>
                </div>
                <div class="col-md-7 col-sm-7">
                  {{ profMobile }}
                </div>
              </div>
              <div class="col-md-12 col-sm-12">
                <div class="col-md-4 col-sm-4">
                  <b-label class="flright item">Email</b-label>
                </div>
                <div class="col-md-1 col-sm-1">
                  <b-label class="flright item">:</b-label>
                </div>
                <div class="col-md-7 col-sm-7">
                  {{ profemail }}
                </div>
              </div>
              <div class="col-md-12 col-sm-12">
                <div class="col-md-4 col-sm-4">
                  <b-label class="flright item">Address</b-label>
                </div>
                <div class="col-md-1 col-sm-1">
                  <b-label class="flright item">:</b-label>
                </div>
                <div class="col-md-7 col-sm-7">
                  {{ profAddress }}
                </div>
              </div>
              <div class="col-md-12 col-sm-12">
                <div class="col-md-4 col-sm-4">
                  <b-label class="flright item">District</b-label>
                </div>
                <div class="col-md-1 col-sm-1">
                  <b-label class="flright item">:</b-label>
                </div>
                <div class="col-md-7 col-sm-7">
                  {{ profDistrict }}
                </div>
              </div>
              <div class="col-md-12 col-sm-12">
                <div class="col-md-4 col-sm-4">
                  <b-label class="flright item">State</b-label>
                </div>
                <div class="col-md-1 col-sm-1">
                  <b-label class="flright item">:</b-label>
                </div>
                <div class="col-md-7 col-sm-7">
                  {{ profstate }}
                </div>
              </div>
              <div class="col-md-12 col-sm-12">
                <div class="col-md-4 col-sm-4">
                  <b-label class="flright item">Pin code</b-label>
                </div>
                <div class="col-md-1 col-sm-1">
                  <b-label class="flright item">:</b-label>
                </div>
                <div class="col-md-7 col-sm-7">
                  {{ profPincode }}
                </div>
              </div>
              <div class="col-md-12 col-sm-12">
                <div class="col-md-4 col-sm-4">
                  <b-label class="flright item">Interview Status</b-label><span class="text-danger">*</span>
                </div>
                <div class="col-md-1 col-sm-1">
                  <b-label class="flright item">:</b-label>
                </div>
                <div class="col-md-7 col-sm-7">
                  <b-select v-model="interviewStatus" placeholder="Select status">
                    <option value="Selected">Selected</option>
                    <option value="Hold">Hold</option>
                    <option value="Rejected">Rejected</option>
                    <option value="Not attended">Not attended</option>
                  </b-select>
                </div>
                <br>
                <br>
              </div>

              <div class="col-md-12 col-sm-12">
                <div class="col-md-4 col-sm-4">
                  <b-label class="flright item">Remarks</b-label><span class="text-danger">*</span>
                </div>
                <div class="col-md-1 col-sm-1">
                  <b-label class="flright item">:</b-label>
                </div>
                <div class="col-md-7 col-sm-7">
                  <b-input v-model="remarks" type="textarea" rows="2"></b-input>
                </div>
              </div>
               <b-button
            class="button-wrapper"
            type="is-success"
            :disabled="!isFormValid"
            @click="doSubmit">Submit</b-button>
            </div>

          </div>
        </div>
      </div>

    </form>
  </section>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      visible: false,
      disabledFlag: true,
      profId: "",
      profName: "",
      profGender: "",
      profMail: "",
      profMobile: "",
      profState: "",
      profDistrict: "",
      profPincode: "",
      profAddress: "",
      profdob: "",
      postdata: [], 
      collapseStates: [],
      interviewStatus: "",
      employerEmail: '',
    remarks: "",
      
    };
    
  },
   computed: {
    isFormValid() {
      return (
        this.interviewStatus.trim() !== "" &&
        this.remarks.trim() 
      );
    },
  },
   mounted() {
    const storedLoggedUser = sessionStorage.getItem("loggedUser");
    if (!storedLoggedUser) {
      this.$router.push("");
      return;
    }

    let loggedUserObject = null;
    try {
      loggedUserObject = JSON.parse(storedLoggedUser);
    } catch (e) {
      console.error("Error parsing logged user:", e);
    }

    if (!loggedUserObject || loggedUserObject.userType !== "E") {
      this.$router.push("");
      return;
    }

    this.userId = loggedUserObject.userId;
    this.employerEmail = loggedUserObject.userEmail;
       this.fetchProfilers();
    },
  methods: {
    
    async fetchProfilers(){
          try{
            const res=await axios.get(`${this.$hostName}/api/v1/interview/opportunities/profiles`)
            this.postdata = res.data;
        this.collapseStates = this.postdata.map(() => false);

    } catch (err) {
        console.error("Fetch All Error:", err);
    }
  },
  toUI(dateStr) {
  if (!dateStr) return "";
  const d = new Date(dateStr);
  return (
    ("0" + d.getDate()).slice(-2) + "/" +
    ("0" + (d.getMonth() + 1)).slice(-2) + "/" +
    d.getFullYear()
  );
},
    viewProfile(p) {
      this.visible = true;
      this.jdcode = p.oppurtunityCode;
      this.designation = p.oppurtunityDesignation;
      this.profId = p.profileId;
      this.profName = p.profileName;
      this.profGender = p.profileGender;
      this.profAddress = p.address;
      this.profMobile = p.mobile;
      this.profdob = p.dob;
      this.profemail = p.email;
      this.profDistrict = p.district;
      this.profstate = p.state;
      this.profPincode = p.pincode;

    },
    toggleCollapse(index) {
      this.collapseStates[index] = !this.collapseStates[index];
    },
     async doSubmit() {
     if (!this.isFormValid) {
        this.$buefy.toast.open({
          message: 
             "⚠️ Please fill all required fields before submitting.",
          type: "is-danger",
          duration: 3000,
        });
        return;
      }
      this.modData = {
        empEmail: this.employerEmail,
        interviewId: this.interviewId,
       employerId:this.employerId,
       profileId:this.profId,
       status:this.interviewStatus,
       remark:this.remarks

       
      };

      try {
        let res;
          res = await axios.post(
            `${this.$hostName}/api/v1/interview-selection`,
            this.modData
          );
          this.$buefy.toast.open({
            message: " Record added successfully!",
            type: "is-success",
            duration: 3000,
          });
          return;

      } catch (err) {
        console.error("=== API ERROR ===");
        console.log(err.response?.data);

        this.$buefy.toast.open({
          message: " Error saving record.",
          type: "is-danger",
          duration: 3000,
        });
      }
    },
  },
  

    
}
</script>

<style scoped>
.text-danger {
  color: red;
}
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

.profile-row {
  display: flex;
  justify-content: space-between;
  padding: 8px;
  background-color: #f9f9f9;
  margin: 4px 0;
  border-radius: 2px;
  align-items: center;
}

.profile-col-id {
  width: 40%;
  color: #007BFF;
  font-weight: 600;
}

.profile-col-name {
  width: 55%;
  font-weight: 500;
}

.profile-link {
  cursor: pointer;
  text-decoration: underline;
}

.slide-fade-enter-active,
.slide-fade-leave-active {
  transition: all 0.5s ease;
}

.slide-fade-enter,
.slide-fade-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}
.profile-list-scroll {
  max-height: 200px; 
  overflow-y: auto;
  margin-top: 5px;
  border-top: 1px solid #ddd;
}
.opp-header {
  display: flex;
  width: 100%;
  max-width: 450px;
  background: #ccc;
  padding: 8px 10px;
  border-radius: 6px;
  font-weight: bold;
  margin-bottom: 10px;
}

.opp-col-code,
.opp-col-desig {
  display: inline-block;    
  margin-right: 20px;
  padding: 2px 4px;
}

.jd-header {
  display: flex;
  width: 100%;
  max-width: 450px;
  background: #f3f3f3;
  padding: 8px 10px;
  margin: 6px 0;
  border-radius: 4px;
  cursor: pointer;
}

.col-code-header,
.col-code {
  width: 150px;      
  white-space: nowrap; 
}

.col-desig-header,
.col-desig {
  flex: 1;            
  white-space: nowrap;
}

.col-code {
  color: blueviolet;
}
.interview-box {
  background: Seashell;
  padding: 10px;
  display: inline-block; 
  border-radius: 4px;
}

</style>