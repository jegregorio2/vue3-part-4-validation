<template>
  <div id="employee-table">
    <table class="table table-striped">
      <thead>
        <tr>
          <th>Employee name</th>
          <th>Employee email</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="employee in employees" :key="employee.id">
          <td>{{ employee.name }}</td>
          <td>{{ employee.email }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  export default {
    name: 'EmployeeTable',
    props: {
      employees: Array,
    },
  }
</script>

<style scoped></style>