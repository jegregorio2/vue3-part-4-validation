<template>
  <div id="employee-form">
    <form @submit.prevent="handleSubmit">
      <div class="mb-3">
        <label for="exampleInputName1" class="form-label">Employee name</label>
        <!-- add :class, @focus, @keypress -->
        <input 
          ref="first"
          v-model="employee.name"
          type="text"
          class="form-control"
          id="exampleInputName1"
          aria-describedby="nameHelp"
          :class="{ 'has-error': submitting && invalidName }"
          @focus="clearStatus"
          @keypress="clearStatus"
        />
      </div>
      <div class="mb-3">
        <label for="exampleInputEmail1" class="form-label">Employee email</label>
        <!-- add :class, @focus -->
        <input 
          v-model="employee.email"
          type="email"
          class="form-control"
          id="exampleInputEmail1"
          aria-describedby="emailHelp"
          :class="{ 'has-error': submitting && invalidEmail }"
          @focus="clearStatus"
        />
        <!-- add if, error message -->
        <p v-if="error && submitting" class="error-message">
          ❗Please fill out all required fields
        </p>
        <!-- add if, success message -->
        <p v-if="success" class="success-message">
          ✅ Employee successfully added
        </p>
      </div>
      <button
        class="btn btn-primary"
        type="submit">Add Employee
      </button>
    </form>
  </div>
</template>

<script>
  export default {
    name: 'EmployeeForm',
    data() {
      return {
        // add submitting, error, success
        submitting: false,
        error: false,
        success: false,
        employee: {
          name: '',
          email: '',
        },
      }
    },
    // add computed
    computed: {
      // add invalidName()
      invalidName() {
        return this.employee.name === ''
      },
      // add invalidEmail()
      invalidEmail() {
        return this.employee.email === ''
      },
    },
    methods: {
      handleSubmit() {
        console.log('testing handleSubmit')
        // when you click 'Add Employee' button, you will see 'testing handleSubmit' in console
        
        this.submitting = true
        this.clearStatus()

        if (this.invalidName || this.invalidEmail) {
          this.error = true
          return
        }

        this.$emit('add:employee', this.employee)
        // when you click 'Add Employee' button, you will see 'add:employee' through vue > events
        
        this.$refs.first.focus()
        this.employee = {
          name: '',
          email: '',
        }
        // add submitting, error, success
        this.error = false
        this.success = true
        this.submitting = false
      },
      // add clearStatus()
      clearStatus() {
        // add error, success
        this.success = false
        this.error = false
      },
    },
  }
</script>

<style scoped>
  form {
    margin-bottom: 2rem;
  }

  [class*='-message'] {
    font-weight: 500;
  }

  .error-message {
    color: #d33c40;
  }

  .success-message {
    color: #32a95d;
  }
</style>