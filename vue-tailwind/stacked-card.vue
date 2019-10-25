<template>
  <div class="bg-gray-200 w-full h-screen md:px-12 md:py-12 sm:px-6 sm:py-6">
    <div class="max-w-sm">
      <div
        class="relative shadow-md rounded-lg border-4 border-white"
        style="padding-bottom: 60%;"
      >
        <div class="absolute top-0 h-full w-full bg-cover bg-center rounded-lg bg-toucan"></div> <!-- :style="{ backgroundImage: `${imageSource}`}" -->
      </div>
      <div class="relative px-4 -mt-16 mb-4">
        <div class="bg-white pt-2 shadow-lg rounded-lg">
          <div class="px-3 pt-2">
            <div class="capitalize font-semibold text-lg leading-tight truncate mx-4">
              {{ title }}
            </div>
            <div class=" mt-4 mx-4">
              <div class="text-md">
                {{description}}
              </div>
              <div class="mt-2 text-sm font-thin text-gray-600">
                {{ subDescription }}
              </div>
            </div>
          </div>
          <div class="mt-4 pt-2 bg-gray-200 pb-3 px-3 rounded-b-lg flex items-baseline content-center">
            <span class="text-xs text-center w-1/2">
              <span class="bg-gray-200 text-indigo-500 inline-block rounded-full mt-2 py-1 px-2 uppercase font-semibold tracking-wide border-indigo-500 border">
                <i
                  :class="badgeIcon"
                  class="pr-1"
                ></i> {{badgeText}}</span>
            </span>
            <div class="text-center w-1/2">
              <span class="text-gray-500 text-sm">Made by </span>
              <span class="text-indigo-500 font-semibold">{{author}}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    dataset: { type: Object, default: () => {} }
  },
  data() {
    return {
      title: "Object title",
      description: "This is the main description",
      subDescription: "This is the sub description",
      objectType: OBJECT_TYPE.TEXT,
      author: "Someone"
    };
  },
  computed: {
    badgeIcon: function() {
      return getIcon(this.objectType);
    },
    badgeText: function() {
      return getText(this.objectType);
    }
  }
};

const OBJECT_TYPE = Object.freeze({
  VIDEO: "video",
  IMAGE: "image",
  TEXT: "text",
  AUDIO: "audio",
  FINANCIALS: "financials"
});

const getIcon = function(objectType) {
  switch (objectType) {
    case OBJECT_TYPE.VIDEO:
      return "icon-video";
    case OBJECT_TYPE.AUDIO:
      return "icon-volume-up";
    case OBJECT_TYPE.IMAGE:
      return "icon-picture";
    case OBJECT_TYPE.FINANCIALS:
      return "icon-chart-line";
    case OBJECT_TYPE.TEXT:
      return "icon-doc-text";
    default:
      return "icon-doc-text";
  }
};

const getText = function(objectType) {
  switch (objectType) {
    case OBJECT_TYPE.VIDEO:
      return "video";
    case OBJECT_TYPE.AUDIO:
      return "audio";
    case OBJECT_TYPE.IMAGE:
      return "image";
    case OBJECT_TYPE.FINANCIALS:
      return "financials";
    case OBJECT_TYPE.TEXT:
      return "text";
    default:
      return "unknown";
  }
};
</script>

<style>
@import url("https://unpkg.com/tailwindcss@^1.0/dist/tailwind.min.css"); /* TODO: Don't use the CDN */
@import url("./badge_font.css");

.bg-toucan {
  background-image: url("../assets/toucan.jpg");
}
</style>