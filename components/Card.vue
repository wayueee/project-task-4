<template>
  <div class="flex flex-col w-full">
    <div class="flex justify-center pb-3 pt-5">
      <div
        class="bg-white flex 2xl:flex-col p-4 rounded-lg shadow-md w-full max-w-2xl max-sm:mx-5"
      >
        <div
          class="flex items-start relative max-sm:relative max-sm:pb-10 max-sm:px-2"
        >
          <div
            class="bg-[#eaecf1] max-sm:absolute max-sm:bottom-0 max-sm:items-end flex 2xl:flex-col items-center rounded-lg mt-2 2xl:p-3 p-1 mr-4"
          >
            <button
              @click="$emit('upComent', data.id)"
              class="mb-3 max-sm:px-2 cursor-pointer"
            >
              <img src="/images/icon-plus.svg" alt="UpComent" />
            </button>
            <p class="text-lg font-semibold text-[#5457b6]">{{ data.votes }}</p>
            <button
              @click="$emit('downComent', data.id)"
              class="2xl:mt-3 max-sm:mb-3 max-sm:px-2 cursor-pointer"
            >
              <img src="/images/icon-minus.svg" alt="DownComent" />
            </button>
          </div>
          <div class="flex flex-col">
            <div class="flex flex-row ml-3">
              <img
                class="w-10 h-10 rounded-full mr-3"
                :src="data.avatar"
                alt="User Avatar"
              />
              <h4 class="font-semibold text-gray-800">
                {{ data.name }}
                <span
                  v-if="data.name == 'juliusomo'"
                  class="bg-[#5457b6] text-white px-1 pb-1 text-sm"
                  >you</span
                >
                <span class="text-gray-500 text-sm ml-2">{{ data.time }}</span>
              </h4>
            </div>
            <p class="text-gray-500 mt-2 max-sm:mb-3">{{ data.text }}</p>
          </div>

          <button
            class="text-blue-500 flex items-center px-2 mr-2 absolute cursor-pointer max-sm:absolute max-sm:bottom-1 right-0 max-sm:right-0"
            v-on:click="$emit('replyComent', data.id)"
          >
            <img
              class="w-4 h-4 mr-1"
              src="/images/icon-reply.svg"
              alt="Reply"
            />Reply
          </button>
        </div>
      </div>
    </div>

    <div v-if="data.showReply" class="flex mx-5 justify-center my-2">
      <div class="bg-white py-4 rounded-lg shadow-md w-full max-w-2xl">
        <div class="flex relative">
          <img
            class="w-10 h-10 rounded-full mx-3"
            src="/images/avatars/image-juliusomo.webp"
            alt=""
          />
          <textarea
            v-model="data.replyComent"
            type="text"
            placeholder="Reply Comment"
            class="border rounded-lg px-4 w-115 h-20 max-sm:w-56"
          ></textarea>
          <button
            class="bg-blue-500 text-white mx-5 px-4 py-2 rounded absolute right-1 max-sm:right-0 "
            @click="$emit('comentReply', data, data.id)"
          >
            Reply
          </button>
        </div>
      </div>
    </div>

    <div v-if="data.replies.length" class="flex justify-center mb-5">
      <div
        class="w-full max-w-2xl px-10 ml-20 max-sm:ml-4 max-sm:pl-5 border-l-3 border-[#8f8fb433]"
      >
        <Comments
          v-for="(item, idx) in data.replies"
          :key="idx"
          :replyes="item"
          @comentReplyChild="$emit('comentReplyChild', item.id, data.id)"
          @replyComentChild="$emit('replyComentChild', item.id, data.id)"
          @upComentChild="$emit('upComentChild', item.id, data.id)"
          @downComentChild="$emit('downComentChild', item.id, data.id)"
          @deleteComent="$emit('deleteComent', item.id, data.id)"
          @editText="$emit('editText', item.id, data.id)"
          @updateText="$emit('updateText', item.id, data.id)"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    data: {
      type: Object,
      default: () => {},
    },
  },
};
</script>

<style></style>
