<template>
  <div class="container">
    <input type="text" v-model="form.text" @blur="" />
    <button @click="Add">新增</button>

    <ul>
      <li v-for="item in listData" :key="item.id">
        {{ item.text }}
        <button>編輯</button>

        <button @click="Delete(item.id)">刪除</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { nanoid } from "nanoid";
import { ref } from "vue";
import { z } from "zod";
const form = ref({
  text: "",
});

const resetForm = () => {
  form.value = {
    text: "",
  };
};

const listData = ref([]);

// 新增
const Add = () => {
  console.log("正在新增", form);
  const text = form.value.text.trim(); // trim處理空白
  console.log("11", text);
  nanoid();
  listData.value.push({
    id: nanoid(),
    text: text,
  });

  resetForm();

  console.log("目前代辦事項", listData.value);
};

//  刪除

const Delete = (id) => {
  console.log("正在刪除");

  const findIndex = listData.value.findIndex((item) => {
    return item.id === id;
  });
  console.log(findIndex);

  const DeleteResult = listData.value.splice(findIndex, 1);

  console.log(DeleteResult);
};

const schema = z.object({
  name: z.string().min(2, "名字太短"),
});

const result = schema.safeParse({ name: "11111111111" });

if (!result.success) {
  console.log(result.error.errors[0].message); // => 名字太短
}
</script>
