<template>
  <div class="flex flex-col w-full">
    <div class="flex justify-center pb-3">
      <div
        class="bg-white flex flex-col p-4 pt-5 rounded-lg w-full 2xl:mt-4 max-w-2xl"
      >
        <div class="flex items-start max-sm:relative max-sm:pb-10 max-sm:px-2">
          <div
            class="bg-[#eaecf1] max-sm:absolute max-sm:bottom-0 max-sm:items-end flex 2xl:flex-col items-center rounded-lg mt-2 2xl:p-3 p-1 mr-4"
          >
            <button
              @click="$emit('upComentChild')"
              class="mb-3 max-sm:px-2 cursor-pointer"
            >
              <img src="/images/icon-plus.svg" alt="UpComent" />
            </button>
            <p class="text-lg font-semibold text-[#5457b6]">
              {{ replyes.votes }}
            </p>
            <button
              @click="$emit('downComentChild')"
              class="mt-3 max-sm:mb-3 max-sm:px-2 cursor-pointer"
            >
              <img src="/images/icon-minus.svg" alt="DownComent" />
            </button>
          </div>
          <div class="flex flex-col">
            <div class="flex flex-row">
              <img
                class="w-10 h-10 rounded-full mr-3"
                :src="replyes.avatar"
                alt="User Avatar"
              />
              <h4 class="font-semibold text-gray-800">
                {{ replyes.name }}
                <span
                  v-if="replyes.name == 'juliusomo'"
                  class="bg-[#5457b6] text-white px-1 pb-1 text-sm"
                  >you</span
                >
                <span class="text-gray-500 text-sm ml-2">{{
                  replyes.time
                }}</span>
              </h4>
            </div>
            <div class="flex mt-2 ">
              <textarea v-if="replyes.showEdit" v-model="replyes.text" class="w-120 h-35 border rounded-lg mb-8 p-2 max-sm:w-70"></textarea>
              <p v-if="!replyes.showEdit" class="font-semibold text-[#5457b6]"
                >@{{ replyes.repliedUsername }}
              <span class="text-gray-500 max-sm:mb-3 ">{{ replyes.text }}</span>
              </p>
            </div>
          </div>
          <button
            v-if="replyes.disableReply"
            class="text-blue-500 flex items-center px-2 mr-2 cursor-pointer max-sm:absolute max-sm:bottom-1 max-sm:right-0"
            v-on:click="$emit('replyComentChild')"
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

    <div v-if="replyes.showReply" class="flex justify-center mt-2 relative">
      <div class="bg-white rounded-lg shadow-md w-full max-w-2xl">
        <div v-if="replyes.disableReply" class="flex my-5">
          <img
            class="w-10 h-10 rounded-full mx-3"
            src="/images/avatars/image-juliusomo.webp"
            alt=""
          />
          <textarea
            v-model="replyes.replyComent"
            type="text"
            placeholder="Reply Comment"
            class="border rounded-lg px-4 w-104 h-20 max-sm:w-48"
          ></textarea>
          <button
            @click="$emit('comentReplyChild')"
            class="bg-blue-500 text-white mx-5 px-4 py-2 rounded absolute right-0"
          >
            Reply
          </button>
        </div>

        <div v-if="replyes.myUserShowReply">
          <button
            v-if="!replyes.showEdit"
            v-on:click="replyes.showModalDel = true"
            class="text-[#ed6468] font-semibold absolute right-20 bottom-32 max-sm:bottom-10 flex cursor-pointer"
          >
            <img
              class="w-3 h-4 mt-1 mr-1"
              src="/images/icon-delete.svg"
              alt=""
            />Delete
          </button>
          <button
            v-if="!replyes.showEdit"
            v-on:click="$emit('editText')"
            class="text-[#5457b6] font-semibold absolute right-4 bottom-32 max-sm:bottom-10 flex cursor-pointer"
          >
            <img
              class="w-3 h-4 mt-1 mr-1"
              src="/images/icon-edit.svg"
              alt=""
            />Edit
          </button>
          <button
            v-if="replyes.showEdit"
            v-on:click="$emit('updateText')"
            class="font-semibold absolute right-0 bottom-6 max-sm:bottom-10 flex cursor-pointer bg-blue-500 text-white mx-5 px-6 py-2 rounded"
          >
            Update
          </button>
        </div>
      </div>
    </div>

    <div>
      <div
        v-if="replyes.showModalDel"
        class="z-50 fixed inset-0 flex items-center justify-center bg-white/20 backdrop-brightness-30 bg-opacity-50"
      >
        <div class="bg-white p-6 rounded-lg shadow-lg w-96">
          <h2 class="text-xl font-bold text-gray-800">Delete comment</h2>
          <p class="text-gray-600 mt-2">
            Are you sure you want to delete this comment? This will remove the
            comment and can’t be undone.
          </p>

          <div class="mt-4 flex justify-end space-x-3">
            <button
              @click="replyes.showModalDel = false"
              class="bg-gray-500 text-white px-4 py-2 rounded hover:bg-gray-600"
            >
              NO, CANCEL
            </button>
            <button
              v-on:click="$emit('deleteComent')"
              class="bg-red-500 text-white px-4 py-2 rounded hover:bg-red-600"
            >
              YES, DELETE
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    replyes: {
      type: Object,
      default: () => {},
    },
  },
};
</script>
