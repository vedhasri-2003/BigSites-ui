<template>
  <section id="myaccount">
    <form id="appointment-form" role="form" method="post" action="#">
      <div class="col-md-12 col-sm-12">
        <div class="col-md-6 col-sm-6">
          <!-- <b-message type="is-info" has-icon style="max-width: 550px;">
            <h4>Securo JOBZ invites "{{ employerEmail }}".</h4>
            <p>Employer's information displayed is duely shared by you</p>
          </b-message> -->
          <b-message type="is-info" has-icon style="font-size: 12px; max-width: 600px;">
                <h5>Welcome to Securo JOBZ!!..</h5>
                <h4>
                  Employeer Email-ID :
                  <a @click="viewJd()"><span class="highlight">{{ employerEmail }}</span></a>
                </h4>
                <h5>Click the above "Email-ID" to update</h5>
              </b-message>
          <div class="row">
            <ul class="nav navbar-nav navbar-center">
              <li>
                <!-- Opportunities(3) -->
                <RouterLink to="/employer/publish">Opportunities(3)</RouterLink>
              </li>
              <li>
                <!-- Profiles(6) -->
                <RouterLink to="/employer/profapplied">Profiles(6)</RouterLink>
              </li>
              <li>
                <!-- Selected(2) -->
                <RouterLink to="/employeer/profselcted">Selected(2)</RouterLink>
              </li>
              <li>
                <!-- Appointed(1) -->
                <RouterLink to="/employeer/profappt">Appointed(1)</RouterLink>
              </li>
            </ul>
          </div>
          <h4>My Account
            <!-- <a @click="viewJd()">(Click to Edit)</a> -->
          </h4>

          <div class="div-Table">
            <div class="div-table-col3">
              <div class="divCell">Emp.Code:</div>
              <div class="divCell">Organization :</div>
              <!-- <div class="divCell">Email.ID :</div> -->
              <div class="divCell">Phone :</div>
              <div class="divCell">Incharge :</div>
              <div class="divCell">Address :</div>
              <div class="divCell">State :</div>
                <div class="divCell">District :</div>
              <div class="divCell">Pin :</div>
            </div>
            <div class="div-table-col2">
              <div class="divCell">{{ employer_data?.empCd }}</div>
              <div class="divCell">{{ employer_data?.empNm }}</div>
              <!-- <div class="divCell">{{ employee_data?.employer_email }}</div> -->
              <!-- <div class="divCell">{{ employer_data?.empEmail }}</div> -->
              <div class="divCell">{{ employer_data?.empMob }}</div>
              <div class="divCell">{{ employer_data?.empIncharge }}</div>
              <div class="divCell">{{ employer_data?.empAddress }}</div>
               <div class="divCell">{{ employer_data?.empState }}</div>
              <div class="divCell">{{ employer_data?.empDistrict }}</div>
             
              <div class="divCell">{{ employer_data?.empPin }}</div>
            </div>
          </div>
        </div>
        
        <div class="col-md-6 col-sm-6 col-scroll" v-if="visible">
          
             <div class="col-md-12 col-sm-12 mb-0">
            <div class="col-md-4 col-sm-4">
              <label class="item">Code</label><span class="text-danger">*</span>
            </div>
            <div class="col-md-1 col-sm-1"><label class="item">:</label></div>
            <div class="col-md-7 col-sm-7">
              <b-input maxlength="50" v-model="code" />
            </div>
          </div>
          <div class="col-md-12 col-sm-12 mb-0">
            <div class="col-md-4 col-sm-4">
              <label class="item">Organization</label><span class="text-danger">*</span>
            </div>
            <div class="col-md-1 col-sm-1"><label class="item">:</label></div>
            <div class="col-md-7 col-sm-7">
              <b-input maxlength="50" v-model="organization" />
            </div>
          </div>
          <!-- <div class="col-md-12 col-sm-12 mb-0">
            <div class="col-md-4 col-sm-4">
              <label class="item">Email</label><span class="text-danger">*</span>
            </div>
            <div class="col-md-1 col-sm-1"><label class="item">:</label></div>
            <div class="col-md-7 col-sm-7">
              <b-input maxlength="50" v-model="employerEmail" />
            </div>
          </div> -->
<div class="col-md-12 col-sm-12 mb-0">
            <div class="col-md-4 col-sm-4">
              <label class="item">Phone</label><span class="text-danger">*</span>
            </div>
            <div class="col-md-1 col-sm-1"><label class="item">:</label></div>
            <div class="col-md-7 col-sm-7">
              <!-- <b-input maxlength="50" v-model="mob" /> -->
               <b-input maxlength="10" v-model="mob" placeholder="Enter 10-digit mobile number"
              type="tel" inputmode="numeric" required
             oninput="this.value= this.value.replace(/[^0-9]/g, '').slice(0,10)"
             :class="{'is-danger': mob && mob.length !==10}"/>
             <p v-if="mob && mob.length !==10" class="help is-danger"> Please enter a valid 10-digit mobile number.</p>
            
            </div>
          </div>
          <div class="col-md-12 col-sm-12 mb-0">
            <div class="col-md-4 col-sm-4">
              <label class="item">Incharge</label><span class="text-danger">*</span>
            </div>
            <div class="col-md-1 col-sm-1"><label class="item">:</label></div>
            <div class="col-md-7 col-sm-7">
              <b-input maxlength="50" v-model="incharge" />
            </div>
          </div>
          <div class="col-md-12 col-sm-12 mb-0">
            <div class="col-md-4 col-sm-4">
              <label class="item">Address</label><span class="text-danger">*</span>
            </div>
            <div class="col-md-1 col-sm-1"><label class="item">:</label></div>
            <div class="col-md-7 col-sm-7">
              <b-input maxlength="50" v-model="address" />
            </div>
          </div>
         
          
<div class="col-md-12 col-sm-12 mb-0">
  <div class="col-md-4 col-sm-4"><label class="item">State</label><span class="text-danger">*</span></div>
  <div class="col-md-1 col-sm-1"><label class="item">:</label></div>
  <div class="col-md-7 col-sm-7">
    <b-select 
      v-model="state" 
      placeholder="Select State"
      style="width:100%;"
      :class="{ 'is-danger': !state }"
    >
      <option value="">--Select--</option>
      <option v-for="s in stateList" :key="s" :value="s">{{ s }}</option>
    </b-select>

    <p v-if="!state" class="help is-danger">Please select a state.</p>
  </div>
</div>
<br>
<div class="col-md-12 col-sm-12 mb-0">
  <div class="col-md-4 col-sm-4"><label class="item">District</label><span class="text-danger">*</span></div>
  <div class="col-md-1 col-sm-1"><label class="item">:</label></div>
  <div class="col-md-7 col-sm-7">
    <b-select 
      v-model="district"
      placeholder="Select District"
      style="width:100%;"
      :class="{ 'is-danger': !dist }"
    >
      <option value="">--Select--</option>
      <option v-for="d in districtList" :key="d" :value="d">{{ d }}</option>
    </b-select>

    <p v-if="!district" class="help is-danger">Please select a district.</p>
  </div>
</div>
          <div class="col-md-12 col-sm-12 mb-0">
            <div class="col-md-4 col-sm-4">
              <label class="item">Pin Code</label><span class="text-danger">*</span>
            </div>
            <div class="col-md-1 col-sm-1"><label class="item">:</label></div>
            <div class="col-md-7 col-sm-7">
              <!-- <b-input maxlength="50" v-model="pin" /> -->
               <b-input maxlength="6" v-model="pin" placeholder="Enter 6-digit pincode"
              inputmode="numeric" required 
              oninput="this.value = this.value.replace(/[^0-9]/g, '').slice(0,6);
              this.dispatchEvent (new Event('input'))"
              :class="{'is-danger': pin && pin.length !==6}"></b-input>
          <p v-if="pin && pin.length !==6" class="help is-danger"> Please enter a valid 6-digit pincode.</p>

            </div>
          </div>
           <!-- :disabled="!isFormValid" -->
            <b-button
            class="button-wrapper"
            type="is-success"
           
            @click="doSubmit">Submit</b-button>
          </div>
      </div>
    </form>
  </section>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
    state: "",
      districtList: [],
stateList: [
  "Andhra Pradesh", "Arunachal Pradesh", "Assam", "Bihar", "Chhattisgarh",
  "Goa", "Gujarat", "Haryana", "Himachal Pradesh", "Jharkhand",
  "Karnataka", "Kerala", "Madhya Pradesh", "Maharashtra", "Manipur",
  "Meghalaya", "Mizoram", "Nagaland", "Odisha", "Punjab",
  "Rajasthan", "Sikkim", "Tamil Nadu", "Telangana", "Tripura",
  "Uttar Pradesh", "Uttarakhand", "West Bengal",
  "Andaman and Nicobar Islands", "Chandigarh", "Dadra and Nagar Haveli",
  "Daman and Diu", "Delhi", "Jammu and Kashmir", "Ladakh", "Lakshadweep",
  "Puducherry"
],
districtList: [
  // Telangana
  "Adilabad", "Bhadradri Kothagudem", "Hyderabad", "Jagtial", "Jangaon",
  "Jayashankar Bhupalpally", "Jogulamba Gadwal", "Kamareddy", "Karimnagar",
  "Khammam", "Komaram Bheem", "Mahabubabad", "Mahabubnagar", "Mancherial",
  "Medak", "Medchal–Malkajgiri", "Mulugu", "Nagarkurnool", "Nalgonda",
  "Narayanpet", "Nirmal", "Nizamabad", "Peddapalli", "Rajanna Sircilla",
  "Rangareddy", "Sangareddy", "Siddipet", "Suryapet", "Vikarabad",
  "Wanaparthy", "Warangal Rural", "Warangal Urban", "Yadadri Bhuvanagiri",

  // Andhra Pradesh
  "Anantapur", "Chittoor", "East Godavari", "Guntur", "Kadapa", "Krishna",
  "Kurnool", "Nellore", "Prakasam", "Srikakulam", "Visakhapatnam",
  "Vizianagaram", "West Godavari"
],
      disabledFlag: true,
      canApprove: false,
      visible: false,
      empId: "",
      employer_data: null,
      modData: {},
      code: "",
      organization: "",
      employerEmail: '',
      mob: "",
      incharge: "",
      address: "",
      district: "",
      state: "",
      pin: "",

    }
  },
  computed: {
    isFormValid() {
      return (
       this.organization.trim() &&
    this.employerEmail.trim() &&
        this.incharge &&
        this.mob.trim() &&
        this.district.trim() &&
        this.address.trim() &&
        this.state.trim() &&
        this.pin.trim() 
      );
    },
  },
  // mounted() {
  //   const storedLoggedUser = sessionStorage.getItem('loggedUser');
  //   if (null === storedLoggedUser || undefined === storedLoggedUser || storedLoggedUser.length === 0) {
  //     this.$router.push('');
  //   } else {
  //     let loggedUserObject = null;
  //     if (storedLoggedUser) {
  //         try {
  //           loggedUserObject = JSON.parse(storedLoggedUser);
  //         } catch (e) {
  //           loggedUserObject = null;
  //         }
  //     }

  //     if (null === loggedUserObject || undefined === loggedUserObject || loggedUserObject.length === 0) {
  //       console.error("Error parsing JSON from sessionStorage:", e);
  //     } else {
  //       if (loggedUserObject.userType !== 'E') {
  //         this.$router.push('');
  //       } else {
  //         this.employerEmail = loggedUserObject.userEmail;
  //         this.fetchEmployer(loggedUserObject.userId);
  //       }
  //     }
  //   }
  // },
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
  //  if(this.empId){
  //         this.fetchEmployer(this.empId);
  //       }
        
  //       this.fetchEmpBasedOnUserId(this.userId);
  this.fetchEmpBasedOnUserId(this.userId).then(() => {
    
    // 🔵 after empId is available, NOW fetch full details
    if (this.empId) {
      this.fetchEmployer(this.empId);
    }

  });
      // } 
    // this.fetchEmployer(this.empId);
    // this.fetchEmpBasedOnUserId(this.userId);
  },

  methods: {
    async fetchEmpBasedOnUserId(id) {
      console.log("fetchEmpBasedOnUserId",id);
      const url = this.$hostName + "/api/v1/employers/user/" + id;
      try {
        const res = await axios.get(url);
        this.employer_data = res.data;
        this.empId = res.data.empId;
        console.log("JSON.stringify(res.data)",JSON.stringify(res.data));
        sessionStorage.setItem("empDetails", JSON.stringify(res.data));
      } catch (err) {
        console.error("Error fetching emp: ", err);
      }
    },
    async fetchEmployer(empId) {
      console.log("gettingg fetch temployee id",empId);
      const url = this.$hostName + '/api/v1/employers/' + empId;
      await axios
      .get(url)
      .then(res => {
        console.log('=====>>> ', res.data)
        sessionStorage.setItem("employerDetails", JSON.stringify(res.data));
         
        this.employer_data = res.data;
        this.populateFormFields(res.data);
      })
      .catch(err => {
        this.employer_data = null;
        console.error('Error fetching employer: ', err)
      })
    },
    
populateFormFields(data) {
      if (!data) return;
    this.code = data.empCd || "";
  this.organization = data.empNm || "";
  this.employerEmail = data.empEmail || "";
  this.mob = data.empMob || "";
      this.address = data.empAddress || "";
      this.district = data.empDistrict || "";
      this.pin = data.empPin || "";
      this.state = data.empState || "";
      this.incharge = data.empIncharge || "";
      this.userId=data.empUserId||"";
    },
     viewJd() {
      this.disabledFlag = true;
      this.visible = true;
      this.populateFormFields(this.employer_data);
    },


    async doSubmit() {
      // if (!this.isFormValid) {
      //   this.$buefy.toast.open({
      //     message
      //       : "⚠️ Please fill all required fields before submitting.",
      //     type: "is-danger",
      //     duration: 3000,
      //   });
      //   return;
      // }

      const storedLoggedUser = sessionStorage.getItem("loggedUser");
      const loggedUserObject = JSON.parse(storedLoggedUser);

      this.modData = {
        empId: this.empId,
        empUserId:this.userId,
        empCd:this.code,
        empEmail: this.employerEmail,
        empNm: this.organization,
        empAddress: this.address,
        empDistrict: this.district,
        empPin: this.pin,
        empState: this.state,
        empIncharge: this.incharge,
        empApprovalFlag:'Y',
        empCreateDate:'',
        empDeleteFlag:'N',
        empMob:this.mob
       
      };

      try {
        let res;
       // console.log("res.data.empId",res.data.empId);
       // console.log("id",this.empId);
        if (this.empId) {
          const url = `${this.$hostName}/api/v1/employers/${this.empId}`;
          res = await axios.patch(url, this.modData);
        } else {
          const url = `${this.$hostName}/api/v1/employers`;
          res = await axios.post(url, this.modData);
        }

        this.empId = res.data.empId;
        await this.fetchEmployer(this.empId);

        this.$buefy.toast.open({
          message: "✅ Record saved successfully!",
          type: "is-success",
          duration: 3000,
        });

        this.visible = false;
      } catch (err) {
        console.error("Error saving profile:", err);
        this.$buefy.toast.open({
          message: "❌ Error saving record. Please try again.",
          type: "is-danger",
          duration: 3000,
        });
      }
    },
  }
}
</script>
<style scoped>
.col-scroll {
  max-height: 360px;
  overflow-y: scroll;
}
.highlight {
  color: #6a1b9a;   /* violet / blue */
  font-weight: 600;
}
.highlight:hover {
  color: #8e24aa;     /* hover color */
  text-decoration: underline;
}
</style>