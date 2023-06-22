<template>
  <h1 class="text-h3">Users</h1>
  <!-- <code>{{ JSON.stringify(users) }}</code> -->

  <q-table :columns="columns" :rows="users ? users : []"></q-table>
</template>

<script>
import { defineComponent, ref } from "vue";
import { api } from "src/boot/axios";

export default defineComponent({
  name: "UsersPage",
  setup() {
    const users = ref(null);

    const fetchUsers = async () => {
      const req = await api.get("/users");

      if (req.status === 200) {
        users.value = req.data;
      }
    };

    const columns = [
      {
        name: "desc",
        label: "Dessert (100g serving)",
        field: "name",
        required: true,
        align: "left",
        sortable: true,
        sort: (a, b, rowA, rowB) => parseInt(a, 10) - parseInt(b, 10),
        sortOrder: "ad", // or 'da'
        format: (val, row) => `${val}%`,
        style: "width: 500px",
        classes: "my-special-class",
        headerStyle: "width: 500px",
        headerClasses: "my-special-class",
      },
      {
        name: "calories",
        label: "Calories",
        field: "calories",
        sortable: true,
      },
      { name: "name", label: "Name", field: "fat", sortable: true },
      { name: "carbs", label: "Carbs (g)", field: "carbs" },
      { name: "protein", label: "Protein (g)", field: "protein" },
      { name: "sodium", label: "Sodium (mg)", field: "sodium" },
      {
        name: "calcium",
        label: "Calcium (%)",
        field: "calcium",
        sortable: true,
        sort: (a, b) => parseInt(a, 10) - parseInt(b, 10),
      },
      {
        name: "iron",
        label: "Iron (%)",
        field: "iron",
        sortable: true,
        sort: (a, b) => parseInt(a, 10) - parseInt(b, 10),
      },
    ];

    return {
      users,
      fetchUsers,
      columns,
    };
  },
  mounted() {
    this.fetchUsers();
  },
});
</script>
