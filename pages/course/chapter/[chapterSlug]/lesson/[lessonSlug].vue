<script setup>
const course = useCourse();
const route = useRoute();

const progress = useLocalStorage("progress", []);

const isLessonComplete = computed(() => {
  if (!progress.value[chapter.value.number - 1]) {
    return false;
  }

  if (!progress.value[chapter.value.number - 1][lesson.value.number - 1]) {
    return false;
  }

  return progress.value[chapter.value.number - 1][lesson.value.number - 1];
});

const toggleComplete = () => {
  if (!progress.value[chapter.value.number - 1]) {
    progress.value[chapter.value.number - 1] = [];
  }

  progress.value[chapter.value.number - 1][lesson.value.number - 1] =
    !isLessonComplete.value;
};

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

const title = computed(() => {
  return `${chapter.value.title} - ${lesson.value.title}`;
});

useHead({ title });
</script>

<template>
  <p class="mt-0 uppercase font-bold text-sate-400 mb-1">
    Lesson {{ chapter.number }} - {{ lesson.number }}
  </p>
  <h2 class="my-0">{{ lesson.title }}</h2>
  <div class="flex space-x-4 mt-2 mb-8">
    <NuxtLink
      class="font-normal text-md text-gray-500"
      :to="lesson.sourceUrl"
      v-if="lesson.sourceUrl"
    >
      Download Source code
    </NuxtLink>
    <NuxtLink
      class="font-normal text-md text-gray-500"
      :to="lesson.downloadUrl"
      v-if="lesson.downloadUrl"
    >
      Download Video
    </NuxtLink>
  </div>
  <VideoPlayer v-if="lesson.videoId" :videoId="lesson.videoId" />
  <p class="">
    {{ lesson.text }}
  </p>
  <LessonCompleteButton
    :modelValue="isLessonComplete"
    @update:modelValue="toggleComplete"
  />
</template>
