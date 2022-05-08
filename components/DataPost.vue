<template>
  <div>
    <div class="mx-2 my-2">
      imageUrl:
      <input
        v-model="imageUrl"
        class="mx-2 my-2 shadow-sm rounded border focus:outline-none focus:ring-2 focus:border-sky-700"
        type="text"
      />
    </div>
    <div class="mx-2 my-2">
      Title:
      <input
        v-model="title"
        class="mx-2 my-2 shadow-sm rounded border focus:outline-none focus:ring-2 focus:border-sky-700"
        type="text"
      />
    </div>
    <div class="mx-2 my-2">
      Price:
      <input
        v-model="price"
        class="mx-2 my-2 shadow-sm rounded border focus:outline-none focus:ring-2 focus:border-sky-700"
        type="text"
      />
    </div>
    <div class="mx-2 my-2">
      Category:
      <input
        v-model="category"
        class="mx-2 my-2 shadow-sm rounded border focus:outline-none focus:ring-2 focus:border-sky-700"
        type="text"
      />
    </div>
    <div class="mx-6 my-6">
      <a
        href=""
        class="px-10 py-2 shadow-sm rounded border bg-blue-200 hover:bg-opacity-70 focus:ring-violet-300 active:bg-blue-400"
        @click="createData()"
      >
        送出
      </a>
    </div>
    <div>
      <!-- <div class="my-2">
        <select v-model="update" class="mb-6" value="請選擇更改欄位">
          <option value="" selected disabled>請選擇更改欄位</option>
          <option v-for="name in dataName" :key="name" :value="name">
            更改 {{ name }}
          </option>
        </select>
      </div>
      <div>
        <input v-model="update" type="text" />
      </div> -->
    </div>
    <div>
      <li v-for="content in filtData" :key="content.id" class="mx-4 my-8">
        {{ content.id }}

        <!-- <a
          href=""
          class="px-2 py-2 shadow-sm rounded border-2 bg-blue-300 hover:bg-opacity-80 focus:ring-violet-300 active:bg-blue-400"
          @click="updateData(content.id)"
          >更新</a
        > -->
        <a
          href=""
          class="px-2 py-2 shadow-sm rounded border-2 bg-blue-300 hover:bg-opacity-80 focus:ring-violet-300 active:bg-blue-400"
          @click="deleteData(content.id)"
          >刪除</a
        >
      </li>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      filtData: [],
      dataName: ['imageUrl', 'title', 'price', 'category'],
      imageUrl: '',
      title: '',
      price: '',
      category: '',
      update: '',
    }
  },
  methods: {
    createData() {
      axios
        .post('http://localhost:2000/filtData', {
          imageUrl: this.imageUrl,
          title: this.title,
          price: this.price,
          category: this.category,
        })
        .then((res) => {
          // this.imageUrl = ''
          // this.title = ''
          // this.price = ''
          // this.category = ''
          // this.filtData.push(res.data)
        })
    },
    deleteData(id) {
      axios.delete(`http://localhost:2000/filtData/${id}`).then((res) => {
        console.log(res)
      })
    },
  },
  // updateData(id) {
  //   axios.post(`http://localhost:2000/filtData/${id}`, {
  //     category: this.update,
  //     _method: 'patch',
  //   })
  // },
  mounted() {
    axios.get('http://localhost:2000/filtData').then((res) => {
      this.filtData = res.data
    })
  },
}
</script>
