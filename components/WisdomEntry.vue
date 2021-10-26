<template>
  <div class="border-2 p-6 my-2 rounded shadow-md">
    <div class="flex items-end">
      <input
        type="text"
        placeholder="Title"
        class="text-2xl flex-grow text-yellow-500 border-none p-1 m-1"
        v-model="item.title"
        @input="$emit('save')"
      />
      <h2 class="text-gray-300">{{ item.date }}</h2>
      <div class="ml-4 cursor-pointer" @click="$emit('remove', item.id)">🗑</div>
    </div>
    <textarea
      type="text"
      placeholder="Description"
      class="p-1 m-1 border-none w-full h-20"
      v-model="item.description"
      @input="$emit('save')"
    />

    <!-- <span
      class="textarea"
      role="textbox"
      contenteditable
      @input="$emit('save')"
      >{{ item.description }}</span
    > -->
  </div>
</template>

<script>
export default {
  props: ['item'],
  data() {
    return {}
  },
}
</script>

<style>
.input,
.textarea {
  border: 1px solid #ccc;
  font-family: inherit;
  font-size: inherit;
  padding: 1px 6px;
}

.textarea {
  display: block;
  width: 100%;
  overflow: hidden;
  resize: both;
  min-height: 40px;
  line-height: 20px;
}

.textarea[contenteditable]:empty::before {
  content: 'Placeholder still possible';
  color: gray;
}
</style>
