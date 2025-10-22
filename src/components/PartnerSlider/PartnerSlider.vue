<template>
  <div class="partners">
    <h3 class="partners-title">Bizning sheriklar</h3>

    <swiper
      :modules="[Autoplay, Navigation, Pagination]"
      :slides-per-view="slidesPerView"
      :space-between="20"
      :loop="true"
      :autoplay="{ delay: 2500, disableOnInteraction: false }"
      navigation
      pagination
      class="partners-swiper"
    >
      <swiper-slide v-for="(p, i) in partners" :key="i" class="partner-slide">
        <div class="partner-card">
          <img :src="p.logo" :alt="p.name" />
          <p class="partner-name">{{ p.name }}</p>
        </div>
      </swiper-slide>
    </swiper>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import { Swiper, SwiperSlide } from 'swiper/vue'
import { Autoplay, Navigation, Pagination } from 'swiper/modules'
import 'swiper/css'
import 'swiper/css/navigation'
import 'swiper/css/pagination'

// Props orqali ma'lumot qabul qilamiz
defineProps({
  partners: {
    type: Array,
    required: true
  }
})

const slidesPerView = computed(() => {
  if (typeof window === 'undefined') return 3
  const w = window.innerWidth
  if (w >= 1200) return 4
  if (w >= 900) return 3
  if (w >= 600) return 2
  return 1
})
</script>

<style scoped>
.partners {
  background: white;
  padding: 18px;
  border-radius: 12px;
  box-shadow: 0 6px 20px rgba(18, 35, 70, 0.04);
}

.partners-title {
  margin: 0 0 12px;
  font-size: 16px;
  color: #0b2447;
}

.partners-swiper {
  padding-bottom: 18px;
}

.partner-slide {
  display: flex;
  justify-content: center;
  align-items: center;
}

.partner-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
  background: #f7fbff;
  padding: 12px;
  border-radius: 10px;
  min-width: 140px;
  max-width: 200px;
  text-align: center;
}

.partner-card img {
  max-width: 160px;
  height: 60px;
  object-fit: contain;
}

.partner-name {
  margin: 0;
  font-size: 13px;
  color: #213a5a;
}
</style>
