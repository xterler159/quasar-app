<template>
  <div style="margin-bottom: 14px; margin-top: 14px">
    <q-table
      :columns="columns"
      :rows="users ? users : []"
      title="Users"
      v-model:selected="selected"
      @update:selected="handleSelection"
      selection="multiple"
    />
  </div>
</template>

<script>
import { defineComponent, ref, onMounted } from "vue";
import { api } from "src/boot/axios";

export default defineComponent({
  name: "UsersPage",
  setup() {
    const users = ref(null);
    const selected = ref([]);

    const handleSelection = (selectedRows) => {
      if (selectedRows.length > 0) {
        selectedRows.forEach((row) => {
          console.log("selected row:", row);
        });
      }
    };

    const fetchUsers = async () => {
      const req = await api.get("/users?_limit=5");

      if (req.status === 200) {
        users.value = req.data;
      }
    };

    const columns = [
      {
        name: "name",
        field: "name",
        label: "Name".toUpperCase(),
        sortable: true,
        align: "left",
      },
      {
        name: "username",
        field: "username",
        label: "Username".toUpperCase(),
        sortable: true,
        align: "left",
      },
      {
        name: "email",
        field: "email",
        label: "Email".toUpperCase(),
        sortable: true,
        align: "left",
      },
      {
        name: "address",
        field: (row) => {
          return `${row.address.street}, ${row.address.suite}, ${row.address.city}, ${row.address.zipcode}`;
        },
        label: "Address".toUpperCase(),
        align: "left",
      },
    ];

    onMounted(() => {
      fetchUsers();
    });

    return {
      users,
      fetchUsers,
      columns,
      selected,
      handleSelection,
    };
  },
});
</script>
