<template>
  <div style="margin-bottom: 14px; margin-top: 14px">
    <q-table
      v-if="!isDataLoading"
      bordered
      :columns="columns"
      :rows="users"
      title="Users"
      v-model:selected="selected"
      @update:selected="handleSelection"
      selection="multiple"
      :pagination="pagination"
    />
    <q-spinner size="3em" v-if="isDataLoading" />
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
    const isDataLoading = ref(true);

    const pagination = ref({
      page: 1,
      sortBy: "desc",
      descending: false,
      page: 1,
      rowsPerPage: 5,
      // rowsNumber: 10, // this means we are managing pagination from the server
    });

    const handleSelection = (selectedRows) => {
      if (selectedRows.length > 0) {
        selectedRows.forEach((row) => {
          console.log("selected row:", row);
        });
      }
    };

    const fetchUsers = async () => {
      const req = await api.get("/users?_limit=10");

      if (req.status === 200) {
        users.value = req.data;
        isDataLoading.value = false;
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
      pagination,
      isDataLoading,
    };
  },
});
</script>
