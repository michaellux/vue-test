<template>
    <div class="table-container" role="table" aria-label="Users">
      <Header v-if="isRoot" :headers="headers" />
      <UserItem v-for="user in filteredUsers" :user="user" :key="user.id" />
    </div>
</template>

<script>
import Header from '../components/views/table/Header';
import UserItem from './UserItem';

export default {
  components: { Header, UserItem },
  name: 'UserList',
  data() {
    return {
      headers:
      [{
        label: 'name',
        name: 'Имя',
      }, {
        label: 'phone',
        name: 'Телефон',
      },
      ],
    };
  },
  props: {
    id: {
      type: Number,
      default() {
        return null;
      },
    },
    isRoot: {
      type: Boolean,
      default() {
        return false;
      },
    },
    users: {
      type: Array,
      default() {
        return [];
      },
    },
  },
  computed: {
    filteredUsers() {
      const filteredUsers = this.users.filter(user => user.parent === this.id);
      return filteredUsers;
    },
  },
};
</script>

<style>
div {
  box-sizing: border-box;
}

.table-container {
  display: block;
  width: 90%;
  max-width: 1000px;
}

.flex-table {
  display: flex;
  flex-flow: row wrap;
  border-left: solid 1px #d9d9d9;
  transition: 0.5s;
}

.table-container .header .flex-row {
  background: #1976D2;
  color: white;
  border-color: #1565C0;
}

.flex-table.row:nth-child(odd) .flex-row {
  background: #f4f2f1;
}

.flex-table:hover {
  background: #F5F5F5;
  transition: 500ms;
}

.flex-row {
  width: calc(100% / 4);
  text-align: center;
  padding: 0.5em 0.5em;
  border-right: solid 1px #d9d9d9;
  border-bottom: solid 1px #d9d9d9;
}

.rowspan {
  display: flex;
  flex-flow: row wrap;
  align-items: flex-start;
  justify-content: center;
}

.column {
  display: flex;
  flex-flow: column wrap;
  width: 75%;
  padding: 0;
}

.column .flex-row {
  display: flex;
  flex-flow: row wrap;
  width: 100%;
  padding: 0;
  border: 0;
  border-bottom: solid 1px #d9d9d9;
}
.column .flex-row:hover {
  background: #F5F5F5;
  transition: 500ms;
}
.flex-cell {
  width: calc(100% / 3);
  text-align: center;
  padding: 0.5em 0.5em;
  border-right: solid 1px #d9d9d9;
}
@media (max-width: 767px) {
  .flex-row {
    width: calc(100% / 3);
  }
  .flex-row.first {
    width: 100%;
  }
  .column {
    width: 100%;
  }
}
@media (max-width: 430px) {
  .flex-table .flex-row {
    border-bottom: 0;
  }
  .flex-table .flex-row:last-of-type {
    border-bottom: solid 1px #d9d9d9;
  }
  .header .flex-row {
    border-bottom: solid 1px;
  }
  .flex-row {
    width: 100%;
  }
  .flex-row.first {
    width: 100%;
    border-bottom: solid 1px #d9d9d9;
  }
  .column {
    width: 100%;
  }
  .column .flex-row {
    border-bottom: solid 1px #d9d9d9;
  }
  .flex-cell {
    width: 100%;
  }
}
</style>
