<template>
  <v-container fluid>
    <v-card>
      <v-card-title class="d-flex align-center pe-2">
        <div class="titletext">{{ headerTitle }}</div>
        <v-spacer></v-spacer>
      </v-card-title>

      <div class="filter">
        <div class="filter-button-group">
          <v-btn
            v-for="option in options"
            :key="option.value"
            class="filter-button"
            :class="{ active: currentFilter === option.value }"
            @click="updateFilter(option.value)"
          >
            {{ option.label }}
          </v-btn>
        </div>
        <div class="search-container">
          <v-icon class="search-icon">mdi-magnify</v-icon>
          <input
            type="text"
            class="search-input"
            placeholder="검색어를 입력해주세요."
            v-model="stitle"
          />
        </div>
        <div class="button-group">
          <button
            class="search-button"
            @click="$emit('search', this.stitle, this.currentFilter)"
          >
            검색
          </button>
        </div>
      </div>

      <v-divider></v-divider>

      <table class="dashboard-table">
        <thead>
          <tr>
            <th v-for="column in columns" :key="column" class="theader">
              {{ column }}
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(row, rowIndex) in paginatedData" :key="rowIndex">
            <td
              v-for="(value, colIndex) in Object.values(row)"
              :key="colIndex"
              class="tdata"
            >
              <a
                v-if="colIndex === 1 && isModal"
                href="#"
                @click.prevent="openModal(value)"
              >
                {{ value }}
              </a>
              <a v-else-if="colIndex === 1"> {{ value }} </a>
              <span v-else>{{ value }}</span>
            </td>
          </tr>
        </tbody>
      </table>
    </v-card>

    <v-pagination
      v-model="currentPage"
      :length="pageCount"
      :total-visible="5"
      @input="searchList"
      class="pagination"
    ></v-pagination>

    <v-dialog v-model="dialog" max-width="600px">
      <v-card>
        <v-card-text>
          <component :is="modalComponent" v-bind="modalProps" />
        </v-card-text>
      </v-card>
    </v-dialog>
  </v-container>
</template>

<script>
export default {
  props: {
    headerTitle: {
      type: String,
      required: true,
    },
    columns: {
      type: Array,
      required: true,
    },
    data: {
      type: Array,
      required: true,
    },
    options: {
      type: Array,
      required: true,
      default: () => [],
    },
    value: {
      type: String,
      default: null,
    },
    modalComponentMap: {
      type: Object,
      required: true,
    },
    isModal: {
      type: Boolean,
      default: false,
    },
    searchMethod: {
      type: Function,
      required: true,
    },
  },
  data() {
    return {
      searchQuery: "",
      currentPage: 1,
      itemsPerPage: 10,
      dialog: false,
      modalComponent: null,
      modalProps: {},
      currentFilter: "all",
    };
  },
  computed: {
    filteredData() {
      if (!this.searchQuery) {
        return this.data;
      }
      return this.data.filter((row) =>
        Object.values(row).some((value) =>
          String(value).toLowerCase().includes(this.searchQuery.toLowerCase())
        )
      );
    },
    paginatedData() {
      const start = (this.currentPage - 1) * this.itemsPerPage;
      const end = start + this.itemsPerPage;
      return this.filteredData.slice(start, end);
    },
    pageCount() {
      return Math.ceil(this.filteredData.length / this.itemsPerPage);
    },
  },
  methods: {
    openModal(content) {
      this.modalComponent = this.modalComponentMap[content] || null;
      this.modalProps = { content };
      this.dialog = true;
    },
    closeModal() {
      this.dialog = false;
      this.modalComponent = null;
      this.modalProps = {};
    },
    updateFilter(filterValue) {
      this.currentFilter = filterValue;
      this.$emit("search", this.stitle, this.currentFilter);
    },
  },
};
</script>

<style>
table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 16px;
  background-color: #ffffff;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.05);
  border-radius: 8px;
}

thead {
  background-color: #f4f6f8;
}

.theader {
  padding: 12px;
  text-align: center;
  font-weight: bold;
  color: #2c3e50;
}

.tdata {
  padding: 12px;
  text-align: center;
  color: #34495e;
  border-bottom: 1px solid #e0e0e0;
}

tr:last-child .tdata {
  border-bottom: none;
}

tr:nth-child(even) .tdata {
  background-color: #f9f9f9;
}

.titletext {
  font-size: 22px;
  font-weight: 600;
}

.search-container {
  width: 280px;
  height: 50px;
  position: relative;
  display: flex;
  align-items: center;
  background-color: #f4f6f8;
  border-radius: 20px;
  padding: 5px 10px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  margin: 0;
  margin-left: auto;
}

.search-container:hover {
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  background-color: #e0e4e8;
}

.search-icon {
  color: #a0a0a0;
  margin-right: 8px;
}

.search-input {
  border: none;
  outline: none;
  background: none;
  padding: 8px;
  font-size: 14px;
  width: 200px;
  border-radius: 20px;
}

.search-input::placeholder {
  color: #a0a0a0;
}

.v-card {
  padding: 16px;
}

.v-divider {
  margin: 16px 0;
}

.pagination {
  margin-top: 20px;
  display: flex;
  justify-content: center;
}

.filter-button-group {
  display: flex;
  margin: 16px 0;
}

.filter {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}

.filter-button {
  background-color: #f4f6f8;
  color: #2c3e50;
  border-radius: 20px;
  padding: 8px 16px;
  margin: 0 4px;
  transition: background-color 0.3s, box-shadow 0.3s;
}

.filter-button.active {
  background-color: #407bff;
  color: #ffffff;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.filter-button:hover {
  background-color: #5a9bff;
}

.search-button {
  padding: 10px 16px;
  background-color: #407bff;
  color: #ffffff;
  border: none;
  border-radius: 4px;
  font-size: 14px;
  cursor: pointer;
  transition: background-color 0.3s, box-shadow 0.3s;
  margin-left: 15px;
}
.search-button:hover {
  background-color: #5a9bff;
  box-shadow: 0 4px 8px rgba(64, 123, 255, 0.2);
}
</style>
