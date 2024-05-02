<template>
  <div>
    <div v-for="(item, index) in users" :key="index" class="flex gap-4 my-4">
      <UInput
        color="primary"
        variant="outline"
        v-model="item.name"
        :placeholder="'Name ' + (index + 1)"
      ></UInput>
      <UInput
        v-model="item.amount"
        color="primary"
        variant="outline"
        placeholder="Amount"
        type="number"
      ></UInput>
    </div>
    <UButton @click="addItem"> Add User</UButton>

    <div class="border rounded mt-4 p-4">
      <div>summary block:</div>
      <div>total: {{ total }}</div>
      <div>average: {{ total / users.length }}</div>
      <div v-for="(item, index) in users" :key="index" class="flex gap-4 my-4">
        Name: {{ item.name }} Amount:{{ item.amount }}
      </div>
    </div>
  </div>
</template>

<script setup>
const users = ref([
  { name: "user1", amount: 10 },
  { name: "user 2", amount: 0 },
  { name: "user 3", amount: 0 },
]);

const addItem = () => {
  users.value.push({ name: "", amount: 0 });
};
const total = computed(() => {
  return users.value.reduce((accumulator, currentItem) => {
    return accumulator + Number(currentItem.amount);
  }, 0);
});
</script>

<style scoped>
</style>