<template>
  <div>
    <h2>Quản lý mượn trả sách</h2>
    <div class="controls">
      <select v-model="statusFilter">
        <option value="all">Tất cả</option>
        <option value="true">Đã trả</option>
        <option value="false">Chưa trả</option>
      </select>
      <button class="add-btn" @click="openForm()">Thêm thông tin</button>
    </div>

    <table class="book-table">
      <thead>
        <tr>
          <th>STT</th>
          <th>Tên sách</th>
          <th>Sinh viên mượn</th>
          <th>Ngày mượn</th>
          <th>Ngày trả</th>
          <th>Trạng thái</th>
          <th>Chức năng</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(book, index) in filteredBooks" :key="index">
          <td>{{ index + 1 }}</td>
          <td>{{ book.name }}</td>
          <td>{{ book.borrower }}</td>
          <td>{{ book.borrowDate }}</td>
          <td>{{ book.returnDate }}</td>
          <td>
            <select
              v-model="book.status"
              @change="updateStatus(index)"
              :class="book.status ? 'true' : 'false'"
            >
              <option :value="true">Đã trả</option>
              <option :value="false">Chưa trả</option>
            </select>
          </td>
          <td>
            <button class="edit-btn" @click="openForm(index)">Sửa</button>
            <button class="delete-btn" @click="deleteBook(index)">Xóa</button>
          </td>
        </tr>
      </tbody>
    </table>

    <div v-if="showForm" class="form-modal">
      <div class="form-content">
        <h3>{{ editIndex === null ? "Thêm" : "Sửa" }} thông tin mượn sách</h3>

        <input v-model="newBook.name" placeholder="Tên sách" />
        <span v-if="errors.name" class="error">{{ errors.name }}</span>

        <input v-model="newBook.borrower" placeholder="Tên người mượn" />
        <span v-if="errors.borrower" class="error">{{ errors.borrower }}</span>

        <input
          v-model="newBook.borrowDate"
          type="date"
          placeholder="Ngày mượn"
        />
        <span v-if="errors.borrowDate" class="error">{{
          errors.borrowDate
        }}</span>

        <input
          v-model="newBook.returnDate"
          type="date"
          placeholder="Ngày trả"
        />
        <span v-if="errors.returnDate" class="error">{{
          errors.returnDate
        }}</span>
        <br />

        <button @click="saveBook" class="add-btn">
          {{ editIndex === null ? "Thêm" : "Lưu" }}
        </button>
        <button @click="closeForm" class="close-btn">Đóng</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from "vue";

const books = ref([]);
const showForm = ref(false);
const statusFilter = ref("all");
const editIndex = ref(null);

const newBook = ref({
  name: "",
  borrower: "",
  borrowDate: "",
  returnDate: "",
  status: false,
});

const errors = ref({
  name: "",
  borrower: "",
  borrowDate: "",
  returnDate: "",
});

onMounted(() => {
  const storedBooks = JSON.parse(localStorage.getItem("books")) || [];
  books.value = storedBooks.map((book) => ({
    ...book,
    status: Boolean(book.status),
  }));
});

const filteredBooks = computed(() => {
  if (statusFilter.value === "all") return books.value;
  return books.value.filter(
    (book) => String(book.status) === statusFilter.value
  );
});

const validateForm = () => {
  errors.value = {};
  if (!newBook.value.name) errors.value.name = "Tên sách không được để trống";
  if (!newBook.value.borrower)
    errors.value.borrower = "Tên người mượn không được để trống";
  if (!newBook.value.borrowDate)
    errors.value.borrowDate = "Ngày mượn không được để trống";
  if (!newBook.value.returnDate)
    errors.value.returnDate = "Ngày trả không được để trống";
  return Object.keys(errors.value).length === 0;
};

const openForm = (index = null) => {
  if (index !== null) {
    editIndex.value = index;
    newBook.value = { ...books.value[index] };
  } else {
    editIndex.value = null;
    newBook.value = {
      name: "",
      borrower: "",
      borrowDate: "",
      returnDate: "",
      status: false,
    };
  }
  showForm.value = true;
};

const closeForm = () => {
  showForm.value = false;
  editIndex.value = null;
};

const saveBook = () => {
  if (!validateForm()) return;

  if (editIndex.value === null) {
    books.value.push({
      ...newBook.value,
      status: Boolean(newBook.value.status),
    });
  } else {
    books.value[editIndex.value] = {
      ...newBook.value,
      status: Boolean(newBook.value.status),
    };
  }

  localStorage.setItem("books", JSON.stringify(books.value));
  closeForm();
};

const updateStatus = (index) => {
  books.value[index].status = !books.value[index].status;
  localStorage.setItem("books", JSON.stringify(books.value));
};

const deleteBook = (index) => {
  if (confirm("Bạn có chắc chắn muốn xóa cuốn sách này?")) {
    books.value.splice(index, 1);
    localStorage.setItem("books", JSON.stringify(books.value));
  }
};
</script>

<style scoped>
.book-table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}
.book-table,
th,
td {
  border: 1px solid #ddd;
}
th,
td {
  padding: 12px;
  text-align: left;
}
th {
  background-color: #f4f4f4;
}

.add-btn,
.edit-btn,
.delete-btn,
.close-btn {
  padding: 8px 12px;
  margin: 5px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.add-btn {
  background-color: #007bff;
  color: white;
}

.edit-btn {
  background-color: #ffc107;
  color: white;
}

.delete-btn {
  background-color: #dc3545;
  color: white;
}

.close-btn {
  background-color: #6c757d;
  color: white;
}

/* Style cho form */
.form-modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}
.form-content {
  background: white;
  padding: 20px;
  border-radius: 8px;
  text-align: center;
  width: 400px;
}
input,
select {
  width: 80%;
  padding: 10px;
  margin: 10px 0;
  border: 1px solid #ccc;
  border-radius: 5px;
}
.error {
  color: red;
  font-size: 14px;
  margin-top: -10px;
  margin-bottom: 10px;
  display: block;
}
.false {
  background-color: red;
  color: white;
}
.true {
  background-color: green;
  color: white;
}
</style>
