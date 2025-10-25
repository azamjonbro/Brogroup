<template>
    <div class="cards_container" >
        <div data-aos="fade-down" v-for="item in projects.slice(0, 4)" :key="item.id" class="card">
            <div class="title">{{ item.projectName }}</div>
            <div class="icon"><i class="fa-thin fa-laptop-code"></i></div>
            <div class="content">
                <p>{{ item.description.length > 250 ? item.description.slice(0, 250) + '...' : item.description }}</p>
            </div>
            <div class="cards_end">
                <p>{{ item.time }}</p>
                <button class="card_btn" @click="$router.push(`/project/${item.id}`)">
                    <span>Batafsil...</span>
                </button>
            </div>
        </div>
    </div>
</template>


<script>
// import axios from "../../utils/axios" 
import AOS from 'aos'
import 'aos/dist/aos.css'
export default {
    mounted() {
        AOS.init({
            duration: 1000, // animatsiya davomiyligi
            once: false      // bir marta scroll qilinsa animatsiya ishlaydi
        })
    },

    // async mounted(){
    //     try{
    //         const res = await axios.get("posts")
    //         console.log(res);

    //     }catch(err){
    //         console.log(err+"project 14 qator");

    //     }

    // }
    data() {
        return {
            projects: [
                {
                    id: 48291736,
                    projectName: "Yosh Dasturchilar Platformasi",
                    description:
                        "Bu loyiha yosh dasturchilar uchun yaratilgan interaktiv o‘quv platformasidir. Unda foydalanuvchilar turli dasturlash tillarini bosqichma-bosqich o‘rganishlari, testlar yechishlari va o‘z loyihalarini joylash imkoniga ega bo‘ladilar. Platforma sun’iy intellekt yordamida foydalanuvchining bilim darajasini tahlil qilib, unga mos kurslarni tavsiya etadi. Shuningdek, foydalanuvchilar o‘zaro fikr almashish, savollar berish va hamkorlikda loyiha yaratish imkoniyatiga ham ega. Bu loyiha yoshlar orasida IT sohasiga bo‘lgan qiziqishni oshirishga xizmat qiladi.",
                    time: "2025-10-25 19:21",
                },
                {
                    id: 90518342,
                    projectName: "EkoMarket Onlayn Do‘koni",
                    description:
                        "EkoMarket – bu ekologik toza mahsulotlar sotiladigan onlayn do‘kon platformasidir. Loyihaning asosiy maqsadi sog‘lom turmush tarzini targ‘ib qilish va chiqindisiz hayotni qo‘llab-quvvatlashdir. Foydalanuvchilar mahalliy fermerlardan olingan tabiiy mahsulotlarni to‘g‘ridan-to‘g‘ri xarid qilishlari mumkin. Platformada mahsulotlar haqida to‘liq ma’lumot, mijozlar fikrlari va ekologik ta’sir ko‘rsatkichi keltiriladi. EkoMarket orqali xaridorlar sog‘lom oziq-ovqat bilan birga atrof-muhitni asrashga ham hissa qo‘shadilar.",
                    time: "2025-10-25 19:22",
                },
                {
                    id: 71920458,
                    projectName: "SmartCity Monitoring Tizimi",
                    description:
                        "SmartCity loyihasi shahar infratuzilmasini raqamlashtirish va boshqaruvni avtomatlashtirish uchun mo‘ljallangan. Tizim transport oqimini, havo sifatini, energiya sarfini va chiqindilar miqdorini real vaqt rejimida kuzatadi. Har bir hududdagi ma’lumotlar yagona markazga uzatiladi va tahlil qilinadi. Bu orqali hokimiyat organlari tezkor qarorlar qabul qilib, resurslarni samarali taqsimlay oladilar. Shuningdek, aholi mobil ilova orqali shahar hayotidagi muammolarni (masalan, chiqindi yig‘ilmagan joy, yo‘l nosozligi) to‘g‘ridan-to‘g‘ri bildirish imkoniga ega bo‘ladi.",
                    time: "2025-10-25 19:23",
                },
                {
                    id: 83475612,
                    projectName: "EduLink Masofaviy Ta’lim Platformasi",
                    description:
                        "EduLink – bu masofaviy ta’limni qulay shaklda tashkil etish uchun yaratilgan zamonaviy tizim. O‘qituvchilar va talabalar videodarslar, interaktiv testlar hamda virtual sinflar orqali birgalikda ishlashlari mumkin. Platforma AI yordamida o‘quvchining o‘zlashtirish darajasini kuzatib boradi va individual ta’lim yo‘lini shakllantiradi. EduLink pandemiya davrida yoki chekka hududlardagi ta’lim muassasalari uchun ayniqsa foydalidir. U bilim olish jarayonini soddalashtiradi va sifatni oshiradi.",
                    time: "2025-10-25 19:24",
                },
                {
                    id: 57390284,
                    projectName: "AgroBot Fermerlar Yordamchisi",
                    description:
                        "AgroBot – bu qishloq xo‘jaligi bilan shug‘ullanuvchi fermerlar uchun mo‘ljallangan raqamli yordamchi tizim. Ilova sun’iy intellekt yordamida ekin holatini, ob-havo sharoitini va hosildorlik darajasini tahlil qiladi. Shuningdek, foydalanuvchiga o‘z vaqtida o‘g‘itlash, sug‘orish yoki zararkunandalarga qarshi kurashish bo‘yicha tavsiyalar beradi. AgroBot orqali fermerlar resurslarni tejash, hosildorlikni oshirish va ekologik xavfsizlikni ta’minlash imkoniga ega bo‘ladilar.",
                    time: "2025-10-25 19:25",
                },
                {
                    id: 19037465,
                    projectName: "BookSpace Elektron Kutubxonasi",
                    description:
                        "BookSpace – bu raqamli kitoblar uchun mo‘ljallangan interaktiv platforma. Unda foydalanuvchilar o‘z sevimli kitoblarini onlayn o‘qishlari, izoh qoldirishlari va muhokamalarda qatnashishlari mumkin. Platforma o‘quv odatini mustahkamlash, o‘zbek adabiyotini targ‘ib qilish va yoshlar orasida kitobxonlik madaniyatini rivojlantirishga qaratilgan. Har bir foydalanuvchi o‘z shaxsiy kutubxonasini yaratib, uni do‘stlari bilan bo‘lishishi mumkin. Tizimda ovozli kitoblar (audiobook) funksiyasi ham mavjud.",
                    time: "2025-10-25 19:26",
                },
                {
                    id: 60294731,
                    projectName: "HealthTrack Sog‘lom Hayot Ilovasi",
                    description:
                        "HealthTrack – bu sog‘lom turmush tarzini kuzatib borish uchun ishlab chiqilgan mobil dastur. Ilova foydalanuvchining jismoniy faolligi, ovqatlanish tartibi va uyqu sifatini tahlil qiladi. Shuningdek, foydalanuvchi sog‘lom maqsadlar qo‘yib, ularni bosqichma-bosqich bajarishini kuzatadi. Ilova AI yordamida foydalanuvchining tanasi uchun mos mashg‘ulot va ovqatlanish rejasini shakllantiradi. Maqsad – foydalanuvchilarga sog‘lom hayot tarzini shakllantirishda yordam berish.",
                    time: "2025-10-25 19:27",
                },
                {
                    id: 49380217,
                    projectName: "TourUz Sayohat Platformasi",
                    description:
                        "TourUz – bu O‘zbekiston bo‘ylab sayohat qilishni osonlashtiruvchi onlayn platforma. Foydalanuvchilar mamlakatning tarixiy joylari, madaniy merosi va tabiat go‘zalliklari haqida ma’lumot olishlari mumkin. Tizim foydalanuvchiga marshrut tuzish, mehmonxona bron qilish va mahalliy gidlar bilan bog‘lanish imkonini beradi. TourUzning maqsadi – ichki turizmni rivojlantirish va xorijiy sayyohlarga qulay xizmat ko‘rsatish. Har bir joy haqida batafsil ma’lumot, suratlar va sharhlar mavjud.",
                    time: "2025-10-25 19:28",
                },
                {
                    id: 85741269,
                    projectName: "FinWise Moliyaviy Tahlil Platformasi",
                    description:
                        "FinWise – bu kichik biznes egalari uchun mo‘ljallangan moliyaviy boshqaruv tizimi. Ilova daromad va xarajatlarni avtomatik tarzda tahlil qilib, foydalanuvchiga hisobotlar yaratadi. Sun’iy intellekt yordamida tizim xarajatlarni kamaytirish va foydani oshirish bo‘yicha tavsiyalar beradi. Foydalanuvchilar o‘z bizneslarini raqamli tarzda boshqarishlari, budjet rejalashtirishni avtomatlashtirishlari va moliyaviy holatini yaxshiroq nazorat qilishlari mumkin. FinWise kichik korxonalar uchun samarali raqamli yechim hisoblanadi.",
                    time: "2025-10-25 19:29",
                },
                {
                    id: 71620893,
                    projectName: "ArtLink Rassomlar Hamjamiyati",
                    description:
                        "ArtLink – bu ijodkorlar va rassomlar uchun mo‘ljallangan onlayn platforma. Unda foydalanuvchilar o‘z asarlarini joylashlari, baham ko‘rishlari va boshqa rassomlar bilan hamkorlik qilishlari mumkin. Platforma raqamli san’atni rivojlantirish, yosh rassomlarni qo‘llab-quvvatlash va ijodiy g‘oyalarni targ‘ib qilishni maqsad qiladi. ArtLink doirasida onlayn ko‘rgazmalar, tanlovlar va o‘quv dasturlari ham tashkil etiladi. Bu loyiha ijodkorlar uchun global miqyosda imkoniyatlar eshigini ochadi.",
                    time: "2025-10-25 19:30",
                },
            ]
        }
    }
}
</script>

<style>
.cards_container {
    /* border: 2px solid red; */
    display: grid;
    grid-template-columns: repeat(2, 40%);
    justify-content: space-around;
    width: 100%;
    background: #d0dbe1;
    gap: 8%;
    padding: 5rem 0;
}

.card {
    width: 100%;
    --grad: red, blue;
    padding: 2.5rem;
    background-image: linear-gradient(to bottom left, #e0e4e5, #f2f6f9);
    border-radius: 2rem;
    gap: 1.5rem;
    display: grid;
    grid-template: 'title icon' 'content content' 'bar bar' / 1fr auto;
    font-family: system-ui, sans-serif;
    color: #444447;
    box-shadow:
        inset -2px 2px hsl(0 0 100% / 1),
        -20px 20px 40px hsl(0 0 0 / .25);
}

.card .title {
    font-size: 1.5rem;
    grid-area: title;
    align-self: end;
    text-transform: uppercase;
    font-weight: 500;
    word-break: break-all;
}

.card .icon {
    grid-area: icon;
    font-size: 3rem;
    border: 1px solid red;
}

.card .icon>i {
    color: transparent;
    background: linear-gradient(to right, var(--grad));
    background-clip: text;
    -webkit-background-clip: text;
}

.card .content {
    grid-area: content;
}

.card .content>*:first-child {
    margin-top: 0rem;
}

.card .content>*:last-child {
    margin-bottom: 0rem;
}

.card::after {
    content: "";
    grid-area: bar;
    height: 2px;
    background-image: linear-gradient(90deg, var(--grad));
    /* margin-inline: -1.5rem; */

}

.cards_end {
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.card_btn span {
    color: black;
    font-size: 16px;
    /* background-color: red; */
}
</style>