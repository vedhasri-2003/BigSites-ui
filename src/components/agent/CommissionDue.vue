<template>
  <section id="jdrecview">
    <div class="col-md-12 col-sm-12">
      <form id="appointment-form" role="form" method="post" action="#">
        <div class="col-md-6 col-sm-6">
          <CommonHead
            :agentNm = "agentNm"
            :agentEmail = "agentEmail"
          />

          <h6>Commission Due</h6>
          <div class="col-md-12 col-sm-12 profile-table-head">
            <div class="col-md-5 col-sm-5 page-font"><b>Profile Email</b></div>
            <div class="col-md-5 col-sm-5 page-font"><b>Name</b></div>
            <div class="col-md-2 col-sm-2 page-font"><b>Approved</b></div>
          </div>

          <div class=" profile-table">
            <div class="col-md-12 col-sm-12" v-for="d in postdata" :key="d?.profileId">
              <div class="col-md-5 col-sm-5 page-font">
                <a @click="viewJd(d)">
                  <span style="color: blueviolet">{{ d?.profileEmail }}</span>
                </a>
              </div>
              <div class="col-md-5 col-sm-5 page-font">{{ d?.profileNm }}</div>
              <div class="col-md-2 col-sm-2 page-font">{{ d?.profileApproveFlag }}</div>
            </div>
          </div>
        </div>

        <div class="col-md-6 col-sm-6 col-scroll" v-if="visible">
          <div class="row">
            <div class="col-md-12 col-sm-12 mb-0">
              <div class="col-md-4 col-sm-4">
                <label class="item">Name</label>
              </div>
              <div class="col-md-1 col-sm-1">
                <label class="item">:</label>
              </div>
              <div class="col-md-7 col-sm-7">
                {{ name }}
              </div>
            </div>

            <div class="col-md-12 col-sm-12 mb-0">
              <div class="col-md-4 col-sm-4">
                <label class="item">Date Of Birth</label>
              </div>
              <div class="col-md-1 col-sm-1">
                <label class="item">:</label>
              </div>
              <div class="col-md-7 col-sm-7">
                {{ dob }}
              </div>
            </div>

            <div class="col-md-12 col-sm-12 mb-2">
              <div class="col-md-4 col-sm-4">
                <label class="item">Gender</label>
              </div>
              <div class="col-md-1 col-sm-1">
                <label class="item">:</label>
              </div>
              <div class="col-md-7 col-sm-7">
                <span v-if="gender==='M'">Male</span>
                <span v-else-if="gender==='F'">Female</span>
                <span v-else>Transgender</span>
              </div>
            </div>

            <div class="col-md-12 col-sm-12 mb-2">
              <div class="col-md-4 col-sm-4">
                <label class="item">Mobile</label>
              </div>
              <div class="col-md-1 col-sm-1">
                <label class="item">:</label>
              </div>
              <div class="col-md-7 col-sm-7">
                {{ mobile }}
              </div>
            </div>

            <div class="col-md-12 col-sm-12 mb-2">
              <div class="col-md-4 col-sm-4">
                <label class="item">Email</label>
              </div>
              <div class="col-md-1 col-sm-1">
                <label class="item">:</label>
              </div>
              <div class="col-md-7 col-sm-7">
                {{ email }}
              </div>
            </div>

            <div class="col-md-12 col-sm-12 mb-2">
              <div class="col-md-4 col-sm-4">
                <label class="item">Address</label>
              </div>
              <div class="col-md-1 col-sm-1">
                <label class="item">:</label>
              </div>
              <div class="col-md-7 col-sm-7">
                <b-input type="textarea" v-model="address" readonly></b-input>
              </div>
            </div>

            <div class="col-md-12 col-sm-12 mb-2">
              <div class="col-md-4 col-sm-4">
                <label class="item">District</label>
              </div>
              <div class="col-md-1 col-sm-1">
                <label class="item">:</label>
              </div>
              <div class="col-md-7 col-sm-7">
                {{ district }}
              </div>
            </div>

            <div class="col-md-12 col-sm-12 mb-2">
              <div class="col-md-4 col-sm-4">
                <label class="item">State</label>
              </div>
              <div class="col-md-1 col-sm-1">
                <label class="item">:</label>
              </div>
              <div class="col-md-7 col-sm-7">
                {{ state }}
              </div>
            </div>

            <div class="col-md-12 col-sm-12 mb-2">
              <div class="col-md-4 col-sm-4">
                <label class="item">Pincode</label>
              </div>
              <div class="col-md-1 col-sm-1">
                <label class="item">:</label>
              </div>
              <div class="col-md-7 col-sm-7">
                {{ pincode }}
              </div>
            </div>

            <div class="col-md-12 col-sm-12 mb-2">
              <div class="col-md-4 col-sm-4">
                <label class="item">Resume</label>
              </div>
              <div class="col-md-1 col-sm-1">
                <label class="item">:</label>
              </div>
              <div class="col-md-7 col-sm-7">
                <b-input type="textarea" v-model="resume" readonly></b-input>
              </div>
            </div>

            <div v-if="!addVisible" class="col-md-12 col-sm-12 mb-2">
              <div class="col-md-4 col-sm-4">
                <label class="item">Created Date</label>
              </div>
              <div class="col-md-1 col-sm-1">
                <label class="item">:</label>
              </div>
              <div class="col-md-7 col-sm-7">
                {{ createDate }}
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
import CommonHead from './CommonHead.vue';
export default {
  components: {
    CommonHead,
  },
  data() {
    return {
      visible: false,
      addVisible: false,
      disabledFlag: true,
      canApprove: false,
      isEditing: false,
      agentId: -1,
      agentNm: "",
      successMessage: "",
      jsCode: "",
      name: "",
      mobile: "",
      email: "",
      address: "",
      district: "",
      state: "",
      resume: "",
      pincode: "",
      createDate: "",
      proapr: "",
      commflg: "",
      agcode: "",
      upiid: "",
      bankAccount: "",
      cbConfirm: "No",
      ifscCode: "",
      dob: "",
      resume: "",
      gender: "",
      agentEmail: "",
      postdata: [],
    };
  },
  mounted() {
    this.extractFromStorage('loggedUser');
    if ("SUCCESS" === this.successMessage) {
      this.extractFromStorage('agentDetails');
      if ("SUCCESS" === this.successMessage) {
        this.fetchProfilesWithCommissionDue(this.agentId);
      }
    }
  },
  methods: {
    extractFromStorage(o) {
      this.successMessage = "";
      const sessionObject = sessionStorage.getItem(o);
      if (null === sessionObject || undefined === sessionObject || sessionObject.length === 0) {
        if (o === 'loggedUser') {
          this.$router.push('');
        }
      } else {
        let storedObject = null;
        if (sessionObject) {
          try {
            storedObject = JSON.parse(sessionObject);
          } catch (e) {
            storedObject = null;
          }
        }

        if (null === storedObject || undefined === storedObject || storedObject.length === 0) {
          console.error("Error parsing JSON from sessionStorage:", e);
        } else {
          if (o === 'loggedUser') {
            if (storedObject.userType === 'A') {
              this.agentEmail = storedObject.userEmail;
              this.successMessage = "SUCCESS";
            } else {
              this.$router.push('');
            }
          } else if (o === 'agentDetails') {
            this.agentId = storedObject.agentId;
            this.agentNm = storedObject.agentNm;
            this.successMessage = "SUCCESS";
          }
        }
      }
    },

    async fetchProfilesWithCommissionDue(id) {
      const url = this.$hostName + '/api/v1/agents/profilesCommissionDue/' + id;
      await axios
        .get(url)
        .then(res => {
          console.log('=====>>> ', res.data)
          this.postdata = res.data
        })
        .catch(err => {
          this.postdata = [];
          console.error('Error fetching agent: ', err)
        })
    },

    viewJd(d) {
      this.visible = true;
      this.addVisible = false;
      this.disabledFlag = false;
      this.jsCode = d.profileCd;
      this.name = d.profileNm;
      this.mobile = d.profileMob;
      this.email = d.profileEmail;
      this.address = d.profileAddr;
      this.district = d.profileDist;
      this.state = d.profileState;
      this.resume = d.profileResume;
      this.pincode = d.profilePin;
      this.createDate = d.profileCreateDate;
      this.proapr = d.profileApproveFlag;
      this.commflg = d.profileCommissionFlag;
      this.dob = d.profileDob;
      this.gender = d.profileGender;
    },
  },
};
</script>

<style scoped>
  .padding8 {
    padding-top: 8px;
  }

  .col-scroll {
    max-height: 360px;
    overflow-y: scroll;
  }

  .flright {
    float: left;
  }

  .item {
    font-weight: 700;
    display: flex;
  }

  .profile-table-head {
    background-color: #ccc;
    border: 1px solid;
    display: flex;
  }

  .profile-table {
    overflow-y: scroll;
    max-height: 150px;
    border: 1px solid;
    background-color: SeaShell;
  }

  .button-wrapper {
    display: flex;
    justify-content: center;
    margin-top: 1rem;
  }
</style>
