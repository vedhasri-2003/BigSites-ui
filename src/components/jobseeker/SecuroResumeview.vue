<template>
  <section id="jdrecview">
    <div class="col-md-12 col-sm-12">
      <form id="appointment-form" role="form" method="post" action="#">
        <div class="col-md-6 col-sm-6">
          <div class="div-table">
            <div class="div-table-row">
              <b-message type="is-info" has-icon style="font-size: 12px; max-width: 600px;">
                <h5>Welcome to Securo JOBZ!!..</h5>
                <h4>
                  Profile Email-ID :
                  <!-- <a @click="viewJd(profile_data)"><span class="highlight">{{ profileEmail }}</span></a> -->
                   <a @click="viewJd(profile_data)"> <span class="highlight">{{ profileEmail }}</span></a>
                </h4>
                <h5>Click the above "Email-ID" to update</h5>
              </b-message>
              <h4>Hello {{ profile_data?.profileNm }}</h4>
              <div class="div-table-col3">
                <div class="divCell">Gender :</div>
                <div class="divCell">Qualification :</div>
                <div class="divCell">DOB :</div>
                <div class="divCell">Mobile :</div>
                <div class="divCell">Address :</div>
                <div class="divCell">State :</div>
                <div class="divCell">District :</div>
                <div class="divCell">Pin :</div>
                <div class="divCell">Experience :</div>
                <div class="divCell">Resume :</div>
              </div>
              <div class="div-table-col2">
                <div class="divCell">{{ profile_data?.profileGender }}</div>
                <div class="divCell">{{ profile_data?.profileEdu }}</div>
                <div class="divCell">{{ profile_data?.profileDob }}</div>
                <div class="divCell">{{ profile_data?.profileMob }}</div>
                <div class="divCell">{{ profile_data?.profileAddr }}</div>
                <div class="divCell">{{ profile_data?.profileState }}</div>
                <div class="divCell">{{ profile_data?.profileDist }}</div>
                <div class="divCell">{{ profile_data?.profilePin }}</div>
                <div class="divCell">{{ profile_data?.profileExp }}</div>
                <div class="divCell">{{ profile_data?.profileResume }}</div>
              </div>
            </div>
          </div>
        </div>

        <!-- Right-side Form -->
        <div class="col-md-6 col-sm-6 col-scroll" v-if="visible">
          <!-- Name -->
          <div class="col-md-12 col-sm-12 mb-0">
            <div class="col-md-4 col-sm-4">
              <label class="item">Name</label><span class="text-danger">*</span>
            </div>
            <div class="col-md-1 col-sm-1"><label class="item">:</label></div>
            <div class="col-md-7 col-sm-7">
              <b-input maxlength="50" v-model="name" :class="{ 'is-danger': !name.trim() && !isFormValid }" />
            </div>
          </div>
          <div class="col-md-12 col-sm-12 mb-0">
            <div class="col-md-4 col-sm-4">
              <label class="item">Gender</label><span class="text-danger">*</span>
            </div>
            <div class="col-md-1 col-sm-1"><label class="item">:</label></div>
            <div class="col-md-7 col-sm-7">
              <b-select v-model="gender" placeholder="Select Gender" required 
              style="width:100%;"
              :class="{ 'is-danger': !gender}">
            <option value="">--Select--</option>
            <option value="Male"> Male</option>
            <option value="Female"> Female </option>
             
            </b-select>
              <!-- <b-input maxlength="50" v-model="name" :class="{ 'is-danger': !name.trim() && !isFormValid }" /> -->
            </div>
          </div>

          <!-- Qualification -->
          <div class="col-md-12 col-sm-12 mb-0">
            <div class="col-md-4 col-sm-4">
              <label class="item">Qualification</label><span class="text-danger">*</span>
            </div>
            <div class="col-md-1 col-sm-1"><label class="item">:</label></div>
            <div class="col-md-7 col-sm-7">
              <b-input maxlength="50" v-model="qual" />
            </div>
          </div>

          <!-- DOB -->
          <div class="col-md-12 col-sm-12 mb-5">
            <div class="col-md-4 col-sm-4">
              <label class="item">DOB</label><span class="text-danger">*</span>
            </div>
            <div class="col-md-1 col-sm-1"><label class="item">:</label></div>
            <div class="col-md-7 col-sm-7">
              <b-datepicker
                v-model="dob"
                placeholder="Select date of birth"
                icon="calendar-today"
                :max-date="maxDob"
                :min-date="minDob"
                :class="{ 'is-danger': !dob && !isFormValid }"
              ></b-datepicker>
              <p v-if="dob && isUnder18" class="text-danger">❌ Must be 18 years or older.</p>
            </div>
          </div>

          <!-- Mobile -->
          <div class="col-md-12 col-sm-12 mb-0">
            <div class="col-md-4 col-sm-4">
              <label class="item">Mobile</label><span class="text-danger">*</span>
            </div>
            <div class="col-md-1 col-sm-1"><label class="item">:</label></div>
            <div class="col-md-7 col-sm-7">
              <b-input maxlength="10" v-model="mob" placeholder="Enter 10-digit mobile number"
              type="tel" inputmode="numeric" required
             oninput="this.value= this.value.replace(/[^0-9]/g, '').slice(0,10)"
             :class="{'is-danger': mob && mob.length !==10}"/>
             <p v-if="mob && mob.length !==10" class="help is-danger"> Please enter a valid 10-digit mobile number.</p>
            </div>
          </div>

          <!-- Email -->
          <!--<div class="col-md-12 col-sm-12 mb-0">
            <div class="col-md-4 col-sm-4">
              <label class="item">Email</label><span class="text-danger">*</span>
            </div>
            <div class="col-md-1 col-sm-1"><label class="item">:</label></div>
            <div class="col-md-7 col-sm-7">
              <b-input v-model="profileEmail" readonly />
            </div>
          </div> -->

          <!-- Address -->
          <div class="col-md-12 col-sm-12 mb-0">
            <div class="col-md-4 col-sm-4">
              <label class="item">Address</label><span class="text-danger">*</span>
            </div>
            <div class="col-md-1 col-sm-1"><label class="item">:</label></div>
            <div class="col-md-7 col-sm-7">
              <b-input maxlength="100" v-model="addr" />
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
          <!-- District -->
          <!-- <div class="col-md-12 col-sm-12 mb-0">
            <div class="col-md-4 col-sm-4"><label class="item">District</label><span class="text-danger">*</span></div>
            <div class="col-md-1 col-sm-1"><label class="item">:</label></div>
            <div class="col-md-7 col-sm-7"><b-input maxlength="100" v-model="dist" /></div>
          </div> -->
          <!-- :disabled="districtList.length === 0" -->
          <div class="col-md-12 col-sm-12 mb-0">
  <div class="col-md-4 col-sm-4"><label class="item">District</label><span class="text-danger">*</span></div>
  <div class="col-md-1 col-sm-1"><label class="item">:</label></div>
  <div class="col-md-7 col-sm-7">
    <b-select 
      v-model="dist"
      placeholder="Select District"
      style="width:100%;"
      :class="{ 'is-danger': !dist }"
    >
      <option value="">--Select--</option>
      <option v-for="d in districtList" :key="d" :value="d">{{ d }}</option>
    </b-select>

    <p v-if="!dist" class="help is-danger">Please select a district.</p>
  </div>
</div>

          <!-- Pincode -->
          <div class="col-md-12 col-sm-12 mb-0">
            <div class="col-md-4 col-sm-4"><label class="item">Pincode</label><span class="text-danger">*</span></div>
            <div class="col-md-1 col-sm-1"><label class="item">:</label></div>
            <div class="col-md-7 col-sm-7"><b-input maxlength="6" v-model="pin" placeholder="Enter 6-digit pincode"
              inputmode="numeric" required 
              oninput="this.value = this.value.replace(/[^0-9]/g, '').slice(0,6);
              this.dispatchEvent (new Event('input'))"
              :class="{'is-danger': pin && pin.length !==6}"></b-input>
            <!--validation message-->
          <p v-if="pin && pin.length !==6" class="help is-danger"> Please enter a valid 6-digit pincode.</p></div>

          </div>

          <!-- Experience -->
          <div class="col-md-12 col-sm-12 mb-5">
            <div class="col-md-4 col-sm-4"><label class="item">Experience</label><span class="text-danger">*</span></div>
            <div class="col-md-1 col-sm-1"><label class="item">:</label></div>
            <div class="col-md-7 col-sm-7">
              <b-select v-model="exp" placeholder="Select Experience" required 
              style="width:100%;"
              :class="{ 'is-danger': !exp}">
            <option value="">--select--</option>
            <option value="Fresher"> Fresher</option>
            <option value="1"> 1 </option>
              <option value="2"> 2</option>
              <option value="3"> 3</option>
              <option value="4"> 4</option>
              <option value="5">5</option>
              <option value="above 5 years"> Above 5 Years</option>
            </b-select>
          <!--validation message-->
        <p v-if="!exp" class="help is-danger">
          Please select your experience.
        </p></div>
          </div>

          <!-- Resume -->
          <div class="col-md-12 col-sm-12 mb-0">
            <div class="col-md-4 col-sm-4"><label class="item">Resume</label><span class="text-danger">*</span></div>
            <div class="col-md-1 col-sm-1"><label class="item">:</label></div>
            <div class="col-md-7 col-sm-7"><b-input maxlength="100" v-model="res" /></div>
          </div>

          <b-button
            class="button-wrapper"
            type="is-success"
            :disabled="!isFormValid || isUnder18"
            @click="doSubmit">Submit</b-button>
        </div>
      </form>
    </div>
  </section>
</template>

<script>
import axios from "axios";
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
      profileId: "",
      //profileEmail: "",
      profileEmail: JSON.parse(sessionStorage.getItem("loggedUser") || "{}").userEmail || "",
      disabledFlag: true,
      canApprove: false,
      visible: false,
      profile_data: null,
      modData: {},
      profileApproveFlag: "N",
gender:"",
      name: "",
      qual: "",
      dob: null,
      addr: "",
      dist: "",
      pin: "",
      mob: "",
      res: "",
      exp: "",
    };
  },

  computed: {
    isFormValid() {
      return (
        this.gender.trim()&&
        this.name.trim() &&
        this.dist.trim() &&
        this.qual.trim() &&
        this.dob &&
        this.mob.trim() &&
        this.profileEmail.trim() &&
        this.addr.trim() &&
        this.state.trim() &&
        this.dist.trim() &&
        this.pin.trim() &&
        this.exp.trim() &&
        this.res.trim()
      );
    },
    maxDob() {
      const today = new Date();
      today.setFullYear(today.getFullYear() - 18);
      return today;
    },
    minDob() {
      return new Date(1900, 0, 1);
    },
    isUnder18() {
      if (!this.dob) return false;
      const today = new Date();
      let age = today.getFullYear() - this.dob.getFullYear();
      const m = today.getMonth() - this.dob.getMonth();
      if (m < 0 || (m === 0 && today.getDate() < this.dob.getDate())) {
        age--;
      }
      return age < 18;
    },
  },

  mounted() {
    this.setLoggedUserData();
  
  },
methods: {
 
    setLoggedUserData() {
      const storedLoggedUser = sessionStorage.getItem("loggedUser");

      if (storedLoggedUser) {
        let loggedUserObject = null;
        try {
          loggedUserObject = JSON.parse(storedLoggedUser);
        } catch (e) {
          console.error("Error parsing logged user:", e);
          return;
        }

        if (!loggedUserObject || loggedUserObject.userType !== "J") {
          this.$router.push("");
          return;
        }

        this.userId = loggedUserObject.userId;
        this.profileEmail = loggedUserObject.userEmail || "";

        // Immediately show email and fetch data
        if(this.profileId){
          this.fetchProfileData(this.profileId);
        }
        
        this.fetchProfileBasedOnUserId(this.userId);
      } else {
        // Retry after small delay until sessionStorage is ready (post-login)
        setTimeout(() => this.setLoggedUserData(), 300);
      }
    },

  // methods: {
    async fetchProfileBasedOnUserId(id) {
      console.log("fetchProfileBasedOnUserId",id);
      const url = this.$hostName + "/api/v1/jobseekers/user/" + id;
      try {
        const res = await axios.get(url);
        this.profile_data = res.data;
        sessionStorage.setItem("agentDetails", JSON.stringify(res.data));
      } catch (err) {
        console.error("Error fetching agent: ", err);
      }
    },

    async fetchProfileData(id) {
      console.log("fetchProfileData",id);
      const url = `${this.$hostName}/api/v1/jobseekers/${id}`;
      try {
        const res = await axios.get(url);
        this.profile_data = res.data;
        sessionStorage.setItem("profileDetails", JSON.stringify(res.data));
        this.populateFormFields(res.data);
      } catch (err) {
        console.error("Error fetching profile:", err);
      }
    },

    populateFormFields(data) {
      if (!data) return;
     
      this.profileId=data.profileId || "",
      this.name = data.profileNm || "";
      this.gender=data.profileGender || "";
      this.qual = data.profileEdu || "";
      this.dob = data.profileDob ? new Date(data.profileDob) : null;
      this.mob = data.profileMob || "";
      this.addr = data.profileAddr || "";
      this.dist = data.profileDist || "";
      this.pin = data.profilePin || "";
      this.exp = data.profileExp || "";
      this.res = data.profileResume || "";
      this.state = data.profileState || "";
    },

    viewJd(d) {
      this.disabledFlag = true;
      this.visible = true;
      this.populateFormFields(d);
    },

    async doSubmit() {
      if (!this.isFormValid || this.isUnder18) {
        this.$buefy.toast.open({
          message: this.isUnder18
            ? "❌ You must be at least 18 years old."
            : "⚠️ Please fill all required fields before submitting.",
          type: "is-danger",
          duration: 3000,
        });
        return;
      }

      const formattedDob = this.dob.toISOString().split("T")[0];
      const storedLoggedUser = sessionStorage.getItem("loggedUser");
      const loggedUserObject = JSON.parse(storedLoggedUser);

      this.modData = {
        profileDist: this.dist,
        profileState: this.state,
        profileId: this.profileId,
        profileUserId: this.userId,
        profileEmail: this.profileEmail,
        profileNm: this.name,
        profileGender:this.gender,
        profileEdu: this.qual,
        profileDob: formattedDob,
        profileMob: this.mob,
        profileAddr: this.addr,
        profileDist: this.dist,
        profilePin: this.pin,
        profileExp: this.exp,
        profileResume: this.res,
        profileApproveFlag: "N",
      };

      try {
        let res;
        if (this.profileId) {
          const url = `${this.$hostName}/api/v1/jobseekers/${this.profileId}`;
          res = await axios.patch(url, this.modData);
        } else {
          const url = `${this.$hostName}/api/v1/jobseekers`;
          res = await axios.post(url, this.modData);
        }

        this.profileId = res.data.profileId;
        await this.fetchProfileData(this.profileId);

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
   },
};
</script>

<style scoped>
.text-danger {
  color: red;
}
.col-scroll {
  max-height: 360px;
  overflow-y: scroll;
}
.col-md-12.mb-0 {
  display: flex;
  align-items: center;
  margin-bottom: 16px !important; /* Even spacing across all rows */
}

/* ✅ Make all inputs and datepickers the same height */
.b-input,
.b-datepicker,
input,
.b-datepicker .control input {
  height: 38px !important;
  min-height: 38px !important;
  font-size: 14px;
}

/* ✅ Ensure labels are vertically aligned */
label.item {
  display: flex;
  align-items: center;
  height: 38px;
  font-weight: 500;
}

/* ✅ Adjust spacing around label and colon */
.col-md-4.col-sm-4,
.col-md-1.col-sm-1,
.col-md-7.col-sm-7 {
  display: flex;
  align-items: center;
}
.highlight {
  color: #6a1b9a;      /* violet */
  font-weight: 600;
  cursor: pointer;
}

.highlight:hover {
  color: #8e24aa;     /* hover color */
  text-decoration: underline;
}
/* ✅ Responsive fine-tuning */
@media (max-width: 992px) {
  .col-md-12.mb-0 {
    margin-bottom: 14px !important;
  }
}

@media (max-width: 576px) {
  .col-md-12.mb-0 {
    flex-direction: column;
    align-items: flex-start;
    margin-bottom: 12px !important;
  }

  .col-md-4.col-sm-4,
  .col-md-1.col-sm-1,
  .col-md-7.col-sm-7 {
    width: 100%;
  }
  
}


</style>
