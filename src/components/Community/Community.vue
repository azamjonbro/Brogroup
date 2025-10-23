<template>
    <section class="community">
        <div class="container">
            <!-- Header -->
            <header class="community-header">
                <h1>Community</h1>
                <p class="subtitle">Jamoa haqida qisqacha — hamkorlaringiz va muallif haqida ma'lumot</p>
            </header>

            <!-- Creator card -->
            <div class="creator-card">
                <div class="avatar-wrap">
                    <img :src="creator.avatar" alt="creator avatar" class="avatar" />
                    <span class="avatar-glow" aria-hidden="true"></span>
                </div>

                <div class="creator-info">
                    <div class="top-row">
                        <div>
                            <h2 class="creator-name">{{ creator.name }}</h2>
                            <p class="creator-role">{{ creator.role }}</p>
                        </div>
                        <div class="cta">
                            <a :href="creator.website" target="_blank" class="btn">
                                Batafsil
                                <svg width="14" height="14" viewBox="0 0 24 24" fill="none" class="btn-icon" aria-hidden="true">
                                    <path d="M5 12h14M13 5l7 7-7 7" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                                </svg>
                            </a>
                        </div>
                    </div>

                    <p class="creator-bio">{{ creator.bio }}</p>

                    <div class="meta">
                        <span class="chip">Founder</span>
                        <span class="chip">Open to collaborations</span>
                    </div>
                </div>
            </div>

            <!-- Partners Swiper -->
            <section class="partners-section">
                <div class="partners-header">
                    <h3>Hamkorlar</h3>
                    <p class="partners-desc">Loyihada ishtirok etgan tashkilotlar va sheriklar</p>
                </div>
                <!-- <PartnerSlider :partners="partners" /> -->
            </section>
        </div>
    </section>
</template>

<script setup>
import { ref } from 'vue'
import PartnerSlider from '@/components/PartnerSlider/PartnerSlider.vue'

const creator = ref({
    name: 'Ismingiz Familiyangiz',
    role: 'Community yaratuvchisi',
    avatar: 'https://images.unsplash.com/photo-1544005313-94ddf0286df2?q=80&w=400&auto=format&fit=crop&ixlib=rb-4.0.3',
    bio: 'Bu yerda qisqacha o‘zingiz haqingizda ma’lumot yozing — nima qilyapsiz, nima maqsadingiz va qanday sherikliklarga ochiq ekanligingizni ko‘rsating.',
    website: '#'
})

const partners = ref([
    { name: 'Partner A', logo: 'https://via.placeholder.com/160x80?text=Partner+A' },
    { name: 'Partner B', logo: 'https://via.placeholder.com/160x80?text=Partner+B' },
    { name: 'Partner C', logo: 'https://via.placeholder.com/160x80?text=Partner+C' },
    { name: 'Partner D', logo: 'https://via.placeholder.com/160x80?text=Partner+D' },
    { name: 'Partner E', logo: 'https://via.placeholder.com/160x80?text=Partner+E' }
])
</script>



<style scoped>
/* Base */
.community {
    padding: 56px 16px;
    color: var(--bg); /* Updated to use theme color */
    background: var(--bg-primary-surface);
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}

.community-header h1 {
    margin: 0;
    font-size: 28px;
    color: var(--bg); /* Updated for contrast */
    letter-spacing: -0.02em;
}

.subtitle {
    margin: 6px 0 0;
    color: var(--text-muted);
    font-size: 14px;
}

.creator-card {
    background: linear-gradient(180deg, var(--bg-primary-surface), rgba(4,14,32,0.9));
    color: var(--bg);
    border: 2px solid var(--color-primary);
    border-radius: var(--radius-md);
    transition: var(--transition-fast);
}

.btn {
    background: linear-gradient(90deg, var(--color-primary) 0%, var(--primary-hover) 100%);
    color: var(--text-on-primary);
    border-radius: var(--radius-md);
    box-shadow: 0 6px 18px var(--primary-outline);
    transition: var(--transition-fast);
}

/* Header */
.community-header {
    text-align: center;
    margin-bottom: 28px;
}
.community-header h1 {
    margin: 0;
    font-size: 28px;
    color: #0b2540;
    letter-spacing: -0.02em;
}
.subtitle {
    margin: 6px 0 0;
    color: #51607a;
    font-size: 14px;
}

/* Creator card */
.creator-card {
    display: flex;
    gap: 20px;
    align-items: center;
    /* theme variable + dark surface for creator card */
    background: linear-gradient(180deg, #020A18, rgba(4,14,32,0.9));
    color: #e6eef8;
    border: 2px solid white;
    padding: 20px;
    border-radius: 16px;
    box-shadow: 0 8px 30px rgba(20,36,59,0.08);
    margin-bottom: 30px;
    transition: transform 220ms ease, box-shadow 220ms ease;
}
.creator-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 20px 40px rgba(18,35,70,0.12);
}

/* Avatar */
.avatar-wrap {
    position: relative;
    width: 104px;
    height: 104px;
    flex-shrink: 0;
    display: flex;
    align-items: center;
    justify-content: center;
}
.avatar {
    width: 96px;
    height: 96px;
    border-radius: 14px;
    object-fit: cover;
    border: 4px solid white;
    box-shadow: 0 6px 18px rgba(11,36,70,0.06);
    transition: transform 220ms ease;
}
.creator-card:hover .avatar {
    transform: translateY(-4px) rotate(-1deg);
}
.avatar-glow {
    position: absolute;
    width: 120px;
    height: 120px;
    border-radius: 50%;
    background: radial-gradient(closest-side, rgba(99,102,241,0.12), transparent 50%);
    z-index: 0;
    pointer-events: none;
}

/* Info */
.creator-info {
    flex: 1;
    position: relative;
    z-index: 1;
}
.top-row {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 16px;
}
.creator-name {
    margin: 0;
    font-size: 18px;
    font-weight: 700;
    color: #082033;
}
.creator-role {
    margin: 6px 0 0;
    font-size: 13px;
    color: #58708b;
}

/* Bio */
.creator-bio {
    margin: 12px 0 14px;
    color: #3a4a63;
    line-height: 1.5;
    max-width: 70ch;
}

/* CTA */
.cta {
    display: flex;
    align-items: center;
}
.btn {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 10px 14px;
    background: linear-gradient(90deg, #2563eb 0%, #06b6d4 100%);
    color: white;
    border-radius: 10px;
    text-decoration: none;
    font-weight: 600;
    font-size: 13px;
    box-shadow: 0 6px 18px rgba(6,32,100,0.12);
    transition: transform 160ms ease, box-shadow 160ms ease, opacity 160ms ease;
}
.btn:hover {
    transform: translateY(-3px);
    box-shadow: 0 18px 40px rgba(6,32,100,0.14);
    opacity: 0.98;
}
.btn-icon {
    display: inline-block;
    color: rgba(255,255,255,0.95);
}

/* Meta chips */
.meta {
    display: flex;
    gap: 8px;
    margin-top: 6px;
    flex-wrap: wrap;
}
.chip {
   
    color: #2b3a66;
    padding: 6px 8px;
    font-size: 12px;
    border-radius: 999px;
    border: 1px solid rgba(99,102,241,0.12);
}

/* Partners */
.partners-section {
    margin-top: 6px;
    padding: 18px;
    
    border-radius: 12px;
    border: 1px solid rgba(15,35,64,0.03);
}
.partners-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 12px;
    margin-bottom: 12px;
}
.partners-header h3 {
    margin: 0;
    font-size: 16px;
    color: #0b2540;
}
.partners-desc {
    margin: 0;
    color: #556575;
    font-size: 13px;
}

/* Responsive */
@media (max-width: 820px) {
    .creator-card {
        gap: 14px;
    }
    .avatar-wrap {
        width: 92px;
        height: 92px;
    }
    .avatar {
        width: 84px;
        height: 84px;
    }
    .creator-bio {
        max-width: 100%;
    }
}
@media (max-width: 640px) {
    .creator-card {
        flex-direction: column;
        text-align: center;
        align-items: center;
    }
    .top-row {
        width: 100%;
        flex-direction: column;
        gap: 12px;
    }
    .cta {
        justify-content: center;
    }
    .meta {
        justify-content: center;
    }
}
</style>
