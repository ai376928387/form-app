<template>
  <div class="container my-3 mx-auto p-3 bg-gray-300">
    <p class="text-xl text-bold">Form Validation</p>
    <div class="mb-2">
      <label class="block">Email *</label>
      <input
      v-model="formValue.email"
      v-validate="'required|email'"
      type="email"
      maxlength="64"
      class="h-10 bg-gray-100 border p-2"
      name="email" />
      <span class="text-red-600">{{ errors.first('email') }}</span>
    </div>
    <div class="mb-2">
      <label class="block">Password *</label>
      <input
      v-model="formValue.password"
      v-validate="passwordRule"
      type="password"
      maxlength="64"
      class="h-10 bg-gray-100 border p-2"
      name="password" />
      <span class="text-red-600">{{ errors.first('password') }}</span>
    </div>
    <div class="mb-2">
      <label class="block">Please select a color *</label>
      <select
        v-model="formValue.color"
        v-validate="'required'"
        name="color"
        class="h-10 bg-gray-100 border p-2"
      >
        <option v-for="color in colorOptions" :key="color" :value="color"
         class="h-10 bg-gray-100 border p-2">{{color}}</option>
      </select>
      <span class="text-red-600">{{ errors.first('color') }}</span>
    </div>
    <div class="mb-2">
      <label class="block">Please select a animal *</label>
      <select
        v-model="formValue.animal"
        v-validate="'required'"
        name="animal"
        class="bg-gray-100 border p-2"
        multiple
      >
        <option v-for="animal in animalOptions" :key="animal" :value="animal"
         class="h-10 bg-gray-100 border p-2">{{animal}}</option>
      </select>
      <span class="text-red-600">{{ errors.first('animal') }}</span>
    </div>
    <div v-if="formValue.animal.includes('Tiger')" class="mb-2">
      <label class="block">Type of Tiger</label>
      <input
      v-model="formValue.typeOfTiger"
      v-validate="'required'"
      type="text"
      maxlength="64"
      class="h-10 bg-gray-100 border p-2"
      name="typeOfTiger"
      data-vv-as="type of tiger"
      />
      <span class="text-red-600">{{ errors.first('typeOfTiger') }}</span>
    </div>
    <div class="mb-2">
      <button class="bg-green-300 leading-none text-center font-bold border h-12 py-4 px-8 hover:cursor-pointer" @click="validate()">validate form</button>
    </div>
    <p v-if="isValidationPass" class="text-green-900">Validation Pass</p>
  </div>
</template>
<script>
export default {
  data () {
    return {
      formValue: {
        email: null,
        password: null,
        color: null,
        animal: [],
        typeOfTiger: null
      },
      isValidationPass: false,
      colorOptions: [
        'Blue', 'Green', 'Red', 'Black', 'Brown'
      ],
      animalOptions: [
        'Bear', 'Tiger', 'Snake', 'Donkey'
      ]
    }
  },
  computed: {
    passwordRule() {
      return 'required|min:8'
    }
  },
  methods: {
    async validate() {
      this.isValidationPass =await this.$validator.validateAll()
    }
  }
}
</script>