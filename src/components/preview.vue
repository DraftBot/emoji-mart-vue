<template>
  <div class="emoji-mart-preview">
    <template v-if="emoji">
      <div class="emoji-mart-preview-emoji">
        <emoji
          :data="data"
          :emoji="emoji"
          :native="emojiProps.native"
          :skin="emojiProps.skin"
          :set="emojiProps.set"
        />
      </div>

      <div class="emoji-mart-preview-data">
        <div class="emoji-mart-preview-name">{{ emoji.name }}</div>
        <div class="emoji-mart-preview-shortnames">
          <span
            v-for="shortName in emojiShortNames"
            :key="shortName"
            class="emoji-mart-preview-shortname"
            >{{ emojiData.custom ? shortName : `:${shortName}:` }}</span
          >
        </div>
        <div class="emoji-mart-preview-emoticons">
          <span
            v-for="emoticon in emojiEmoticons"
            :key="emoticon"
            class="emoji-mart-preview-emoticon"
            >{{ emoticon }}</span
          >
        </div>
      </div>
    </template>

    <template v-else>
      <div class="emoji-mart-preview-emoji">
        <emoji
          :data="data"
          :emoji="idleEmoji"
          :native="emojiProps.native"
          :skin="emojiProps.skin"
          :set="emojiProps.set"
        />
      </div>

      <div class="emoji-mart-preview-data">
        <span class="emoji-mart-title-label">{{ title }}</span>
      </div>

      <div
        v-if="showSkinTones || showRemoveButton"
        class="emoji-mart-preview-skins"
      >
        <skins
          v-if="showSkinTones"
          :skin="skinProps.skin"
          @change="onSkinChange($event)"
        />
        <div
          class="emoji-mart-preview-remove"
          v-if="showRemoveButton"
          @click="$parent.$emit('remove')"
        >
          <svg
            width="14"
            height="18"
            viewBox="0 0 14 18"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M1 16C1 17.1 1.9 18 3 18H11C12.1 18 13 17.1 13 16V4H1V16ZM3.46 8.88L4.87 7.47L7 9.59L9.12 7.47L10.53 8.88L8.41 11L10.53 13.12L9.12 14.53L7 12.41L4.88 14.53L3.47 13.12L5.59 11L3.46 8.88ZM10.5 1L9.5 0H4.5L3.5 1H0V3H14V1H10.5Z"
              fill="#cd6e57"
            />
          </svg>
        </div>
      </div>
    </template>
  </div>
</template>

<script>
import Emoji from './Emoji.vue'
import Skins from './skins.vue'

export default {
  props: {
    data: {
      type: Object,
      required: true,
    },
    title: {
      type: String,
      required: true,
    },
    emoji: {
      type: [String, Object],
    },
    idleEmoji: {
      type: [String, Object],
      required: true,
    },
    showSkinTones: {
      type: Boolean,
      default: true,
    },
    showRemoveButton: {
      type: Boolean,
      default: true,
    },
    emojiProps: {
      type: Object,
      required: true,
    },
    skinProps: {
      type: Object,
      required: true,
    },
    onSkinChange: {
      type: Function,
      required: true,
    },
  },
  computed: {
    emojiData() {
      if (this.emoji) {
        return this.emoji
      } else {
        return {}
      }
    },
    emojiShortNames() {
      return this.emojiData.short_names
    },
    emojiEmoticons() {
      return this.emojiData.emoticons
    },
  },
  components: {
    Emoji,
    Skins,
  },
}
</script>
