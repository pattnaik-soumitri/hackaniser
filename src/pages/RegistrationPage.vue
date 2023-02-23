<template>
  <div class="q-pa-md" style="max-width: 500px">

    <h6>Register</h6>

    <q-form
      @submit="onSubmit"
      @reset="onReset"
      class="q-gutter-md"
    >
      <q-input
        outlined
        v-model="entry.email"
        label="Your email *"
        type="email"
        lazy-rules
        :rules="[
          val => val !== null && val !== '' || 'Please type your email',
          val => validateEmail(val) || 'Please type a valid email'
        ]"
      />

      <q-input
        outlined
        v-model="entry.firstName"
        label="Your first name *"
        lazy-rules
        :rules="[
          val => val !== null && val !== '' || 'Please type your first name',
        ]"
      />

      <q-input
        outlined
        v-model="entry.lastName"
        label="Your last name *"
        lazy-rules
        :rules="[
          val => val !== null && val !== '' || 'Please type your last name',
        ]"
      />

      <div class="q-pa-sm rounded-borders">
        <span style="font-weight: 500;">What business unit do you work in? *</span>
        <q-option-group
          :options="businessUnitOptions"
          type="radio"
          v-model="entry.businessUnit"
          aria-required="true"
        />
      </div>

      <div class="q-pa-sm rounded-borders">
        <span style="font-weight: 500;">Do you plan to participate as a hackathon team member? *</span>
        <q-option-group
          :options="[{label: 'Yes', value: 'yes'}, {label: 'No', value: 'no'}, {label: 'MayBe', value: 'maybe'}]"
          type="radio"
          v-model="entry.doPlanToParticipate"
        />
      </div>

      <q-input
        outlined
        v-model="entry.problemStatement"
        label="What problem does your idea solve? *"
        type="textarea"
        lazy-rules
        :rules="[
          val => val !== null && val !== '' || 'Please type your answer',
        ]"
      />

      <q-input
        outlined
        v-model="entry.solutionDescription"
        label="Please describe how your idea would solve the problem and why it is novel (new and original). *"
        type="textarea"
        lazy-rules
        :rules="[
          val => val !== null && val !== '' || 'Please type your answer',
        ]"
      />

      <div class="q-pa-sm rounded-borders">
        <span style="font-weight: 500;">Is this a new product or a change to an existing product? *</span>
        <q-option-group
          :options="[{label: 'New Product', value: true}, {label: 'Existing Product', value: false}]"
          type="radio"
          v-model="entry.isNewProduct"
        />
      </div>

      <div class="q-pa-sm rounded-borders">
        <span style="font-weight: 500;">Has this idea been shared with any entity outside of JCI that has not signed an NDA? *</span>
        <q-option-group
          :options="[{label: 'Yes', value: true}, {label: 'No', value: false}]"
          type="radio"
          v-model="entry.isSharedOutsideOrg"
        />
      </div>

      <div class="q-pa-sm rounded-borders">
        <span style="font-weight: 500;">Have you or anyone else started created a prototype? *</span>
        <q-option-group
          :options="[{label: 'Yes', value: true}, {label: 'No', value: false}]"
          type="radio"
          v-model="entry.isPrototypeStarted"
        />
      </div>


      <div>
        <q-btn label="Submit" type="submit" color="primary"/>
        <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
      </div>
    </q-form>

  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useQuasar } from 'quasar';
const $q = useQuasar();

const emptyEntry = {
  email: null,
  firstName: null,
  lastName: null,
  businessUnit: 'Traffic',
  doPlanToParticipate: 'yes',
  problemStatement: null,
  solutionDescription: null,
  isNewProduct: true,
  isSharedOutsideOrg: false,
  isPrototypeStarted: false,
  helpOrg: []
}

const businessUnitOptions = [
  { label: 'Traffic/Shopper Engagement', value: 'Traffic' },
  { label: 'Inventory', value: 'Inventory' },
  { label: 'Loss Prevention', value: 'LP' }
]

/* REFS */
const entry = ref(emptyEntry);

/* METHODS */
const onSubmit =  () => {
  console.log(entry.value);
  $q.notify({
    color: 'green-4',
    textColor: 'white',
    icon: 'cloud_done',
    message: 'Submitted'
  });
}

const onReset = () => {
  entry.value = {...emptyEntry};
}

const validateEmail = (email) => {
  return /[a-z0-9]+@[a-z]+\.[a-z]{2,3}/.test(email);
}
</script>
