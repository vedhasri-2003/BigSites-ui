<template>
  <section id="jdrecview">
    <div class="col-md-12 col-sm-12">
      <form id="appointment-form" role="form" method="post" action="#">
        <div class="col-md-6 col-sm-6">
          <div class="div-table">
            <div class="div-table-row">
              <b-message type="is-info" has-icon style="font-size: 12px; max-width: 520px">
                <h5>Welcome to Securo JOBZ!!..</h5>
                <h4>
                  Agent Id :
                  <a @click="viewJd(agent_data)">{{ agentEmail }}</a>
                </h4>
                <h5>Click the above "Agent Id" to update</h5>
              </b-message>
              <h6>Agent Detail:</h6>
              <div class="div-table-col3">
                <div class="divCell">Name :</div>
                <div class="divCell">Mobile :</div>
                <div class="divCell">Email :</div>
                <div class="divCell">Address :</div>
                <div class="divCell">District :</div>
                <div class="divCell">State :</div>
                <div class="divCell">Pin :</div>
                <div class="divCell">UPI :</div>
              </div>
              <div class="div-table-col2">
                <div class="divCell">{{ agent_data?.agentNm }}</div>
                <div class="divCell">{{ agent_data?.agentMob }}</div>
                <div class="divCell">{{ agentEmail }}</div>
                <div class="divCell">{{ agent_data?.agentAddr }}</div>
                <div class="divCell">{{ agent_data?.agentDist }}</div>
                <div class="divCell">{{ agent_data?.agentState }}</div>
                <div class="divCell">{{ agent_data?.agentPin }}</div>
                <div class="divCell">{{ agent_data?.agentUpi }}</div>
              </div>
            </div>
          </div>
        </div>

        <div class="col-md-6 col-sm-6 col-scroll" v-if="visible">
          <div class="col-md-12 col-sm-12 mb-0">
            <div class="col-md-4 col-sm-4">
              <label class="item">Name</label>
            </div>
            <div class="col-md-1 col-sm-1">
              <label class="item">:</label>
            </div>
            <div class="col-md-7 col-sm-7">
              <b-input maxlength="50" v-model="name"></b-input>
            </div>
          </div>

          <div class="col-md-12 col-sm-12 mb-0">
            <div class="col-md-4 col-sm-4">
              <label class="item">Mobile</label>
            </div>
            <div class="col-md-1 col-sm-1">
              <label class="item">:</label>
            </div>
            <div class="col-md-7 col-sm-7">
              <b-input maxlength="50" v-model="mob"></b-input>
            </div>
          </div>

          <div class="col-md-12 col-sm-12 mb-0">
            <div class="col-md-4 col-sm-4">
              <label class="item">Address</label>
            </div>
            <div class="col-md-1 col-sm-1">
              <label class="item">:</label>
            </div>
            <div class="col-md-7 col-sm-7">
              <b-input maxlength="100" v-model="addr"></b-input>
            </div>
          </div>

          <div class="col-md-12 col-sm-12 mb-0">
            <div class="col-md-4 col-sm-4">
              <label class="item">District</label>
            </div>
            <div class="col-md-1 col-sm-1">
              <label class="item">:</label>
            </div>
            <div class="col-md-7 col-sm-7">
              <b-input maxlength="100" v-model="dist"></b-input>
            </div>
          </div>

          <div class="col-md-12 col-sm-12 mb-0">
            <div class="col-md-4 col-sm-4">
              <label class="item">State</label>
            </div>
            <div class="col-md-1 col-sm-1">
              <label class="item">:</label>
            </div>
            <div class="col-md-7 col-sm-7">
              <b-input maxlength="100" v-model="state"></b-input>
            </div>
          </div>

          <div class="col-md-12 col-sm-12 mb-0">
            <div class="col-md-4 col-sm-4">
              <label class="item">Pincode</label>
            </div>
            <div class="col-md-1 col-sm-1">
              <label class="item">:</label>
            </div>
            <div class="col-md-7 col-sm-7">
              <b-input maxlength="100" v-model="pin"></b-input>
            </div>
          </div>

          <div class="col-md-12 col-sm-12 mb-0">
            <div class="col-md-4 col-sm-4">
              <label class="item">UPI-Code</label>
            </div>
            <div class="col-md-1 col-sm-1">
              <label class="item">:</label>
            </div>
            <div class="col-md-7 col-sm-7">
              <b-input maxlength="100" v-model="upi"></b-input>
            </div>
          </div>

          <b-button class="button-wrapper" type="is-success" @click="doSubmit"> Submit </b-button>
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
      agentId: 1,
      disabledFlag: true,
      canApprove: false,
      visible: false,
      agent_data: null,
      modData: {},
      agentEmail: '',
      name: '',
      mob: '',
      addr: '',
      dist: '',
      state: '',
      pin: '',
      upi: '',
    }
  },
  mounted() {
    const storedLoggedUser = sessionStorage.getItem('loggedUser')
    if (
      null === storedLoggedUser ||
      undefined === storedLoggedUser ||
      storedLoggedUser.length === 0
    ) {
      this.$router.push('')
    } else {
      let loggedUserObject = null
      if (storedLoggedUser) {
        try {
          loggedUserObject = JSON.parse(storedLoggedUser)
        } catch (e) {
          loggedUserObject = null
        }
      }

      if (
        null === loggedUserObject ||
        undefined === loggedUserObject ||
        loggedUserObject.length === 0
      ) {
        console.error('Error parsing JSON from sessionStorage:', e)
      } else {
        if (loggedUserObject.userType !== 'A') {
          this.$router.push('')
        } else {
          this.agentEmail = loggedUserObject.userEmail
          this.userId=loggedUserObject.userId
          this.fetchAgent(loggedUserObject.userId)
        }
      }
    }
  },
  methods: {
    async fetchAgent(id) {
      const url = this.$hostName + '/api/v1/agents/' + id
      await axios
        .get(url)
        .then((res) => {
          console.log('=====>>> ', res.data)
          sessionStorage.setItem('agentDetails', JSON.stringify(res.data))
          this.agent_data = res.data
        })
        .catch((err) => {
          this.agent_data = null
          console.error('Error fetching agent: ', err)
        })
    },
    viewJd(d) {
      this.visible = true
      this.disabledFlag = true
      this.agentId = d.agentId
      this.name = d.agentNm
      this.mob = d.agentMob
      this.addr = d.agentAddr
      this.dist = d.agentDist
      this.state = d.agentState
      this.pin = d.agentPin
      this.upi = d.agentUpi
    },
    async doSubmit() {
      console.log('Submit Button clicked !!')
      this.modData.agentNm = this.name
      this.modData.agentMob = this.mob
      this.modData.agentAddr = this.addr
      this.modData.agentDist = this.dist
      this.modData.agentState = this.state
      this.modData.agentPin = this.pin
      this.modData.agentUpi = this.upi
      const url = this.$hostName + '/api/v1/agents/' + this.userId
      await axios
        .patch(url, this.modData)
        .then((res) => {
          console.log('=====>>> ', res.data)
          sessionStorage.setItem('agentDetails', JSON.stringify(res.data))
          this.agent_data = res.data
          this.visible = false
        })
        .catch((err) => {
          this.agent_data = null
          console.error('Error modifying agent: ', err)
        })
    },
  },
}
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
</style>
