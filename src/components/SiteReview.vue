<script setup lang="ts">
// Интерфейс для отзыва
interface Review {
  // Имя участника
  name: string;
  // Дата отзыва (месяц и год)
  date: string;
  // Текст отзыва
  review: string;
  // Путь к изображению участника
  img: string;
}

// Список отзывов
const reviewsAll: Review[] = [
  {
    name: "Jason (USA)",
    date: "March 2025",
    review:
      "First ride felt like surfing a desert wave! Unreal vibes, I’m hooked.",
    img: "/src/assets/images/reviews/1.png",
  },
  {
    name: "Lucía (España)",
    date: "Febrero 2025",
    review:
      "¡Nunca pensé que volar sobre arena fuera tan épico! Lo recomiendo 100%.",
    img: "/src/assets/images/reviews/2.png",
  },
  {
    name: "Nassim (France)",
    date: "Avril 2025",
    review:
      "Du sable, du vent et des frissons. Meilleure expérience de ma vie !",
    img: "/src/assets/images/reviews/3.png",
  },
  {
    name: "Takumi (日本)",
    date: "2025年1月",
    review: "砂の波に乗る感覚、マジでヤバい。次の休みも絶対来る！",
    img: "/src/assets/images/reviews/4.png",
  },
  {
    name: "Mia (Deutschland)",
    date: "März 2025",
    review: "Wie Snowboarden, nur heißer! 😎 Sandstorming ist der neue Hype.",
    img: "/src/assets/images/reviews/5.png",
  },
  {
    name: "Rafa (Brasil)",
    date: "Janeiro 2025",
    review: "Pura adrenalina no meio do nada! Areia + vento = explosão total.",
    img: "/src/assets/images/reviews/6.png",
  },

  /*

  {
    name: " ()",
    date: "",
    review: "",
    img: "@/assets/images/review1.png",
  },

   */
];

/**
 * Возвращает случайные элементы из массива без повторений.
 *
 * @template T Тип элементов в массиве.
 * @param {T[]} elements - Исходный массив отзывов.
 * @param {number} count - Количество случайных элементов, которые нужно вернуть.
 * @returns {T[]} Массив из случайных, неповторяющихся элементов.
 */
const getRandomElements = <T,>(elements: T[], count: number): T[] => {
  const shuffled = [...elements].sort(() => 0.5 - Math.random());
  return shuffled.slice(0, count);
};

const reviews = getRandomElements(reviewsAll, 4);
</script>

<template>
  <article class="wrap-container review">
    <header class="w-full md:w-1/2 md:ml-auto">
      <h1 id="review">{{ $t("review") }}</h1>
      <h2>
        {{ $t("Join the team!") }}
      </h2>
    </header>
    <section class="reviews mb-5 flex flex-col md:flex-row gap-[2em]">
      <article
        v-for="(review, index) in reviews"
        :key="index"
        class="review w-full md:basis-1/2 lg:basis-1/4"
        :class="[
          // До широкого экрана показываем только 2 отзыва, остальные скрываем
          index >= 2 ? 'hidden lg:block' : '',
          // На широких экранах у нечётных отзывов добавляем отступы
          index % 2 === 0 ? 'lg:self-end lg:mt-[4vw]' : 'lg:self-start',
        ]"
      >
        <img :src="review.img" :alt="review.name" class="review-img" />
        <div class="review-text-container flex flex-col gap-[1em] xl:flex-row">
          <div class="review-text xl:basis-2/3">
            {{ review.review }}
          </div>
          <div class="review-user self-end xl:basis-1/3">
            <div class="text-right">
              <span class="hidden xl:inline">/ </span>{{ review.name }}
            </div>
            <div class="text-right">{{ review.date }}</div>
          </div>
        </div>
      </article>
    </section>
  </article>
</template>

<style lang="css" scoped>
.review {
  margin-bottom: clamp(50px, 11vw, 150px);
}

header {
  margin-bottom: clamp(30px, 7vw, 100px);
}
</style>
