<template>
  <div class="h-screen">
    <div class="mx-80">
      <h1 class="text-xl mt-8 text-center">The Wisdom Book</h1>

      <div class="flex">
        <div @click="addWisdom" class="mt-8 button text-xl px-8">+</div>
      </div>

      <WisdomEntry
        v-for="item in items"
        :item="item"
        :key="item.id"
        @save="save"
        @remove="remove"
      />
    </div>
  </div>
</template>

<script>
function uuidv4() {
  return ([1e7] + -1e3 + -4e3 + -8e3 + -1e11).replace(/[018]/g, (c) =>
    (
      c ^
      (crypto.getRandomValues(new Uint8Array(1))[0] & (15 >> (c / 4)))
    ).toString(16)
  )
}

const defaultItem = {
  title: 'A new item',
  description: '- A \n- B \n- C',
}
export default {
  mounted() {
    try {
      this.items = JSON.parse(localStorage.getItem('items')) || [
        this.getNewItem(),
      ]
    } catch (e) {
      this.items = [this.getNewItem()]
    }
  },
  methods: {
    save() {
      localStorage.setItem('items', JSON.stringify(this.items))
    },
    remove(id) {
      if (!confirm('Are you sure?')) return
      this.items = this.items.filter((item) => item.id !== id)
      this.save()
    },
    addWisdom() {
      this.items.push(this.getNewItem())
    },
    getNewItem() {
      return {
        ...defaultItem,
        date: new Date().toISOString().slice(0, 10),
        id: uuidv4(),
      }
    },
  },
  data() {
    return {
      items: [],
    }
  },
}
</script>

<style>
.button {
  @apply border-2 rounded  text-gray-300 hover:text-yellow-300 hover:border-yellow-300 cursor-pointer;
}
</style>
