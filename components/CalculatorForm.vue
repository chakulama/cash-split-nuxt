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
        @input="calculateOwes"
      ></UInput>
    </div>
    <UButton @click="addItem"> Add User</UButton>

    <div class="border rounded mt-4 p-4">
      <div>summary block:</div>
      <div>total: {{ totalAmount }}</div>
      <div>average: {{ averageAmount }}</div>
    </div>
    <div v-for="(owe, index) in owes" :key="index">
      {{ owe[1] }} --> {{ owe[0] }} ---> {{ owe[2] }}
    </div>
  </div>
</template>

<script setup>
const users = ref([
  { name: "user1", amount: 30 },
  { name: "user2", amount: 30 },
  { name: "user3", amount: 0 },
]);
const owes = ref([]);

const addItem = () => {
  users.value.push({ name: "", amount: 0 });
};
const totalAmount = computed(() => {
  return users.value.reduce((accumulator, currentItem) => {
    return accumulator + Number(currentItem.amount);
  }, 0);
});
const averageAmount = computed(() => {
  return totalAmount.value / users.value.length;
});

const calculateOwes = () => {
  owes.value = [];
  users.value.forEach((user) => {
    user.balance = user.amount - averageAmount.value;
  });
  users.value.sort((a, b) => b.balance - a.balance);
  let i = 0;
  let j = users.value.length - 1;
  while (i < j) {
    const min = Math.min(users.value[i].balance, -users.value[j].balance);
    if (min !== 0) {
      owes.value.push([
        users.value[i].name,
        users.value[j].name,
        `$${Math.abs(min)}`,
      ]);
      users.value[i].balance -= min;
      users.value[j].balance += min;
    }
    if (users.value[i].balance === 0) i++;
    if (users.value[j].balance === 0) j--;
  }
};

watchEffect(() => {
  users.value.forEach((user) => user.amount);
  calculateOwes();
});
</script>

<style scoped>
</style>