<template>
  <p class="mt-0 uppercase font-bold text-sate-400 mb-1">
    Lesson {{ chapter.number }} - {{ lesson.number }}
  </p>
  <h2 class="my-0">{{ lesson.title }}</h2>
  <div class="flex space-x-4 mt-2 mb-8">
    <a
      class="font-normal text-md text-gray-500"
      :href="lesson.sourceUrl"
      v-if="lesson.sourceUrl"
    >
      Download Source code
    </a>
    <a
      class="font-normal text-md text-gray-500"
      :href="lesson.downloadUrl"
      v-if="lesson.downloadUrl"
    >
      Download Video
    </a>
  </div>
  <p class="">
    {{ lesson.text }}
  </p>
</template>

<script setup>
const course = useCourse();
const route = useRoute();

const chapter = computed(() => {
  return course.chapters.find(
    (chapter) => chapter.slug === route.params.chapterSlug
  );
});

const lesson = computed(() => {
  return chapter.value.lessons.find(
    (lesson) => lesson.slug === route.params.lessonSlug
  );
});
</script>
