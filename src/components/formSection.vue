<template>
  <div class="py-6">
    <div>
      <v-form ref="form" v-model="form_model" lazy-validation>
        <!-- date activePicker -->
        <v-row>
          <v-col cols="6" md="3">
            <v-menu
              ref="menu"
              v-model="menu"
              :close-on-content-click="true"
              transition="scale-transition"
              offset-y
            >
              <template v-slot:activator="{ on, attrs }">
                <v-text-field
                  outlined
                  v-model="date"
                  label="Date of Error"
                  prepend-icon="mdi-calendar"
                  readonly
                  v-bind="attrs"
                  v-on="on"
                  required
                  :rules="date_rules"
                ></v-text-field>
              </template>
              <v-date-picker
                v-model="date"
                :active-picker.sync="activePicker"
                :max="
                  new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
                    .toISOString()
                    .substr(0, 10)
                "
                min="1950-01-01"
              ></v-date-picker>
            </v-menu>
          </v-col>
          <v-col cols="6" md="3">
            <v-menu
              v-model="time"
              :close-on-content-click="false"
              :return-value.sync="time"
              transition="scale-transition"
              offset-y
            >
              <template v-slot:activator="{ on, attrs }">
                <v-text-field
                  v-model="timeModel"
                  label="Time of error"
                  prepend-icon="mdi-clock-time-four-outline"
                  readonly
                  v-bind="attrs"
                  v-on="on"
                  outlined
                  required
                  :rules="time_rules"
                ></v-text-field>
              </template>
              <v-time-picker
                v-if="time"
                v-model="timeModel"
                @click:minute="$refs.menu.save(time)"
              ></v-time-picker>
            </v-menu>
          </v-col>
          <v-col cols="6" md="3">
            <v-select
              required
              :items="genderModel"
              label="Gender"
              outlined
              :rules="gender_rules"
            ></v-select>
          </v-col>
          <v-col cols="6" md="3">
            <v-select
              required
              :items="get_age_data"
              label="age"
              outlined
              :rules="age_rules"
            ></v-select>
          </v-col>

          <v-col md="6">
            <v-text-field
              v-model="diagnosis_model"
              :rules="diagnosis_rules"
              :counter="200"
              label="Diagnosis"
              required
              outlined
            ></v-text-field>
          </v-col>
          <v-col md="6">
            <v-select
              :items="get_area_of_error"
              label="area of error"
              v-model="area_of_error_model"
              outlined
              required
              :rules="area_of_error_rules"
            ></v-select>
          </v-col>
          <v-col md="6">
            <v-select
              :items="get_type_of_error"
              label="type of error"
              v-model="type_of_error_model"
              outlined
              required
              :rules="type_of_error_rules"
            ></v-select>
          </v-col>
          <v-col md="6">
            <v-select
              :items="outcome_of_error_data"
              label="outcome of error"
              outlined
              required
              v-model="outcome_of_error_model"
              :rules="outcome_of_error_rules"
            ></v-select>
          </v-col>
          <v-col md="6">
            <!-- <p class="font-weight-bold">
              Possible factors leading to the error *
            </p> -->
            <v-textarea
              name="input-7-1"
              label="possible factors contributing to the error"
              auto-grow
              outlined
              required
              v-model="possible_causes_model"
              :rules="possible_causes_rules"
            ></v-textarea>
          </v-col>
          <v-col md="6">
            <v-textarea
              name="input-7-1"
              label="suggested preventive measures"
              auto-grow
              outlined
              required
              v-model="suggestions_model"
              :rules="suggestions_rules"
            ></v-textarea>
          </v-col>
          <v-col cols="12">
            <p class="font-weight-bold text-uppercase">
              all the data submitted via this form is secure and confidential
            </p>
          </v-col>
          <v-btn
            :disabled="!form_model"
            color="primary"
            class="mr-4"
            type="submit"
            @click="validate"
          >
            submit
          </v-btn>
        </v-row>
      </v-form>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      activePicker: null,
      form_model: true,
      date: null,
      date_rules: [(v) => !!v || "Date is required"],
      menu: false,
      time: null,
      timeModel: null,
      time_rules: [(v) => !!v || "Time is required"],
      genderModel: ["Male", "Female"],
      gender_rules: [(v) => !!v || "Gender is required"],
      dateModel: null,
      diagnosis_model: null,
      diagnosis_rules: [(v) => !!v || "Diagnosis is required"],
      ageModel: null,
      age_rules: [(v) => !!v || "Time is required"],
      area_of_error_model: null,
      area_of_error_rules: [(v) => !!v || "Area of Error is required"],
      type_of_error_model: null,
      type_of_error_rules: [(v) => !!v || "Type of Error is required"],
      outcome_of_error_model: null,
      outcome_of_error_rules: [(v) => !!v || "Outcome of Error is required"],
      possible_causes_model: null,
      possible_causes_rules: [
        (v) => !!v || "Possible causes of Error is required",
      ],
      suggestions_model: null,
      suggestions_rules: [(v) => !!v || "Suggestions is required"],
      area_and_type_of_error_data: [
        {
          title: "Surgical Events",
          area_of_error: [
            "Surgery performed on the wrong body part.",
            "Surgery performed on the wrong patient.",
            "Wrong surgical procedure .",
            "Unintended retention of a foreign object in an enclosed body cavity in a patient after surgery/ procedure. ",
            "Return to surgery (repeat surgery).",
            "Admission to ICU post-operatively.",
            "Intra or post-operative death.",
            "Mechanical ventilation more than 24hours post-operation.",
            "Change in procedure.",
            "Normal pathology reports or unrelated to diagnosis.",
            "Occurrence of any operative (intra-op or post-op) complications.",
            "Patient Identification errors.",
          ],
        },
        {
          title: "Anesthetic Events",
          area_of_error: [
            "Airway injury or airway problems.",
            "Awareness under general anaesthesia.",
            "Aspiration",
            "Dental damage.",
            "Post-operative pain (24 hours after surgery).",
            "Mendelsohn’s syndrome.",
            "Equipment failure/ malfunction.",
            "Death",
            "Change in anesthetic use during surgery.",
            "Intra-operative epinephrine or norepinephrine administration.",
            "Intubation/ re-intubation post-operatively in PACU.",
            "Admission to ICU post-operatively.",
            "Mechanical ventilation more than 24hours post-operation.",
          ],
        },
        {
          title: "Product and device related events",
          area_of_error: [
            "Use of contaminated medications, medical devices or biologics provided by the hospital.",
            "Use of a medical device other functions than was intended or anticipated in the care of a patient provided by the healthcare provider.",
          ],
        },
        {
          title: "Patient protection events",
          area_of_error: [
            "Infant/ child or any other dependent person discharged to the wrong person.",
            "Absconding patient.",
            "Patient suicide/ attempted suicide while admitted in hospital.",
          ],
        },
        {
          title: "Patient Care management events",
          area_of_error: [
            "Patient Falls",
            "Decubitus ulcers.",
            "Readmission within 30 (thirty) days.",
            "In-hospital stroke/ Cardiovascular accident.",
            "Complications arising from bedside procedures.",
            "Use of restraints on patients.",
            "Missing essential information required on patient clinical/ request forms.",
            "Wrong formulation/ route administration of medication.",
            "Administration of incompatible blood or blood products. ",
            "Incorrect blood or blood products transfused.",
            "Patient identification errors.",
          ],
        },
        {
          title: "Environmental events",
          area_of_error: [
            "Electric shock while being cared for in the hospital but excluding events involving planned treatments such as cardioversion",
            "Contaminated oxygen/ other gases being delivered to a patient while in hospital.",
            "Burn injury incurred within the hospital.",
          ],
        },
        {
          title: "Radiologic events",
          area_of_error: [
            "Introduction of a metallic object into the MRI room.",
            "Missed fractures",
            "Missed diagnosis.",
            "Accidental irradiation exposure to pregnant patients.",
            "Errors in interpretation of radiological films.",
            "Errors in radiology reporting.",
            "Delayed imaging procedures.",
            "Delay in results.",
            "Delay in alerting clinician about emergency situations.",
            "Failure to suggest the next appropriate procedure.",
            "Failure to communicate in a timely and clinically appropriate manner.",
            "Patient identification errors.",
          ],
        },
        {
          title: "Obstetrics and Gynecology events",
          area_of_error: [
            "Maternal death ",
            "Patient identification errors.",
            "Use of mis-matched donor sperm or ovum or transfer of wrong zygote during IVF.",
            "Mix-up in babies.",
            "Missed diagnosis.",
            "Third- or fourth-degree tears.",
            "Birth asphyxia.",
            "Unattended birth/ delivery.",
            "Ruptured uterus.",
            "Post-partum hemorrhage.",
            "Birth trauma.",
          ],
        },
        {
          title: "Laboratory related events",
          area_of_error: [
            "Patient identification error.",
            "Specimen Labelling error.",
            "Error in specimen reporting.",
            "Error in collection of specimens.",
            "Equipment malfunction/ quality control issues.",
            "Mix- up of samples.",
            "Contamination of samples/ specimen.",
            "Failure to communicate in a timely and clinically appropriate manner.",
            "Use of wrong reagents.",
            "Failure to alert clinician on critical values.",
            "Delayed results.",
            "Errors in transport of blood and blood products/ components.",
            "Storing blood and blood products at ‘inadequate’ temperatures.",
            "Errors in tissue handling.",
            "Errors in interpretation by a pathologist.",
          ],
        },
        {
          title: "Criminal Events",
          area_of_error: [
            "Impersonating a doctor, nurse, pharmacist or other licensed healthcare provider.",
            "Abduction of patient of any age while being cared for in the hospital.",
            "Sexual assault on a patient or staff within or on hospital grounds.",
            "Physical assault on a patient/staff that occurs within or on the grounds of the hospital.",
          ],
        },
        {
          title: "Farewell Home Events",
          area_of_error: [
            "Body identification errors.",
            "Post mortem done on wrong bodies.",
            "Release of wrong body to wrong family.",
            "Unauthorized removal and retention of organs from bodies.",
            "Refrigerator/ equipment malfunction.",
            "Failure in communication between farewell home and other departments.",
            "Missing body.",
            "Inappropriate and unauthorized access to farewell home/ unsupervised collection of bodies.",
          ],
        },
        {
          title: "Accident and Emergency events",
          area_of_error: [
            "Revisit to A&E department within 48 hours.",
            "Missing patient",
            "Patient identification errors.",
          ],
        },
        {
          title: "Pediatric events",
          area_of_error: [
            "Patient identification errors.",
            "Breast milk administration errors.",
            "Mix-up in babies.",
            "Missed diagnosis.",
            "Delayed diagnosis.",
          ],
        },
        {
          title: "Medicine and critical care unit events",
          area_of_error: [
            "Missed diagnosis",
            "Delayed diagnosis",
            "Excess administration of intravenous narcotics.",
            "Readmission to ICU.",
            "Over sedation of patients.",
            "Failure to monitor ",
            "Patient identification errors.",
          ],
        },
        {
          title: "Pharmacy related events",
          area_of_error: [
            "Improper dose.",
            "Wrong time.",
            "Wrong patient.",
            "Administration of unauthorized drug",
            "Dispensing error.",
            "Prescribing errors.",
          ],
        },
        {
          title: "Health Information related events",
          area_of_error: [
            "Patient names not matching in HMIS.",
            "Missing file.",
          ],
        },
      ],
      area_of_error_data: ["Surgical Events", "Anesthetic Events"],
      outcome_of_error_data: [
        "No Error",
        "Error, No Harm",
        "Error, Harm",
        "Error, Death",
      ],
    };
  },
  methods: {
    validate() {
      this.$refs.form.validate();
    },
  },
  computed: {
    get_some_array: function () {
      let x = this.area_and_type_of_error_data;
      const newx = x.map((element) => element.title);
      return newx;
    },
    get_area_of_error: function () {
      let x = this.area_and_type_of_error_data;
      const newx = x.map((element) => element.title);
      return newx;
    },
    get_type_of_error: function () {
      let x = this.area_and_type_of_error_data;
      let filtered_arr = x.filter(
        (element) => element.title === this.area_of_error_model
      );
      filtered_arr[0];
      const new_filtered_arr = filtered_arr.map(
        (element) => element.area_of_error
      );

      return new_filtered_arr[0];
    },
    get_age_data: function () {
      let total = "";
      for (let i = 0; i < 150; i++) {
        total = total + i + ",";
      }
      let alll = total.split(",");

      return alll;
    },
  },
};
</script>
