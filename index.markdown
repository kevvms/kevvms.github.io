---
layout: home
cover: true
title: "welcome! 👋🏼"
---

<style>
/* Layout helpers for responsive image visibility */
.desktop-only { float: right; margin-left: 40px; display: block !important; }
.mobile-only  { display: none !important; }

/* Breakpoints */
@media (max-width: 767px) {
    .desktop-only { display: none !important; }
    .mobile-only  { display: flex !important; justify-content: center; align-items: center; margin: 0 auto 1rem; }
}
@media (min-width: 768px) {
    .mobile-only  { display: none !important; }
    .desktop-only { display: block !important; }
}
</style>

<div class="desktop-only">
    <img src="https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExYzF3ODJtcmR2MHMyZWE4dzg1czZmc3Vud3JoeGVnaWt4bHoyZ2xjZyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/JIX9t2j0ZTN9S/giphy.gif"
             width="200" alt="enjoy a gif ;)">
</div>

Hey there! Just a code tinkerer sharing experiments, notes, and snippets. Hope you get around :D

> _"You must be the change you wish to see in the world."_ ~**Mahatma Gandhi**
{:.lead}

<div class="mobile-only">
    <img src="https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExYzF3ODJtcmR2MHMyZWE4dzg1czZmc3Vud3JoeGVnaWt4bHoyZ2xjZyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/JIX9t2j0ZTN9S/giphy.gif"
             width="200" alt="enjoy a gif ;)">
</div>