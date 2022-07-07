<template>
  <q-page class="relative-position">
    <q-scroll-area class="absolute fullscreen">
      <div class="q-py-lg q-px-md row items-end q-col-gutter-md">
        <div class="col">
          <q-input
            bottom-slots
            v-model="newQweet"
            placeholder="What's happening?"
            counter
            maxlength="280"
            autogrow
            class="new_qweet"
          >
            <template v-slot:before>
              <q-avatar size="xl">
                <img src="https://cdn.quasar.dev/img/avatar5.jpg" />
              </q-avatar>
            </template>
          </q-input>
        </div>
        <div class="col col-shrink">
          <q-btn
            unelevated
            rounded
            color="primary"
            label="Tweet"
            no-caps
            :disable="!newQweet"
            class="q-mb-lg"
            @click="addNewQweet"
          />
        </div>
      </div>
      <q-separator size="10px" color="grey-2" class="divider" />

      <q-list class="q-py-md" separator>
        <transition-group
          appear
          enter-active-class="animated fadeIn slow"
          leave-active-class="animated fadeOut"
        >
          <q-item v-for="(qweet, index) in qweets" :key="index" class="qwitter">
            <q-item-section avatar>
              <q-avatar size="xl">
                <img src="https://cdn.quasar.dev/img/avatar5.jpg" />
              </q-avatar>
            </q-item-section>

            <q-item-section top>
              <q-item-label class="text-subtitle1">
                <strong>Lilitha Mdlalana</strong>
                <span class="text-grey-7 q-px-sm"
                  >@lithacodes &bull; {{ relativeDate(qweet.date) }}</span
                >
              </q-item-label>
              <q-item-label class="qweet-content text-body1">
                {{ qweet.content }}
              </q-item-label>
              <div class="qweet-icons row justify-between q-mt-sm">
                <q-btn color="grey" size="sm" icon="fa fa-comment" flat round />
                <q-btn color="grey" size="sm" icon="fa fa-retweet" flat round />
                <q-btn color="grey" size="sm" icon="fa fa-heart" flat round />
                <q-btn
                  color="grey"
                  size="sm"
                  icon="fa fa-trash"
                  flat
                  round
                  @click="deleteQweet(index)"
                />
              </div>
            </q-item-section>
          </q-item>
        </transition-group>
      </q-list>
    </q-scroll-area>
  </q-page>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { formatDistance } from 'date-fns';

const newQweet = ref('');
const qweets = ref([
  {
    content: `Lorem ipsum dolor sit amet consectetur adipisicing elit. Blanditiis,
            nihil vero molestiae libero suscipit nisi deleniti itaque sunt
            dolorem beatae cum tenetur at repudiandae quod earum nemo. Et,
            perspiciatis veniam.`,
    date: 1657154277738,
  },
  {
    content: `Lorem ipsum dolor sit amet consectetur adipisicing elit. Blanditiis,
            nihil vero molestiae libero suscipit nisi deleniti itaque sunt
            dolorem beatae cum tenetur at repudiandae quod earum nemo. Et,
            perspiciatis veniam.`,
    date: 1657154277738,
  },
  {
    content: `Lorem ipsum dolor sit amet consectetur adipisicing elit. Blanditiis,
            nihil vero molestiae libero suscipit nisi deleniti itaque sunt
            dolorem beatae cum tenetur at repudiandae quod earum nemo. Et,
            perspiciatis veniam.`,
    date: 1657154277738,
  },
]);

const relativeDate = (value: number) => formatDistance(value, new Date());

const addNewQweet = () => {
  qweets.value.unshift({
    content: newQweet.value,
    date: Date.now(),
  });
  newQweet.value = '';
};
const deleteQweet = (index: number) => qweets.value.splice(index, 1);
</script>

<style lang="scss">
.new_qweet {
  font-size: 19px;
  line-height: 1.4em;
}
.divider {
  border-top: 1px solid;
  border-bottom: 1px solid;
  border-color: $grey-5;
}
.qweet:not(:first-child) {
  border-top: 1px solid rgba(0, 0, 0, 0.12);
}
.qweet-content {
  white-space: pre-line;
}
.qweet-icons {
  margin-left: -5px;
}
</style>
