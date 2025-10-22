<template>
    <section class="hero">
        <canvas ref="canvas" class="stars-canvas"></canvas>

        <div class="overlay"></div>

        <div class="hero-content" :class="{ enter: entered }">
            <h1>BROGROUP — Muvaffaqiyatdagi sherigingiz</h1>
            <p>
                Biz kichik bizneslar, startaplar va jamoalarga marketing, strategiya va
                rivojlanish bo'yicha amaliy yordam hamda faol hamjamiyat taqdim etamiz.
                G'oyalaringizni real natijaga aylantirishda birga ishlaymiz.
            </p>
            <button @click="$router.push('/services')">Xizmatlar</button>
        </div>
    </section>
</template>

<script>
export default {
    name: 'Hero',
    data() {
        return {
            entered: false,
            stars: [],
            raf: null,
            ctx: null,
            dpr: 1,
        };
    },
    mounted() {
        // trigger content animation
        requestAnimationFrame(() => (this.entered = true));
        this.initCanvas();
        window.addEventListener('resize', this.onResize);
    },
    beforeUnmount() {
        window.removeEventListener('resize', this.onResize);
        cancelAnimationFrame(this.raf);
    },
    methods: {
        initCanvas() {
            const canvas = this.$refs.canvas;
            this.ctx = canvas.getContext('2d');
            this.dpr = window.devicePixelRatio || 1;
            this.onResize();
            this.makeStars();
            this.animate();
        },
        onResize() {
            const canvas = this.$refs.canvas;
            const rect = this.$el.getBoundingClientRect();
            canvas.width = Math.max(800, rect.width) * this.dpr;
            canvas.height = (rect.height || window.innerHeight * 0.7) * this.dpr;
            canvas.style.width = rect.width + 'px';
            canvas.style.height = (rect.height || window.innerHeight * 0.7) + 'px';
            if (this.ctx) this.ctx.scale(this.dpr, this.dpr);
        },
        makeStars() {
            // create a varied star field
            this.stars = [];
            const rect = this.$el.getBoundingClientRect();
            const count = Math.round((rect.width * (rect.height || 600)) / 8000); // density
            for (let i = 0; i < count; i++) {
                this.stars.push({
                    x: Math.random() * rect.width,
                    y: Math.random() * (rect.height || window.innerHeight * 0.7),
                    r: Math.random() * 1.6 + 0.2,
                    speed: Math.random() * 0.6 + 0.1,
                    twinkle: Math.random() * Math.PI * 2,
                    hue: 200 + Math.random() * 60, // blue-ish to purple-ish
                });
            }
            // add a few larger glowing particles
            for (let j = 0; j < 6; j++) {
                this.stars.push({
                    x: Math.random() * rect.width,
                    y: Math.random() * (rect.height || window.innerHeight * 0.7),
                    r: Math.random() * 3 + 1.5,
                    speed: Math.random() * 0.3 + 0.05,
                    twinkle: Math.random() * Math.PI * 2,
                    glow: true,
                    hue: 180 + Math.random() * 80,
                });
            }
        },
        animate() {
            const ctx = this.ctx;
            const canvas = this.$refs.canvas;
            const w = canvas.width / this.dpr;
            const h = canvas.height / this.dpr;

            ctx.clearRect(0, 0, w, h);

            // subtle gradient background behind stars (not covering overlay)
            const g = ctx.createLinearGradient(0, 0, 0, h);
            g.addColorStop(0, 'rgba(10,12,30,0.85)');
            g.addColorStop(1, 'rgba(18,12,40,0.85)');
            ctx.fillStyle = g;
            ctx.fillRect(0, 0, w, h);

            for (let s of this.stars) {
                // move upward slowly to simulate drifting (wrap around)
                s.y -= s.speed;
                s.twinkle += 0.03 + Math.random() * 0.02;
                if (s.y < -10) s.y = h + 10;

                const alpha = 0.5 + 0.5 * Math.sin(s.twinkle) * (s.r / 2 + 0.2);
                if (s.glow) {
                    // soft glow
                    const glow = ctx.createRadialGradient(s.x, s.y, 0, s.x, s.y, s.r * 8);
                    glow.addColorStop(0, `hsla(${s.hue}, 90%, 70%, ${0.12 * alpha})`);
                    glow.addColorStop(0.4, `hsla(${s.hue}, 80%, 60%, ${0.06 * alpha})`);
                    glow.addColorStop(1, `rgba(0,0,0,0)`);
                    ctx.fillStyle = glow;
                    ctx.beginPath();
                    ctx.arc(s.x, s.y, s.r * 8, 0, Math.PI * 2);
                    ctx.fill();
                }

                ctx.beginPath();
                ctx.fillStyle = `hsla(${s.hue}, 60%, 85%, ${alpha})`;
                ctx.arc(s.x, s.y, s.r, 0, Math.PI * 2);
                ctx.fill();
            }

            // slight moving nebula layer - long, soft shapes for attraction
            ctx.save();
            ctx.globalAlpha = 0.06;
            ctx.fillStyle = 'rgba(160,110,255,0.2)';
            const t = Date.now() * 0.00005;
            ctx.translate(Math.sin(t) * 80, Math.cos(t * 0.7) * 40);
            this.drawNebula(w, h);
            ctx.restore();

            this.raf = requestAnimationFrame(this.animate);
        },
        drawNebula(w, h) {
            const ctx = this.ctx;
            // soft blobs using radial gradients
            const blobs = [
                { x: w * 0.2, y: h * 0.3, r: Math.min(w, h) * 0.6, hue: 260 },
                { x: w * 0.8, y: h * 0.6, r: Math.min(w, h) * 0.5, hue: 220 },
            ];
            for (let b of blobs) {
                const grad = ctx.createRadialGradient(b.x, b.y, 0, b.x, b.y, b.r);
                grad.addColorStop(0, `hsla(${b.hue}, 80%, 60%, 0.25)`);
                grad.addColorStop(0.4, `hsla(${b.hue}, 70%, 50%, 0.08)`);
                grad.addColorStop(1, 'rgba(0,0,0,0)');
                ctx.fillStyle = grad;
                ctx.beginPath();
                ctx.arc(b.x, b.y, b.r, 0, Math.PI * 2);
                ctx.fill();
            }
        },
    },
};
</script>

<style>
.hero {
    position: relative;
    overflow: hidden;
    height: 90vh;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #fff;
    background: linear-gradient(180deg, rgba(8,10,25,1) 0%, rgba(16,12,40,1) 100%);
    border-radius: 8px;
}

/* canvas sits behind content */
.stars-canvas {
    position: absolute;
    inset: 0;
    width: 100%;
    height: 100%;
    display: block;
    z-index: 0;
}

/* soft overlay for contrast (adds vignette) */
.overlay {
    position: absolute;
    inset: 0;
    z-index: 1;
    pointer-events: none;
    background-image:
        radial-gradient(60% 40% at 30% 30%, rgba(255,255,255,0.03), transparent 20%),
        radial-gradient(60% 40% at 70% 70%, rgba(255,200,255,0.02), transparent 20%),
        linear-gradient(180deg, rgba(0,0,0,0.05), rgba(0,0,0,0.25));
    mix-blend-mode: overlay;
}

/* centered content */
.hero-content {
    position: relative;
    z-index: 2;
    text-align: center;
    padding: 3rem 1.5rem;
    max-width: 1100px;
    transition: transform 700ms cubic-bezier(.2,.9,.2,1), opacity 700ms ease;
    transform: translateY(30px);
    opacity: 0;
    display: flex;
    flex-direction: column;
    gap: 1rem;
    align-items: center;
}
.hero-content.enter {
    transform: translateY(0);
    opacity: 1;
}

.hero-content h1 {
    width: 100%;
    font-size: clamp(1.8rem, 4vw, 3.2rem);
    margin: 0;
    font-weight: 800;
    letter-spacing: -0.02em;
    line-height: 1.02;
    background: linear-gradient(90deg, #f8fbff 0%, #ffd6f8 35%, #bff0ff 65%, #ffffff 100%);
    background-size: 220% 100%;
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
    text-shadow: 0 8px 30px rgba(6,8,25,0.6);
    transition: transform 500ms ease, filter 400ms ease;
    /* subtle pop on hover (desktop) */
}
.hero-content h1 {
    transform: translateY(-4px) scale(1.01);
    filter: drop-shadow(0 18px 40px rgba(140,80,220,0.15));
}
@keyframes headline-shimmer {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
}
.hero-content.enter h1 {
    animation: headline-shimmer 6s linear infinite;
}

/* paragraph becomes more readable and persuasive */
.hero-content p {
    margin: 0.5rem 0 0;
    max-width: 68ch;
    color: rgba(255,255,255,0.95);
    font-size: clamp(0.98rem, 1.7vw, 1.15rem);
    line-height: 1.5;
    font-weight: 500;
    letter-spacing: 0.01em;
    text-shadow: 0 4px 14px rgba(0,0,0,0.45);
    transform-origin: center;
}

/* small pill-style slogan/tagline that you can add inside .hero-content (e.g. <div class="slogan">) */
.hero-content .slogan {
    display: inline-block;
    margin-top: 0.8rem;
    padding: 0.45rem 0.9rem;
    border-radius: 999px;
    font-weight: 700;
    font-size: 0.85rem;
    letter-spacing: 0.08em;
    color: #fff;
    background: linear-gradient(90deg, rgba(255,255,255,0.06), rgba(255,255,255,0.03));
    box-shadow: 0 8px 30px rgba(140,80,220,0.12), inset 0 1px 0 rgba(255,255,255,0.03);
}

.hero-content h1 .accent {
    background: linear-gradient(90deg, #ffd6f8, #bff0ff);
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
    font-weight: 900;
    padding: 0 0.06rem;
    text-shadow: 0 10px 28px rgba(120,60,180,0.12);
}






.hero-content button {
    padding: 0.75rem 1.25rem;
    background: linear-gradient(90deg, var(--color-primary) 0%, var(--primary-hover) 100%);
    color: var(--text-on-primary);
    border-radius: var(--radius-md);
    font-weight: 700;
    font-size: 0.9375rem;
    line-height: 1;
    box-shadow: 0 6px 18px rgba(176, 60, 222, 0.18);
    transition: transform var(--transition-fast), box-shadow var(--transition-fast), background-color var(--transition-fast), opacity var(--transition-fast);
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
    border: none;
    -webkit-tap-highlight-color: transparent;
    cursor: pointer;
}

.hero-content button:hover {
    transform: translateY(-3px);
    box-shadow: 0 12px 30px rgba(176, 60, 222, 0.22);
    background: linear-gradient(90deg, var(--primary-hover) 0%, var(--color-primary) 100%);
}

.hero-content button:active {
    transform: translateY(0) scale(0.98);
    background-color: var(--primary-active);
    box-shadow: 0 6px 14px rgba(0,0,0,0.12);
}

.hero-content button:focus-visible {
    outline: none;
    box-shadow: var(--focus-ring);
}

@media (max-width: 600px) {
    .hero {
        min-height: 55vh;
    }
    .hero-content {
        padding: 2.25rem 1rem;
    }
}
</style>