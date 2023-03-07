<script setup lang="ts">
import { computed, reactive, ref } from 'vue'
import List from '@/components/List.vue'
import Emoji from '@/components/Emoji.vue'

//mock data
const status = ['Why?', "I'm ready", 'Busy', 'Shall we dance?']
const emoji = [
  { code: '&#128512;', description: 'Grinning face' },
  { code: '&#128513;', description: 'grinning face with smiling eyes' },
  { code: '&#128514;', description: 'face with tears of joy' },
  { code: '&#128515;', description: 'smiling face with open mouth' },
  { code: '&#128516;', description: 'smiling face with open mouth and smiling eyes' },
  { code: '&#128517;', description: 'smiling face with open mouth and cold sweat' },
  { code: '&#128518;', description: 'smiling face with open mouth and tightly-closed eyes' },
  { code: '&#128519;', description: 'smiling face with halo' },
  { code: '&#128520;', description: 'smiling face with horns' },
  { code: '&#128521;', description: 'winking face' },
  { code: '&#128522;', description: 'smiling face with smiling eyes' },
  { code: '&#128523;', description: 'face savouring delicious food' },
  { code: '&#128524;', description: 'relieved face' },
  { code: '&#128525;', description: 'smiling face with heart-shaped eyes' },
  { code: '&#128526;', description: 'smiling face with sunglasses' },
  { code: '&#128527;', description: 'smirking face' },
  { code: '&#128528;', description: 'neutral face' },
  { code: '&#128529;', description: 'expressionless face' },
  { code: '&#128530;', description: 'unamused face' },
  { code: '&#128531;', description: 'face with cold sweat' },
  { code: '&#128532;', description: 'pensive face' },
  { code: '&#128533;', description: 'confused face' },
  { code: '&#128534;', description: 'confounded face' },
  { code: '&#128535;', description: 'kissing face' },
  { code: '&#128536;', description: 'face throwing a kiss' },
  { code: '&#128537;', description: 'kissing face with smiling eyes' },
  { code: '&#128538;', description: 'kissing face with closed eyes' },
  { code: '&#128539;', description: 'face with stuck-out tongue' },
  { code: '&#128540;', description: 'face with stuck-out tongue and winking eye' },
  { code: '&#128541;', description: 'face with stuck-out tongue and tightly-closed eyes' },
  { code: '&#128542;', description: 'disappointed face' },
  { code: '&#128543;', description: 'worried face' },
  { code: '&#128544;', description: 'angry face' },
  { code: '&#128545;', description: 'pouting face' },
  { code: '&#128546;', description: 'crying face' },
  { code: '&#128547;', description: 'persevering face' },
  { code: '&#128548;', description: 'face with look of triumph' },
  { code: '&#128549;', description: 'disappointed but relieved face' },
  { code: '&#128550;', description: 'frowning face with open mouth' },
  { code: '&#128551;', description: 'anguished face' },
  { code: '&#128552;', description: 'fearful face' },
  { code: '&#128553;', description: 'weary face' },
  { code: '&#128554;', description: 'sleepy face' },
  { code: '&#128555;', description: 'tired face' },
  { code: '&#128556;', description: 'grimacing face' },
  { code: '&#128557;', description: 'loudly crying face' },
  { code: '&#128558;', description: 'face with open mouth' },
  { code: '&#128559;', description: 'hushed face' },
  { code: '&#128560;', description: 'face with open mouth and cold sweat' },
  { code: '&#128561;', description: 'face screaming in fear' },
  { code: '&#128562;', description: 'astonished face' },
  { code: '&#128563;', description: 'flushed face' },
  { code: '&#128564;', description: 'sleeping face' },
  { code: '&#128565;', description: 'dizzy face' },
  { code: '&#128566;', description: 'face without mouth' },
  { code: '&#128567;', description: 'face with medical mask' },
  { code: '&#128577;', description: 'slightly frowning face' },
  { code: '&#128578;', description: 'slightly smiling face' },
  { code: '&#128579;', description: 'upside-down face' },
  { code: '&#128580;', description: 'face with rolling eyes' },
  { code: '&#129296;', description: 'zipper-mouth face' },
  { code: '&#129297;', description: 'money-mouth face' },
  { code: '&#129298;', description: 'face with thermometer' },
  { code: '&#129299;', description: 'nerd face' },
  { code: '&#129300;', description: 'thinking face' },
  { code: '&#129301;', description: 'face with head-bandage' },
  { code: '&#129312;', description: 'cowboy hat face' },
  { code: '&#129313;', description: 'clown face' },
  { code: '&#129314;', description: 'nauseated face' },
  { code: '&#129315;', description: 'rolling on the floor laughing' },
  { code: '&#129316;', description: 'drooling face' },
  { code: '&#129317;', description: 'lying face' },
  { code: '&#129319;', description: 'sneezing face' },
  { code: '&#129320;', description: 'face with raised eyebrow' },
  { code: '&#129321;', description: 'star-struck' },
  { code: '&#129322;', description: 'zany face' },
  { code: '&#129323;', description: 'shushing face' },
  { code: '&#129325;', description: 'face with hand over mouth' },
  { code: '&#129326;', description: 'face vomiting' },
  { code: '&#129327;', description: 'exploding head' },
  { code: '&#129488;', description: 'face with monocle' }
]

//reactive
const messageStatus = ref('Why?')

const selectedEmoji = reactive({ code: '&#128512;', description: 'Grinning face' })
const emojiSelectOpened = ref(false)

const searchEmojiText = ref('')

//methods
const handleSelectEmojiOpened = (value) => {
  emojiSelectOpened.value = value
}

const selectEmoji = ({ code, description }) => {
  selectedEmoji.code = code
  selectedEmoji.description = description

  handleSelectEmojiOpened(false)
}

//computed
const emojiFiltered = computed(() => {
  return emoji.filter(({ description }) =>
    description.toLowerCase().includes(searchEmojiText.value.toLocaleLowerCase())
  )
})
</script>
<template>
  <div class="wrapper">
    <div class="status">
      <button class="status__emoji" @click="handleSelectEmojiOpened(!emojiSelectOpened)">
        <Emoji :code="selectedEmoji.code" :description="selectedEmoji.description" />
      </button>
      <button class="status__message">{{ messageStatus }}</button>
    </div>

    <div class="search-wrapper" v-if="emojiSelectOpened">
      <div class="search-box">
        <label class="sr-only" for="search-input-emoji">Search an Emoji by description</label>
        <input
          v-model="searchEmojiText"
          id="search-input-emoji"
          class="search-input"
          type="text"
          placeholder="Search example: Grinning face"
        />
      </div>
      <List :data="emojiFiltered">
        <template #element="{ data }">
          <Emoji :code="data.code" :description="data.description" @click="selectEmoji(data)" />
        </template>
      </List>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.wrapper {
  inline-size: 30rem;
  margin: 0 auto;
}

.status {
  padding: 1rem;
  border: 1px solid var(--color-text);
  border-radius: 0.4rem;
  button {
    background-color: transparent;
    outline: 0;
    border: 0;
    font-size: 2rem;
    color: white;
  }
}
.search-wrapper {
  padding: 0.3rem;
  margin-block-start: 0.5rem;
  border-radius: 0.4rem;
  background-color: white;
  color: black;
}
.list {
  block-size: 20rem;
  overflow-y: auto;
  font-size: 2.2rem;
}

.search-input {
  inline-size: 100%;
  margin-block-end: 0.5rem;
  line-height: 2rem;
  &::placeholder {
    font-style: italic;
  }
}
</style>
