<template>
  <div class="container">
    <input type="text" v-model="form" @blur="" />
    <button @click="Add">新增</button>

    <ul>
      <li v-for="item in listData" :key="item.key">
        {{ item }}
        <button>編輯</button>

        <button @click="Delete">刪除</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { z } from "zod";
const form = ref("");

const listData = ref([]);

// 新增
const Add = () => {
  console.log("正在新增", form);

  listData.value.push(form.value);

  console.log("目前代辦事項", listData.value);
};

//  刪除

// const Delete = ()=>{
//   console.log("正在刪除");

//   const findIndex =

// }

const schema = z.object({
  name: z.string().min(2, "名字太短"),
});

const result = schema.safeParse({ name: "11111111111" });

if (!result.success) {
  console.log(result.error.errors[0].message); // => 名字太短
}
</script>

