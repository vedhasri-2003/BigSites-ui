<template>
  <section id="jdpost">
    <div class="col-md-12 col-sm-12">
      <form id="appointment-form" role="form" method="post" action="#">
        <div class="col-md-6 col-sm-6">

          <b-message type="is-info" has-icon style="font-size: 12px; max-width: 650px;">
            <h5>Welcome to Securo JOBZ!!..</h5>
            <h4>Profile Email-ID : <span class="highlight">{{ profileEmail }}</span></h4>
            <h5>Job Seekers could view Opportunities by selecting Opportunity Code!</h5>
          </b-message>

          <h4>List of Opportunities</h4>

          <div class="heading" style="background-color: SeaShell;">
            <div class="div-table-row" style="background-color: #ccc;">
              <div class="div-table-col3"><b>Opportunity.Code</b></div>
              <div class="div-table-col6"><b>Designation</b></div>
              <div class="div-table-col5"><b>Last Date</b></div>
            </div>
            <div class="div-table-row" v-for="opp in opportunities_data" :key="opp.id">
              <div class="div-table-col3 opp-code-value">
                <a @click="viewJd(opp)" v-b-tooltip.hover title="Click here for Details">
                  <span style="color: blueviolet">{{ opp?.oppurtunityCode }}</span>
                </a>
              </div>
              <div class="div-table-col6">{{ opp?.oppurtunityDesignation }}</div>
              <div class="div-table-col5">{{ toUI(opp?.oppurtunityLastDate) }}</div>
            </div>
          </div>
        </div>

        <div class="col-md-6 col-sm-6" v-if="visible">

          <h4>Opportunity.Code: {{ jdCode }}</h4>

          <div class="div-table">

            <div class="col-md-12 col-sm-12">
              <div class="col-md-4 col-sm-4"><b-label class="flright item">Employer Name</b-label></div>
              <div class="col-md-1 col-sm-1"><b-label class="flright item">:</b-label></div>
              <div class="col-md-7 col-sm-7">{{ empNm }}</div>
            </div>

            <div class="col-md-12 col-sm-12">
              <div class="col-md-4 col-sm-4"><b-label class="flright item">Designation</b-label></div>
              <div class="col-md-1 col-sm-1"><b-label class="flright item">:</b-label></div>
              <div class="col-md-7 col-sm-7">{{ designation }}</div>
            </div>

            <div class="col-md-12 col-sm-12">
              <div class="col-md-4 col-sm-4"><b-label class="flright item">Location</b-label></div>
              <div class="col-md-1 col-sm-1"><b-label class="flright item">:</b-label></div>
              <div class="col-md-7 col-sm-7">{{ location }}</div>
            </div>

            <div class="col-md-12 col-sm-12">
              <div class="col-md-4 col-sm-4"><b-label class="flright item">Description</b-label></div>
              <div class="col-md-1 col-sm-1"><b-label class="flright item">:</b-label></div>
              <div class="col-md-7 col-sm-7">{{ jdesc }}</div>
            </div>

            <div class="col-md-12 col-sm-12">
              <div class="col-md-4 col-sm-4"><b-label class="flright item">Last.Dt</b-label></div>
              <div class="col-md-1 col-sm-1"><b-label class="flright item">:</b-label></div>
              <div class="col-md-7 col-sm-7">{{ lastDt }}</div>
            </div>

            <div class="col-md-12 col-sm-12">
              <div class="col-md-4 col-sm-4"><b-label class="flright item">Interested</b-label></div>
              <div class="col-md-1 col-sm-1"><b-label class="flright item">:</b-label></div>
              <div class="col-md-7 col-sm-7">
                <b-field>
                  <b-checkbox v-model="cbConfirm" true-value="Yes" false-value="No">
                    {{ cbConfirm }}
                  </b-checkbox>
                </b-field>
              </div>

              <div class="row" style="margin-left:15px; margin-top:10px;">
                <a style="font-size:15px"><b>Important: </b>If interested click YES in the checkbox</a>
               
              </div>
               <b-button class="button-wrapper" type="is-success" @click="doSubmit">
                  Submit
                </b-button>
            </div>

            <br />

          </div>
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
      visible: false,
      oppurtunityId: "",
      opportunities_data: null,

      designation: "",
      location: "",
      jdesc: "",
      jdCode: "",
      lastDt: "",

      cbConfirm: "No",

      profileEmail: JSON.parse(sessionStorage.getItem("loggedUser") || "{}").userEmail || "",
      profileId: JSON.parse(sessionStorage.getItem("loggedUser") || "{}").profileId || "",

      profileeee_data: null,
      profileId: "",
      userId: "",
      empNm: "",
      modData: {}
    };
  },

  mounted() {
    this.setLoggedUserData();
  },

  methods: {
    async fetchProfileBasedOnUserIdd(id) {
      console.log("fetchProfileBasedOnUserId", id);
      const url = this.$hostName + "/api/v1/jobseekers/user/" + id;

      try {
        const res = await axios.get(url);
        this.profileeee_data = res.data;
        this.profileId = res.data.profileId;
        this.fetchOpp(this.profileId);
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
        console.log("-----------------",this.empNm);
        this.empNm = res.data.empNm;
      } catch (err) {
        console.error("Error fetching employer:", err);
        this.empNm = "";
      }
    },

    async fetchOpp(profileId) {
      console.log("profileid",profileId);
      const url = this.$hostName + `/api/v1/oppurtunity/unselected/${profileId}`;

      try {
        const res = await axios.get(url);
        this.opportunities_data = res.data;
      } catch (err) {
        console.error("Error fetching opportunities:", err);
      }
    },

    populateFormFields(d) {
      if (!d) return;
      this.empNm = d.empNm || "";
      this.jdCode = d.oppurtunityCode || "";
      this.jdesc = d.oppurtunityJobDescription || "";
      this.location = d.oppurtunityLocation || "";
      this.designation = d.oppurtunityDesignation || "";
      this.lastDt = this.toUI(d.oppurtunityLastDate) || "";
    },

    viewJd(d) {
      this.visible = true;
      this.oppurtunityId = d.oppurtunityId;

      this.populateFormFields(d);

      if (d.oppurtunityEmployerId) {
        this.fetchEmployerById(d.oppurtunityEmployerId);
      } else {
        this.empNm = "";
      }
    },

    toUI(dateStr) {
      if (!dateStr) return null;
      const d = new Date(dateStr);
      return (
        ("0" + d.getDate()).slice(-2) + "/" +
        ("0" + (d.getMonth() + 1)).slice(-2) + "/" +
        d.getFullYear()
      );
    },

    async doSubmit() {
      this.modData = {
        oppurtunityId: this.oppurtunityId,
        profileId: this.profileId,
        status: this.cbConfirm
      };

      try {
        const url = `${this.$hostName}/api/v1/oppurtunity-selection`;
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
};
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
.heading {
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
  color: #6a1b9a;      /* violet */
  font-weight: 600;
  cursor: pointer;
}

.highlight:hover {
  color: #8e24aa;     /* hover color */
  text-decoration: underline;
}
</style>
