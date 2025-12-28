<script setup>
import { ref, computed, onMounted } from 'vue'

const isRtl = ref(true)
const currentLang = ref('ar')
const isMenuOpen = ref(false)
const isScrolled = ref(false)
const activeTab = ref(0)

const toggleLanguage = () => {
  isRtl.value = !isRtl.value
  currentLang.value = isRtl.value ? 'ar' : 'en'
  document.documentElement.dir = isRtl.value ? 'rtl' : 'ltr'
}

const content = computed(() => currentLang.value === 'ar' ? arContent : enContent)

const arContent = {
  nav: {
    home: 'الرئيسية',
    about: 'من نحن',
    products: 'منتجاتنا',
    brands: 'علاماتنا',
    operations: 'العمليات',
    contact: 'تواصل معنا'
  },
  hero: {
    badge: 'الموزع الرائد في العراق',
    title: 'الدلة',
    subtitle: 'شريكك الموثوق في سلاسل الإمداد',
    desc: 'نربط العلامات التجارية العالمية بالمستهلك العراقي من خلال شبكة توزيع متكاملة تغطي جميع المحافظات',
    cta1: 'استكشف خدماتنا',
    cta2: 'تواصل معنا',
    stats: [
      { value: '+3000', label: 'نقطة بيع' },
      { value: '18', label: 'محافظة' },
      { value: '+6', label: 'علامة تجارية' },
      { value: '24/7', label: 'دعم متواصل' }
    ]
  },
  about: {
    badge: 'قصة نجاحنا',
    title: 'من نحن',
    subtitle: 'الجسر الموثوق بين العلامات العالمية والمستهلك المحلي',
    desc: 'شركة الدلة للتجارة العامة المحدودة من الشركات العراقية الرائدة المتخصصة في توزيع السلع الاستهلاكية السريعة الحركة (FMCG)، تشمل منتجاتنا الأغذية والمشروبات والبهارات ومنتجات التنظيف والعناية المنزلية.',
    features: [
      { icon: 'target', title: 'هدفنا', desc: 'بناء شبكة توزيع قوية تمتد إلى جميع محافظات العراق' },
      { icon: 'eye', title: 'رؤيتنا', desc: 'الريادة في قطاع التوزيع من خلال الشفافية والابتكار' },
      { icon: 'rocket', title: 'رسالتنا', desc: 'ضمان وصول أفضل المنتجات لكل بيت عراقي بأعلى جودة' }
    ],
    values: [
      { icon: 'shield', title: 'الشفافية', desc: 'علاقات قائمة على المصداقية' },
      { icon: 'star', title: 'الاحترافية', desc: 'معايير عالمية في الإدارة' },
      { icon: 'bulb', title: 'الابتكار', desc: 'تطوير مستمر في أساليبنا' },
      { icon: 'globe', title: 'المسؤولية', desc: 'أثر إيجابي للمجتمع' }
    ]
  },
  products: {
    badge: 'تشكيلتنا المتنوعة',
    title: 'منتجاتنا',
    subtitle: 'مجموعة واسعة من المنتجات عالية الجودة لتلبية احتياجات السوق العراقي',
    categories: [
      { icon: 'grain', title: 'الأغذية الأساسية', desc: 'الأرز، البقوليات، المعلبات', image: 'https://images.unsplash.com/photo-1586201375761-83865001e31c?w=800' },
      { icon: 'spice', title: 'البهارات والتوابل', desc: 'تشكيلة واسعة من البهارات', image: 'https://images.unsplash.com/photo-1596040033229-a9821ebd058d?w=800' },
      { icon: 'drink', title: 'المشروبات الصحية', desc: 'خيارات متنوعة للمشروبات', image: 'https://images.unsplash.com/photo-1544145945-f90425340c7e?w=800' },
      { icon: 'clean', title: 'المنظفات والورقيات', desc: 'منتجات تنظيف فعالة', image: 'https://images.unsplash.com/photo-1583947215259-38e31be8751f?w=800' },
      { icon: 'home', title: 'العناية المنزلية', desc: 'عناية شاملة للأسرة', image: 'https://images.unsplash.com/photo-1563453392212-326f5e854473?w=800' },
      { icon: 'grill', title: 'منتجات الشواء', desc: 'جودة وموثوقية', image: 'https://images.unsplash.com/photo-1555939594-58d7cb561ad1?w=800' }
    ]
  },
  brands: {
    badge: 'شركاء النجاح',
    title: 'علاماتنا التجارية',
    subtitle: 'نستورد من أفضل الشركات العالمية المعروفة بجودتها',
    items: [
      { name: 'WOW', type: 'منظفات ومنتجات ورقية', country: 'الأردن', color: '#3b82f6', icon: 'sparkle' },
      { name: 'الأسرة', type: 'بهارات وأرز ومنتجات غذائية', country: 'الهند', color: '#f59e0b', icon: 'grain' },
      { name: 'ڤاليو', type: 'منتجات عناية منزلية', country: 'الأردن', color: '#10b981', icon: 'home' },
      { name: 'سناك بيك', type: 'سناك ومقرمشات', country: 'مصر', color: '#ef4444', icon: 'snack' },
      { name: 'ChaiTea', type: 'مشروبات صحية وطبيعية', country: 'بولندا', color: '#8b5cf6', icon: 'tea' },
      { name: 'NARI', type: 'منتجات شواء', country: 'اندونيسيا', color: '#ec4899', icon: 'fire' }
    ]
  },
  operations: {
    badge: 'قوة التشغيل',
    title: 'العمليات والتوزيع',
    subtitle: 'منظومة تشغيل وتوزيع متكاملة تضمن الكفاءة والموثوقية',
    features: [
      { icon: 'warehouse', title: 'مخازن مركزية', desc: 'لتخزين المنتجات الجافة والمبردة', image: 'https://images.unsplash.com/photo-1586528116311-ad8dd3c8310d?w=800' },
      { icon: 'map', title: 'تغطية وطنية', desc: 'تمتد إلى جميع المحافظات', image: 'https://images.unsplash.com/photo-1524661135-423995f22d0b?w=800' },
      { icon: 'tech', title: 'أنظمة رقمية', desc: 'لمتابعة الطلبات والمخزون', image: 'https://images.unsplash.com/photo-1460925895917-afdab827c52f?w=800' },
      { icon: 'truck', title: 'أسطول نقل', desc: 'يضمن كفاءة التسليم', image: 'https://images.unsplash.com/photo-1519003722824-194d4455a60c?w=800' }
    ],
    stats: [
      { value: '+3000', label: 'متجر بقالة', icon: 'store' },
      { value: '+500', label: 'سوبرماركت', icon: 'cart' },
      { value: '+250', label: 'تاجر جملة', icon: 'box' },
      { value: '+200', label: 'حساب رئيسي', icon: 'key' }
    ]
  },
  whyUs: {
    title: 'لماذا الدلة؟',
    items: [
      { icon: 'network', title: 'انتشار وطني', desc: 'تغطية شاملة لجميع المحافظات' },
      { icon: 'handshake', title: 'شراكات موثوقة', desc: 'مع علامات عالمية رائدة' },
      { icon: 'gear', title: 'كفاءة تشغيلية', desc: 'سلسلة إمداد قوية ومتكاملة' },
      { icon: 'badge', title: 'التزام دائم', desc: 'بالجودة والمصداقية' },
      { icon: 'growth', title: 'ثقافة مؤسسية', desc: 'قائمة على التطوير المستمر' }
    ]
  },
  contact: {
    badge: 'نحن هنا لخدمتك',
    title: 'تواصل معنا',
    subtitle: 'للاستفسارات والشراكات التجارية',
    info: {
      email: 'info@aldalla.iq',
      phone1: '+964 7850556677',
      phone2: '+964 7750556677',
      address: 'بغداد، العراق'
    },
    form: {
      name: 'الاسم الكامل',
      email: 'البريد الإلكتروني',
      phone: 'رقم الهاتف',
      company: 'اسم الشركة',
      message: 'رسالتك',
      submit: 'إرسال الرسالة'
    }
  },
  footer: {
    desc: 'شركة عراقية رائدة في توزيع السلع الاستهلاكية',
    rights: 'جميع الحقوق محفوظة',
    company: 'شركة الدلة للتجارة العامة المحدودة'
  }
}

const enContent = {
  nav: {
    home: 'Home',
    about: 'About',
    products: 'Products',
    brands: 'Brands',
    operations: 'Operations',
    contact: 'Contact'
  },
  hero: {
    badge: 'Leading Distributor in Iraq',
    title: 'Al-Dalla',
    subtitle: 'Your Trusted Supply Chain Partner',
    desc: 'We connect global brands with Iraqi consumers through an integrated distribution network covering all governorates',
    cta1: 'Explore Services',
    cta2: 'Contact Us',
    stats: [
      { value: '+3000', label: 'Points of Sale' },
      { value: '18', label: 'Governorates' },
      { value: '+6', label: 'Brands' },
      { value: '24/7', label: 'Support' }
    ]
  },
  about: {
    badge: 'Our Story',
    title: 'About Us',
    subtitle: 'The Trusted Bridge Between Global Brands and Local Consumers',
    desc: 'Al-Dalla General Trading Company Ltd. is a leading Iraqi company specialized in distributing Fast Moving Consumer Goods (FMCG), including food products, beverages, spices, and cleaning and home care products.',
    features: [
      { icon: 'target', title: 'Our Goal', desc: 'Building a strong distribution network across all Iraqi governorates' },
      { icon: 'eye', title: 'Our Vision', desc: 'Leadership in distribution through transparency and innovation' },
      { icon: 'rocket', title: 'Our Mission', desc: 'Ensuring the best products reach every Iraqi home with highest quality' }
    ],
    values: [
      { icon: 'shield', title: 'Transparency', desc: 'Relationships built on credibility' },
      { icon: 'star', title: 'Professionalism', desc: 'Global standards in management' },
      { icon: 'bulb', title: 'Innovation', desc: 'Continuous improvement in methods' },
      { icon: 'globe', title: 'Responsibility', desc: 'Positive impact on community' }
    ]
  },
  products: {
    badge: 'Our Selection',
    title: 'Our Products',
    subtitle: 'Wide range of high-quality products to meet the needs of the Iraqi market',
    categories: [
      { icon: 'grain', title: 'Basic Foods', desc: 'Rice, Legumes, Canned Goods', image: 'https://images.unsplash.com/photo-1586201375761-83865001e31c?w=800' },
      { icon: 'spice', title: 'Spices & Seasonings', desc: 'Wide selection of spices', image: 'https://images.unsplash.com/photo-1596040033229-a9821ebd058d?w=800' },
      { icon: 'drink', title: 'Healthy Beverages', desc: 'Various drink options', image: 'https://images.unsplash.com/photo-1544145945-f90425340c7e?w=800' },
      { icon: 'clean', title: 'Detergents & Paper', desc: 'Effective cleaning products', image: 'https://images.unsplash.com/photo-1583947215259-38e31be8751f?w=800' },
      { icon: 'home', title: 'Home Care', desc: 'Complete family care', image: 'https://images.unsplash.com/photo-1563453392212-326f5e854473?w=800' },
      { icon: 'grill', title: 'BBQ Products', desc: 'Quality and reliability', image: 'https://images.unsplash.com/photo-1555939594-58d7cb561ad1?w=800' }
    ]
  },
  brands: {
    badge: 'Success Partners',
    title: 'Our Brands',
    subtitle: 'We import from the best global companies known for their quality',
    items: [
      { name: 'WOW', type: 'Detergents & Paper Products', country: 'Jordan', color: '#3b82f6', icon: 'sparkle' },
      { name: 'Al-Osra', type: 'Spices, Rice & Food Products', country: 'India', color: '#f59e0b', icon: 'grain' },
      { name: 'Value', type: 'Home Care Products', country: 'Jordan', color: '#10b981', icon: 'home' },
      { name: 'Snack Pick', type: 'Snacks & Chips', country: 'Egypt', color: '#ef4444', icon: 'snack' },
      { name: 'ChaiTea', type: 'Health & Natural Drinks', country: 'Poland', color: '#8b5cf6', icon: 'tea' },
      { name: 'NARI', type: 'BBQ Products', country: 'Indonesia', color: '#ec4899', icon: 'fire' }
    ]
  },
  operations: {
    badge: 'Operational Power',
    title: 'Operations & Distribution',
    subtitle: 'Integrated operations system ensuring efficiency and reliability',
    features: [
      { icon: 'warehouse', title: 'Central Warehouses', desc: 'For dry and refrigerated storage', image: 'https://images.unsplash.com/photo-1586528116311-ad8dd3c8310d?w=800' },
      { icon: 'map', title: 'National Coverage', desc: 'Extending to all governorates', image: 'https://images.unsplash.com/photo-1524661135-423995f22d0b?w=800' },
      { icon: 'tech', title: 'Digital Systems', desc: 'Order and inventory tracking', image: 'https://images.unsplash.com/photo-1460925895917-afdab827c52f?w=800' },
      { icon: 'truck', title: 'Transport Fleet', desc: 'Ensuring delivery efficiency', image: 'https://images.unsplash.com/photo-1519003722824-194d4455a60c?w=800' }
    ],
    stats: [
      { value: '+3000', label: 'Grocery Stores', icon: 'store' },
      { value: '+500', label: 'Supermarkets', icon: 'cart' },
      { value: '+250', label: 'Wholesalers', icon: 'box' },
      { value: '+200', label: 'Key Accounts', icon: 'key' }
    ]
  },
  whyUs: {
    title: 'Why Al-Dalla?',
    items: [
      { icon: 'network', title: 'National Reach', desc: 'Complete coverage of all governorates' },
      { icon: 'handshake', title: 'Trusted Partnerships', desc: 'With leading global brands' },
      { icon: 'gear', title: 'Operational Efficiency', desc: 'Strong integrated supply chain' },
      { icon: 'badge', title: 'Constant Commitment', desc: 'To quality and credibility' },
      { icon: 'growth', title: 'Corporate Culture', desc: 'Based on continuous development' }
    ]
  },
  contact: {
    badge: 'We Are Here For You',
    title: 'Contact Us',
    subtitle: 'For inquiries and business partnerships',
    info: {
      email: 'info@aldalla.iq',
      phone1: '+964 7850556677',
      phone2: '+964 7750556677',
      address: 'Baghdad, Iraq'
    },
    form: {
      name: 'Full Name',
      email: 'Email Address',
      phone: 'Phone Number',
      company: 'Company Name',
      message: 'Your Message',
      submit: 'Send Message'
    }
  },
  footer: {
    desc: 'Leading Iraqi company in FMCG distribution',
    rights: 'All Rights Reserved',
    company: 'Al-Dalla General Trading Company Ltd.'
  }
}

if (typeof window !== 'undefined') {
  window.addEventListener('scroll', () => {
    isScrolled.value = window.scrollY > 50
  })
}

onMounted(() => {
  document.documentElement.dir = 'rtl'
  document.documentElement.lang = 'ar'
})

const submitForm = () => {
  alert(isRtl.value ? 'شكراً لتواصلك! سنرد عليك قريباً' : 'Thank you! We will contact you soon')
}
</script>

<template>
  <div :dir="isRtl ? 'rtl' : 'ltr'" class="min-h-screen bg-[#0a1628]">
    <!-- Navbar - Corporate Navy Style -->
    <nav :class="['fixed top-0 left-0 right-0 z-50 transition-all duration-500', isScrolled ? 'bg-[#0a1628]/98 backdrop-blur-2xl shadow-xl shadow-black/10 py-4' : 'bg-transparent py-6']">
      <div class="max-w-7xl mx-auto px-6 lg:px-8">
        <div class="flex items-center justify-between">
          <!-- Logo with Company Name -->
          <a href="#home" class="flex items-center gap-4 group">
            <img src="./assets/logo.svg" alt="Al-Dalla Logo" class="h-16 w-auto group-hover:scale-105 transition-transform" />
            <div class="hidden sm:block">
              <h1 class="text-xl font-bold text-white">{{ isRtl ? 'الدلة' : 'Al-Dalla' }}</h1>
              <p class="text-xs text-[#38bfbe] font-medium">{{ isRtl ? 'الموزع الرائد' : 'Leading Distributor' }}</p>
            </div>
          </a>

          <!-- Desktop Nav - Horizontal Pills -->
          <div class="hidden lg:flex items-center gap-2">
            <a v-for="(item, key) in content.nav" :key="key" :href="`#${key}`"
               class="px-5 py-3 text-gray-300 hover:text-white hover:bg-[#38bfbe]/10 font-medium transition-all rounded-xl text-sm border border-transparent hover:border-[#38bfbe]/20">
              {{ item }}
            </a>
          </div>

          <!-- Actions -->
          <div class="hidden md:flex items-center gap-4">
            <button @click="toggleLanguage" class="w-12 h-12 rounded-xl font-bold transition-all bg-[#38bfbe]/10 text-[#38bfbe] hover:bg-[#38bfbe]/20 border border-[#38bfbe]/20 flex items-center justify-center">
              {{ currentLang === 'ar' ? 'EN' : 'ع' }}
            </button>
            <a href="#contact" class="btn-primary py-3.5 px-7">
              <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20 13V6a2 2 0 00-2-2H6a2 2 0 00-2 2v7m16 0v5a2 2 0 01-2 2H6a2 2 0 01-2-2v-5m16 0h-2.586a1 1 0 00-.707.293l-2.414 2.414a1 1 0 01-.707.293h-3.172a1 1 0 01-.707-.293l-2.414-2.414A1 1 0 006.586 13H4" /></svg>
              {{ isRtl ? 'شراكة تجارية' : 'Partnership' }}
            </a>
          </div>

          <!-- Mobile Menu Button -->
          <button @click="isMenuOpen = !isMenuOpen" class="lg:hidden p-3 text-white bg-[#38bfbe]/10 hover:bg-[#38bfbe]/20 rounded-xl border border-[#38bfbe]/20 transition-all">
            <svg v-if="!isMenuOpen" class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" /></svg>
            <svg v-else class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" /></svg>
          </button>
        </div>

        <!-- Mobile Menu -->
        <transition enter-active-class="transition duration-300 ease-out" enter-from-class="opacity-0 -translate-y-4" enter-to-class="opacity-100 translate-y-0" leave-active-class="transition duration-200 ease-in" leave-from-class="opacity-100 translate-y-0" leave-to-class="opacity-0 -translate-y-4">
          <div v-show="isMenuOpen" class="lg:hidden mt-4 bg-[#0f1d32] rounded-2xl p-6 border border-white/10 shadow-2xl">
            <div class="flex flex-col gap-2">
              <a v-for="(item, key) in content.nav" :key="key" :href="`#${key}`" @click="isMenuOpen = false" class="font-medium text-gray-300 hover:text-white py-3.5 px-5 hover:bg-[#38bfbe]/10 rounded-xl transition-all text-lg">{{ item }}</a>
              <hr class="border-white/10 my-3">
              <div class="flex items-center gap-3">
                <button @click="toggleLanguage" class="flex-1 py-3.5 px-5 bg-[#38bfbe]/10 rounded-xl font-medium text-[#38bfbe] transition-all">{{ currentLang === 'ar' ? 'English' : 'عربي' }}</button>
                <a href="#contact" @click="isMenuOpen = false" class="flex-1 btn-primary text-center justify-center py-3.5">{{ isRtl ? 'تواصل' : 'Contact' }}</a>
              </div>
            </div>
          </div>
        </transition>
      </div>
    </nav>

    <!-- Hero Section -->
    <section id="home" class="relative min-h-screen flex items-center overflow-hidden">
      <!-- Background Effects -->
      <div class="absolute inset-0 gradient-mesh"></div>
      <div class="absolute inset-0 pattern-grid opacity-30"></div>

      <!-- Animated Orbs -->
      <div class="absolute top-1/4 left-[10%] w-[500px] h-[500px] bg-[#38bfbe]/20 rounded-full blur-[150px] animate-pulse-slow"></div>
      <div class="absolute bottom-1/4 right-[10%] w-[400px] h-[400px] bg-[#f59e0b]/10 rounded-full blur-[120px] animate-pulse-slow" style="animation-delay: 2s;"></div>

      <!-- Floating Elements -->
      <div class="absolute top-[20%] right-[15%] w-20 h-20 border border-[#38bfbe]/20 rounded-2xl animate-float opacity-40" style="animation-delay: 0s;"></div>
      <div class="absolute bottom-[30%] left-[10%] w-16 h-16 border border-[#f59e0b]/20 rounded-full animate-float opacity-30" style="animation-delay: 2s;"></div>
      <div class="absolute top-[40%] left-[20%] w-3 h-3 bg-[#38bfbe] rounded-full animate-float opacity-60" style="animation-delay: 1s;"></div>

      <div class="relative z-10 max-w-7xl mx-auto px-6 lg:px-8 pt-32 pb-24">
        <div class="grid lg:grid-cols-2 gap-16 items-center">
          <!-- Content -->
          <div class="animate-fade-in">
            <!-- Badge -->
            <div class="inline-flex items-center gap-3 glass px-5 py-2.5 rounded-full mb-8">
              <span class="w-2 h-2 bg-[#38bfbe] rounded-full animate-pulse"></span>
              <span class="text-[#38bfbe] font-semibold text-sm">{{ content.hero.badge }}</span>
              <svg class="w-4 h-4 text-[#f59e0b]" fill="currentColor" viewBox="0 0 20 20"><path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"/></svg>
            </div>

            <h1 class="text-6xl md:text-7xl lg:text-8xl font-black text-white mb-4 leading-[0.95]">
              {{ content.hero.title }}
            </h1>

            <h2 class="text-2xl md:text-3xl font-bold text-gradient mb-6">{{ content.hero.subtitle }}</h2>

            <p class="text-gray-400 text-lg leading-relaxed mb-10 max-w-xl">{{ content.hero.desc }}</p>

            <div class="flex flex-wrap gap-4 mb-14">
              <a href="#products" class="btn-primary">
                <span>{{ content.hero.cta1 }}</span>
                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 8l4 4m0 0l-4 4m4-4H3" /></svg>
              </a>
              <a href="#contact" class="btn-white">{{ content.hero.cta2 }}</a>
            </div>

            <!-- Stats -->
            <div class="grid grid-cols-4 gap-4">
              <div v-for="(stat, i) in content.hero.stats" :key="i" class="text-center">
                <div class="text-2xl md:text-3xl font-black text-white mb-1">{{ stat.value }}</div>
                <div class="text-xs text-gray-500 font-medium">{{ stat.label }}</div>
              </div>
            </div>
          </div>

          <!-- Hero Visual -->
          <div class="hidden lg:block relative">
            <!-- Main Card -->
            <div class="relative">
              <div class="absolute inset-0 gradient-primary rounded-[32px] blur-2xl opacity-20 animate-pulse-slow"></div>
              <div class="relative glass rounded-[32px] p-8 border border-white/10">
                <!-- Main Image -->
                <div class="relative rounded-2xl overflow-hidden mb-6">
                  <img src="https://images.unsplash.com/photo-1586528116311-ad8dd3c8310d?w=800" alt="Warehouse" class="w-full h-72 object-cover" />
                  <div class="absolute inset-0 bg-gradient-to-t from-[#0a1628] via-transparent to-transparent"></div>
                  <div class="absolute bottom-4 left-4 right-4">
                    <div class="glass rounded-xl px-4 py-3 flex items-center justify-between">
                      <div class="flex items-center gap-3">
                        <div class="w-10 h-10 bg-[#38bfbe] rounded-lg flex items-center justify-center">
                          <svg class="w-5 h-5 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" /></svg>
                        </div>
                        <div>
                          <p class="text-white font-bold text-sm">{{ isRtl ? 'توزيع موثوق' : 'Reliable Distribution' }}</p>
                          <p class="text-gray-400 text-xs">{{ isRtl ? 'تغطية كاملة' : 'Full Coverage' }}</p>
                        </div>
                      </div>
                      <div class="text-[#38bfbe] font-bold">100%</div>
                    </div>
                  </div>
                </div>

                <!-- Mini Cards -->
                <div class="grid grid-cols-2 gap-4">
                  <div class="bg-white/5 rounded-xl p-4 border border-white/5">
                    <div class="flex items-center gap-3 mb-3">
                      <div class="w-10 h-10 bg-[#f59e0b]/20 rounded-lg flex items-center justify-center">
                        <svg class="w-5 h-5 text-[#f59e0b]" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4" /></svg>
                      </div>
                      <span class="text-white font-bold">{{ isRtl ? 'المنتجات' : 'Products' }}</span>
                    </div>
                    <div class="text-3xl font-black text-gradient-gold">+500</div>
                  </div>
                  <div class="bg-white/5 rounded-xl p-4 border border-white/5">
                    <div class="flex items-center gap-3 mb-3">
                      <div class="w-10 h-10 bg-[#38bfbe]/20 rounded-lg flex items-center justify-center">
                        <svg class="w-5 h-5 text-[#38bfbe]" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" /><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" /></svg>
                      </div>
                      <span class="text-white font-bold">{{ isRtl ? 'التغطية' : 'Coverage' }}</span>
                    </div>
                    <div class="text-3xl font-black text-gradient">18</div>
                  </div>
                </div>
              </div>
            </div>

            <!-- Floating Badge -->
            <div class="absolute -top-6 -left-6 glass rounded-2xl p-4 animate-float border border-white/10">
              <div class="flex items-center gap-3">
                <div class="w-12 h-12 gradient-primary rounded-xl flex items-center justify-center">
                  <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4M7.835 4.697a3.42 3.42 0 001.946-.806 3.42 3.42 0 014.438 0 3.42 3.42 0 001.946.806 3.42 3.42 0 013.138 3.138 3.42 3.42 0 00.806 1.946 3.42 3.42 0 010 4.438 3.42 3.42 0 00-.806 1.946 3.42 3.42 0 01-3.138 3.138 3.42 3.42 0 00-1.946.806 3.42 3.42 0 01-4.438 0 3.42 3.42 0 00-1.946-.806 3.42 3.42 0 01-3.138-3.138 3.42 3.42 0 00-.806-1.946 3.42 3.42 0 010-4.438 3.42 3.42 0 00.806-1.946 3.42 3.42 0 013.138-3.138z" /></svg>
                </div>
                <div>
                  <p class="text-white font-bold text-sm">{{ isRtl ? 'موزع معتمد' : 'Certified' }}</p>
                  <p class="text-[#38bfbe] text-xs font-medium">FMCG Partner</p>
                </div>
              </div>
            </div>

            <!-- Floating Image -->
            <div class="absolute -bottom-4 -right-4 w-32 h-32 rounded-2xl overflow-hidden border-4 border-[#0a1628] shadow-2xl animate-float" style="animation-delay: 1s;">
              <img src="https://images.unsplash.com/photo-1553413077-190dd305871c?w=400" alt="Logistics" class="w-full h-full object-cover" />
            </div>
          </div>
        </div>
      </div>

      <!-- Scroll Indicator -->
      <div class="absolute bottom-8 left-1/2 -translate-x-1/2 flex flex-col items-center gap-2 animate-bounce">
        <span class="text-gray-500 text-xs">{{ isRtl ? 'اكتشف المزيد' : 'Discover More' }}</span>
        <svg class="w-5 h-5 text-[#38bfbe]" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 14l-7 7m0 0l-7-7m7 7V3" /></svg>
      </div>
    </section>

    <!-- About Section -->
    <section id="about" class="py-32 relative overflow-hidden">
      <div class="absolute inset-0 gradient-dark"></div>
      <div class="absolute top-0 left-0 right-0 h-px bg-gradient-to-r from-transparent via-[#38bfbe]/50 to-transparent"></div>

      <div class="relative z-10 max-w-7xl mx-auto px-6 lg:px-8">
        <!-- Header -->
        <div class="text-center mb-20">
          <span class="inline-flex items-center gap-2 px-5 py-2 glass text-[#38bfbe] rounded-full text-sm font-bold mb-6">
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" /></svg>
            {{ content.about.badge }}
          </span>
          <h2 class="text-4xl md:text-5xl lg:text-6xl font-black text-white mb-6">{{ content.about.title }}</h2>
          <p class="text-xl text-[#38bfbe] font-medium max-w-3xl mx-auto">{{ content.about.subtitle }}</p>
        </div>

        <div class="grid lg:grid-cols-2 gap-16 items-start mb-20">
          <!-- Left Content -->
          <div>
            <p class="text-gray-400 text-lg leading-relaxed mb-10">{{ content.about.desc }}</p>

            <!-- Features -->
            <div class="space-y-6">
              <div v-for="(feature, i) in content.about.features" :key="i"
                   class="glass rounded-2xl p-6 card-hover group cursor-pointer"
                   :class="[isRtl ? 'border-r-4' : 'border-l-4']"
                   :style="{ borderColor: i === 0 ? '#38bfbe' : i === 1 ? '#f59e0b' : '#8b5cf6' }">
                <div class="flex items-start gap-5">
                  <div class="w-14 h-14 rounded-2xl flex items-center justify-center shrink-0 transition-transform group-hover:scale-110"
                       :class="i === 0 ? 'bg-[#38bfbe]/20' : i === 1 ? 'bg-[#f59e0b]/20' : 'bg-[#8b5cf6]/20'">
                    <svg v-if="feature.icon === 'target'" class="w-7 h-7" :class="i === 0 ? 'text-[#38bfbe]' : i === 1 ? 'text-[#f59e0b]' : 'text-[#8b5cf6]'" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M15.59 14.37a6 6 0 01-5.84 7.38v-4.8m5.84-2.58a14.98 14.98 0 006.16-12.12A14.98 14.98 0 009.631 8.41m5.96 5.96a14.926 14.926 0 01-5.841 2.58m-.119-8.54a6 6 0 00-7.381 5.84h4.8m2.581-5.84a14.927 14.927 0 00-2.58 5.84m2.699 2.7c-.103.021-.207.041-.311.06a15.09 15.09 0 01-2.448-2.448 14.9 14.9 0 01.06-.312m-2.24 2.39a4.493 4.493 0 00-1.757 4.306 4.493 4.493 0 004.306-1.758M16.5 9a1.5 1.5 0 11-3 0 1.5 1.5 0 013 0z" /></svg>
                    <svg v-else-if="feature.icon === 'eye'" class="w-7 h-7" :class="i === 0 ? 'text-[#38bfbe]' : i === 1 ? 'text-[#f59e0b]' : 'text-[#8b5cf6]'" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M2.036 12.322a1.012 1.012 0 010-.639C3.423 7.51 7.36 4.5 12 4.5c4.638 0 8.573 3.007 9.963 7.178.07.207.07.431 0 .639C20.577 16.49 16.64 19.5 12 19.5c-4.638 0-8.573-3.007-9.963-7.178z" /><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" /></svg>
                    <svg v-else class="w-7 h-7" :class="i === 0 ? 'text-[#38bfbe]' : i === 1 ? 'text-[#f59e0b]' : 'text-[#8b5cf6]'" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M15.59 14.37a6 6 0 01-5.84 7.38v-4.8m5.84-2.58a14.98 14.98 0 006.16-12.12A14.98 14.98 0 009.631 8.41m5.96 5.96a14.926 14.926 0 01-5.841 2.58m-.119-8.54a6 6 0 00-7.381 5.84h4.8m2.581-5.84a14.927 14.927 0 00-2.58 5.84m2.699 2.7c-.103.021-.207.041-.311.06a15.09 15.09 0 01-2.448-2.448 14.9 14.9 0 01.06-.312m-2.24 2.39a4.493 4.493 0 00-1.757 4.306 4.493 4.493 0 004.306-1.758M16.5 9a1.5 1.5 0 11-3 0 1.5 1.5 0 013 0z" /></svg>
                  </div>
                  <div>
                    <h4 class="text-xl font-bold text-white mb-2">{{ feature.title }}</h4>
                    <p class="text-gray-400">{{ feature.desc }}</p>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Values Grid -->
          <div class="grid grid-cols-2 gap-5">
            <div v-for="(value, i) in content.about.values" :key="i"
                 class="glass rounded-3xl p-7 card-3d text-center group"
                 :class="i % 2 === 1 ? 'mt-8' : ''">
              <div class="w-16 h-16 mx-auto gradient-primary rounded-2xl flex items-center justify-center mb-5 group-hover:scale-110 transition-transform shadow-lg shadow-[#38bfbe]/20">
                <svg v-if="value.icon === 'shield'" class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M9 12.75L11.25 15 15 9.75m-3-7.036A11.959 11.959 0 013.598 6 11.99 11.99 0 003 9.749c0 5.592 3.824 10.29 9 11.623 5.176-1.332 9-6.03 9-11.622 0-1.31-.21-2.571-.598-3.751h-.152c-3.196 0-6.1-1.248-8.25-3.285z" /></svg>
                <svg v-else-if="value.icon === 'star'" class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M11.48 3.499a.562.562 0 011.04 0l2.125 5.111a.563.563 0 00.475.345l5.518.442c.499.04.701.663.321.988l-4.204 3.602a.563.563 0 00-.182.557l1.285 5.385a.562.562 0 01-.84.61l-4.725-2.885a.562.562 0 00-.586 0L6.982 20.54a.562.562 0 01-.84-.61l1.285-5.386a.562.562 0 00-.182-.557l-4.204-3.602a.562.562 0 01.321-.988l5.518-.442a.563.563 0 00.475-.345L11.48 3.5z" /></svg>
                <svg v-else-if="value.icon === 'bulb'" class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M12 18v-5.25m0 0a6.01 6.01 0 001.5-.189m-1.5.189a6.01 6.01 0 01-1.5-.189m3.75 7.478a12.06 12.06 0 01-4.5 0m3.75 2.383a14.406 14.406 0 01-3 0M14.25 18v-.192c0-.983.658-1.823 1.508-2.316a7.5 7.5 0 10-7.517 0c.85.493 1.509 1.333 1.509 2.316V18" /></svg>
                <svg v-else class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M12 21a9.004 9.004 0 008.716-6.747M12 21a9.004 9.004 0 01-8.716-6.747M12 21c2.485 0 4.5-4.03 4.5-9S14.485 3 12 3m0 18c-2.485 0-4.5-4.03-4.5-9S9.515 3 12 3m0 0a8.997 8.997 0 017.843 4.582M12 3a8.997 8.997 0 00-7.843 4.582m15.686 0A11.953 11.953 0 0112 10.5c-2.998 0-5.74-1.1-7.843-2.918m15.686 0A8.959 8.959 0 0121 12c0 .778-.099 1.533-.284 2.253m0 0A17.919 17.919 0 0112 16.5c-3.162 0-6.133-.815-8.716-2.247m0 0A9.015 9.015 0 013 12c0-1.605.42-3.113 1.157-4.418" /></svg>
              </div>
              <h4 class="font-bold text-white text-lg mb-2">{{ value.title }}</h4>
              <p class="text-gray-400 text-sm leading-relaxed">{{ value.desc }}</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Products Section -->
    <section id="products" class="py-32 relative overflow-hidden">
      <div class="absolute inset-0 bg-[#0a1628]"></div>
      <div class="absolute inset-0 pattern-dots"></div>

      <div class="relative z-10 max-w-7xl mx-auto px-6 lg:px-8">
        <div class="text-center mb-16">
          <span class="inline-flex items-center gap-2 px-5 py-2 glass text-[#38bfbe] rounded-full text-sm font-bold mb-6">
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4" /></svg>
            {{ content.products.badge }}
          </span>
          <h2 class="text-4xl md:text-5xl lg:text-6xl font-black text-white mb-6">{{ content.products.title }}</h2>
          <p class="text-xl text-gray-400 max-w-2xl mx-auto">{{ content.products.subtitle }}</p>
        </div>

        <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
          <div v-for="(cat, i) in content.products.categories" :key="i"
               class="group relative rounded-3xl overflow-hidden card-hover cursor-pointer h-80">
            <img :src="cat.image" :alt="cat.title" class="w-full h-full object-cover group-hover:scale-110 transition-transform duration-700" />
            <div class="absolute inset-0 bg-gradient-to-t from-[#0a1628] via-[#0a1628]/60 to-transparent"></div>

            <!-- Content -->
            <div class="absolute inset-0 p-7 flex flex-col justify-end">
              <div class="transform group-hover:-translate-y-2 transition-transform duration-500">
                <div class="w-14 h-14 gradient-primary rounded-2xl flex items-center justify-center mb-4 shadow-lg">
                  <svg class="w-7 h-7 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4" /></svg>
                </div>
                <h3 class="text-2xl font-bold text-white mb-2">{{ cat.title }}</h3>
                <p class="text-gray-300">{{ cat.desc }}</p>
              </div>
            </div>

            <!-- Hover Arrow -->
            <div class="absolute top-6 right-6 w-12 h-12 glass rounded-xl flex items-center justify-center opacity-0 group-hover:opacity-100 transition-all transform translate-x-4 group-hover:translate-x-0">
              <svg class="w-5 h-5 text-white" :class="isRtl ? 'rotate-180' : ''" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 8l4 4m0 0l-4 4m4-4H3" /></svg>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Brands Section -->
    <section id="brands" class="py-32 relative overflow-hidden">
      <div class="absolute inset-0 gradient-dark"></div>

      <div class="relative z-10 max-w-7xl mx-auto px-6 lg:px-8">
        <div class="text-center mb-16">
          <span class="inline-flex items-center gap-2 px-5 py-2 glass text-[#f59e0b] rounded-full text-sm font-bold mb-6">
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11.049 2.927c.3-.921 1.603-.921 1.902 0l1.519 4.674a1 1 0 00.95.69h4.915c.969 0 1.371 1.24.588 1.81l-3.976 2.888a1 1 0 00-.363 1.118l1.518 4.674c.3.922-.755 1.688-1.538 1.118l-3.976-2.888a1 1 0 00-1.176 0l-3.976 2.888c-.783.57-1.838-.197-1.538-1.118l1.518-4.674a1 1 0 00-.363-1.118l-3.976-2.888c-.784-.57-.38-1.81.588-1.81h4.914a1 1 0 00.951-.69l1.519-4.674z" /></svg>
            {{ content.brands.badge }}
          </span>
          <h2 class="text-4xl md:text-5xl lg:text-6xl font-black text-white mb-6">{{ content.brands.title }}</h2>
          <p class="text-xl text-gray-400 max-w-2xl mx-auto">{{ content.brands.subtitle }}</p>
        </div>

        <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
          <div v-for="(brand, i) in content.brands.items" :key="i"
               class="glass rounded-3xl p-8 card-3d group cursor-pointer border border-white/5 hover:border-white/20">
            <div class="flex items-start justify-between mb-6">
              <div class="w-16 h-16 rounded-2xl flex items-center justify-center text-white text-2xl font-black shadow-lg"
                   :style="{ backgroundColor: brand.color }">
                {{ brand.name.charAt(0) }}
              </div>
              <div class="glass px-4 py-2 rounded-full">
                <span class="text-gray-300 text-sm font-medium">{{ brand.country }}</span>
              </div>
            </div>
            <h3 class="text-2xl font-bold text-white mb-2 group-hover:text-gradient transition-all">{{ brand.name }}</h3>
            <p class="text-gray-400">{{ brand.type }}</p>

            <!-- Decorative line -->
            <div class="mt-6 h-1 rounded-full bg-gradient-to-r opacity-50 group-hover:opacity-100 transition-opacity"
                 :style="{ backgroundImage: `linear-gradient(to right, ${brand.color}, transparent)` }"></div>
          </div>
        </div>
      </div>
    </section>

    <!-- Operations Section -->
    <section id="operations" class="py-32 relative overflow-hidden">
      <div class="absolute inset-0 bg-[#0a1628]"></div>
      <div class="absolute inset-0 pattern-grid opacity-20"></div>

      <div class="relative z-10 max-w-7xl mx-auto px-6 lg:px-8">
        <div class="text-center mb-16">
          <span class="inline-flex items-center gap-2 px-5 py-2 glass text-[#38bfbe] rounded-full text-sm font-bold mb-6">
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z" /><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" /></svg>
            {{ content.operations.badge }}
          </span>
          <h2 class="text-4xl md:text-5xl lg:text-6xl font-black text-white mb-6">{{ content.operations.title }}</h2>
          <p class="text-xl text-gray-400 max-w-2xl mx-auto">{{ content.operations.subtitle }}</p>
        </div>

        <!-- Features Grid -->
        <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-6 mb-16">
          <div v-for="(feature, i) in content.operations.features" :key="i"
               class="group relative rounded-3xl overflow-hidden h-96 card-hover">
            <img :src="feature.image" :alt="feature.title" class="w-full h-full object-cover group-hover:scale-110 transition-transform duration-700" />
            <div class="absolute inset-0 bg-gradient-to-t from-[#0a1628] via-[#0a1628]/80 to-transparent"></div>

            <div class="absolute inset-0 p-6 flex flex-col justify-end">
              <div class="w-14 h-14 gradient-primary rounded-2xl flex items-center justify-center mb-4 shadow-lg group-hover:scale-110 transition-transform">
                <svg class="w-7 h-7 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4" /></svg>
              </div>
              <h3 class="text-xl font-bold text-white mb-2">{{ feature.title }}</h3>
              <p class="text-gray-300 text-sm">{{ feature.desc }}</p>
            </div>
          </div>
        </div>

        <!-- Stats -->
        <div class="glass rounded-3xl p-10 border border-white/10">
          <div class="grid grid-cols-2 md:grid-cols-4 gap-8">
            <div v-for="(stat, i) in content.operations.stats" :key="i" class="text-center">
              <div class="text-4xl md:text-5xl font-black text-gradient mb-3">{{ stat.value }}</div>
              <div class="text-gray-400 font-medium">{{ stat.label }}</div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Why Us Section -->
    <section class="py-32 relative overflow-hidden">
      <div class="absolute inset-0 gradient-mesh"></div>

      <div class="relative z-10 max-w-7xl mx-auto px-6 lg:px-8">
        <div class="text-center mb-16">
          <h2 class="text-4xl md:text-5xl lg:text-6xl font-black text-white">{{ content.whyUs.title }}</h2>
        </div>

        <div class="grid md:grid-cols-3 lg:grid-cols-5 gap-6">
          <div v-for="(item, i) in content.whyUs.items" :key="i"
               class="glass rounded-3xl p-8 card-hover text-center group">
            <div class="w-16 h-16 mx-auto gradient-primary rounded-2xl flex items-center justify-center mb-5 group-hover:scale-110 transition-transform shadow-lg shadow-[#38bfbe]/20">
              <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M9 12.75L11.25 15 15 9.75M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>
            </div>
            <h3 class="font-bold text-white text-lg mb-2">{{ item.title }}</h3>
            <p class="text-gray-400 text-sm">{{ item.desc }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="py-32 relative overflow-hidden">
      <div class="absolute inset-0 gradient-dark"></div>

      <div class="relative z-10 max-w-7xl mx-auto px-6 lg:px-8">
        <div class="text-center mb-16">
          <span class="inline-flex items-center gap-2 px-5 py-2 glass text-[#38bfbe] rounded-full text-sm font-bold mb-6">
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" /></svg>
            {{ content.contact.badge }}
          </span>
          <h2 class="text-4xl md:text-5xl lg:text-6xl font-black text-white mb-6">{{ content.contact.title }}</h2>
          <p class="text-xl text-gray-400">{{ content.contact.subtitle }}</p>
        </div>

        <div class="grid lg:grid-cols-5 gap-10 max-w-6xl mx-auto">
          <!-- Contact Info -->
          <div class="lg:col-span-2">
            <div class="glass rounded-3xl overflow-hidden h-full">
              <div class="relative h-48">
                <img src="https://images.unsplash.com/photo-1577563908411-5077b6dc7624?w=800" alt="Contact" class="w-full h-full object-cover" />
                <div class="absolute inset-0 gradient-primary opacity-80"></div>
                <div class="absolute inset-0 flex items-center justify-center">
                  <div class="w-20 h-20 bg-white/20 backdrop-blur-xl rounded-full flex items-center justify-center">
                    <svg class="w-10 h-10 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M8.625 12a.375.375 0 11-.75 0 .375.375 0 01.75 0zm0 0H8.25m4.125 0a.375.375 0 11-.75 0 .375.375 0 01.75 0zm0 0H12m4.125 0a.375.375 0 11-.75 0 .375.375 0 01.75 0zm0 0h-.375M21 12c0 4.556-4.03 8.25-9 8.25a9.764 9.764 0 01-2.555-.337A5.972 5.972 0 015.41 20.97a5.969 5.969 0 01-.474-.065 4.48 4.48 0 00.978-2.025c.09-.457-.133-.901-.467-1.226C3.93 16.178 3 14.189 3 12c0-4.556 4.03-8.25 9-8.25s9 3.694 9 8.25z" /></svg>
                  </div>
                </div>
              </div>

              <div class="p-8 space-y-6">
                <div class="flex items-center gap-5">
                  <div class="w-14 h-14 bg-[#38bfbe]/10 rounded-2xl flex items-center justify-center shrink-0">
                    <svg class="w-6 h-6 text-[#38bfbe]" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M21.75 6.75v10.5a2.25 2.25 0 01-2.25 2.25h-15a2.25 2.25 0 01-2.25-2.25V6.75m19.5 0A2.25 2.25 0 0019.5 4.5h-15a2.25 2.25 0 00-2.25 2.25m19.5 0v.243a2.25 2.25 0 01-1.07 1.916l-7.5 4.615a2.25 2.25 0 01-2.36 0L3.32 8.91a2.25 2.25 0 01-1.07-1.916V6.75" /></svg>
                  </div>
                  <div>
                    <p class="text-gray-500 text-sm mb-1">{{ isRtl ? 'البريد الإلكتروني' : 'Email' }}</p>
                    <p class="text-white font-semibold">{{ content.contact.info.email }}</p>
                  </div>
                </div>

                <div class="flex items-center gap-5">
                  <div class="w-14 h-14 bg-[#38bfbe]/10 rounded-2xl flex items-center justify-center shrink-0">
                    <svg class="w-6 h-6 text-[#38bfbe]" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M2.25 6.75c0 8.284 6.716 15 15 15h2.25a2.25 2.25 0 002.25-2.25v-1.372c0-.516-.351-.966-.852-1.091l-4.423-1.106c-.44-.11-.902.055-1.173.417l-.97 1.293c-.282.376-.769.542-1.21.38a12.035 12.035 0 01-7.143-7.143c-.162-.441.004-.928.38-1.21l1.293-.97c.363-.271.527-.734.417-1.173L6.963 3.102a1.125 1.125 0 00-1.091-.852H4.5A2.25 2.25 0 002.25 4.5v2.25z" /></svg>
                  </div>
                  <div>
                    <p class="text-gray-500 text-sm mb-1">{{ isRtl ? 'الهاتف' : 'Phone' }}</p>
                    <p class="text-white font-semibold" dir="ltr">{{ content.contact.info.phone1 }}</p>
                    <p class="text-white font-semibold" dir="ltr">{{ content.contact.info.phone2 }}</p>
                  </div>
                </div>

                <div class="flex items-center gap-5">
                  <div class="w-14 h-14 bg-[#38bfbe]/10 rounded-2xl flex items-center justify-center shrink-0">
                    <svg class="w-6 h-6 text-[#38bfbe]" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M15 10.5a3 3 0 11-6 0 3 3 0 016 0z" /><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M19.5 10.5c0 7.142-7.5 11.25-7.5 11.25S4.5 17.642 4.5 10.5a7.5 7.5 0 1115 0z" /></svg>
                  </div>
                  <div>
                    <p class="text-gray-500 text-sm mb-1">{{ isRtl ? 'العنوان' : 'Address' }}</p>
                    <p class="text-white font-semibold">{{ content.contact.info.address }}</p>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Contact Form -->
          <div class="lg:col-span-3">
            <div class="glass-light rounded-3xl p-10">
              <form @submit.prevent="submitForm" class="space-y-6">
                <div class="grid md:grid-cols-2 gap-6">
                  <div>
                    <label class="block text-sm font-semibold text-gray-700 mb-3">{{ content.contact.form.name }}</label>
                    <input type="text" required class="w-full px-5 py-4 rounded-2xl border-2 border-gray-100 focus:border-[#38bfbe] outline-none transition-all bg-gray-50/50 text-gray-800" />
                  </div>
                  <div>
                    <label class="block text-sm font-semibold text-gray-700 mb-3">{{ content.contact.form.company }}</label>
                    <input type="text" class="w-full px-5 py-4 rounded-2xl border-2 border-gray-100 focus:border-[#38bfbe] outline-none transition-all bg-gray-50/50 text-gray-800" />
                  </div>
                </div>
                <div class="grid md:grid-cols-2 gap-6">
                  <div>
                    <label class="block text-sm font-semibold text-gray-700 mb-3">{{ content.contact.form.email }}</label>
                    <input type="email" required class="w-full px-5 py-4 rounded-2xl border-2 border-gray-100 focus:border-[#38bfbe] outline-none transition-all bg-gray-50/50 text-gray-800" />
                  </div>
                  <div>
                    <label class="block text-sm font-semibold text-gray-700 mb-3">{{ content.contact.form.phone }}</label>
                    <input type="tel" class="w-full px-5 py-4 rounded-2xl border-2 border-gray-100 focus:border-[#38bfbe] outline-none transition-all bg-gray-50/50 text-gray-800" dir="ltr" />
                  </div>
                </div>
                <div>
                  <label class="block text-sm font-semibold text-gray-700 mb-3">{{ content.contact.form.message }}</label>
                  <textarea rows="5" required class="w-full px-5 py-4 rounded-2xl border-2 border-gray-100 focus:border-[#38bfbe] outline-none resize-none transition-all bg-gray-50/50 text-gray-800"></textarea>
                </div>
                <button type="submit" class="w-full btn-primary justify-center text-lg py-5">
                  <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M6 12L3.269 3.126A59.768 59.768 0 0121.485 12 59.77 59.77 0 013.27 20.876L5.999 12zm0 0h7.5" /></svg>
                  {{ content.contact.form.submit }}
                </button>
              </form>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="bg-[#060a10] border-t border-white/5">
      <div class="max-w-7xl mx-auto px-6 lg:px-8">
        <!-- Main Footer -->
        <div class="py-16 grid md:grid-cols-2 lg:grid-cols-4 gap-12">
          <!-- Company Info -->
          <div class="lg:col-span-2">
            <div class="flex items-center gap-5 mb-6">
              <img src="./assets/logo.svg" alt="Al-Dalla Logo" class="h-16 w-auto" />
              <div>
                <h3 class="font-bold text-xl text-white">{{ content.footer.company }}</h3>
                <p class="text-[#38bfbe] text-sm">aldalla.iq</p>
              </div>
            </div>
            <p class="text-gray-400 leading-relaxed mb-6 max-w-md">{{ content.footer.desc }}</p>
            <!-- Social Links -->
            <div class="flex items-center gap-3">
              <a href="https://www.facebook.com/aldalla.iq" target="_blank" class="w-11 h-11 glass rounded-xl flex items-center justify-center hover:bg-[#38bfbe] transition-all duration-300 group">
                <svg class="w-5 h-5 text-gray-400 group-hover:text-white transition-colors" fill="currentColor" viewBox="0 0 24 24"><path d="M22 12c0-5.523-4.477-10-10-10S2 6.477 2 12c0 4.991 3.657 9.128 8.438 9.878v-6.987h-2.54V12h2.54V9.797c0-2.506 1.492-3.89 3.777-3.89 1.094 0 2.238.195 2.238.195v2.46h-1.26c-1.243 0-1.63.771-1.63 1.562V12h2.773l-.443 2.89h-2.33v6.988C18.343 21.128 22 16.991 22 12z"/></svg>
              </a>
              <a href="https://www.instagram.com/aldalla.iq" target="_blank" class="w-11 h-11 glass rounded-xl flex items-center justify-center hover:bg-[#38bfbe] transition-all duration-300 group">
                <svg class="w-5 h-5 text-gray-400 group-hover:text-white transition-colors" fill="currentColor" viewBox="0 0 24 24"><path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z"/></svg>
              </a>
              <a href="https://wa.me/9647850556677" target="_blank" class="w-11 h-11 glass rounded-xl flex items-center justify-center hover:bg-[#25D366] transition-all duration-300 group">
                <svg class="w-5 h-5 text-gray-400 group-hover:text-white transition-colors" fill="currentColor" viewBox="0 0 24 24"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>
              </a>
            </div>
          </div>

          <!-- Quick Links -->
          <div>
            <h4 class="text-white font-bold text-lg mb-6">{{ isRtl ? 'روابط سريعة' : 'Quick Links' }}</h4>
            <ul class="space-y-3">
              <li><a href="#home" class="text-gray-400 hover:text-[#38bfbe] transition-colors">{{ content.nav.home }}</a></li>
              <li><a href="#about" class="text-gray-400 hover:text-[#38bfbe] transition-colors">{{ content.nav.about }}</a></li>
              <li><a href="#products" class="text-gray-400 hover:text-[#38bfbe] transition-colors">{{ content.nav.products }}</a></li>
              <li><a href="#brands" class="text-gray-400 hover:text-[#38bfbe] transition-colors">{{ content.nav.brands }}</a></li>
              <li><a href="#contact" class="text-gray-400 hover:text-[#38bfbe] transition-colors">{{ content.nav.contact }}</a></li>
            </ul>
          </div>

          <!-- Contact Info -->
          <div>
            <h4 class="text-white font-bold text-lg mb-6">{{ isRtl ? 'تواصل معنا' : 'Contact Us' }}</h4>
            <ul class="space-y-4">
              <li class="flex items-start gap-3">
                <svg class="w-5 h-5 text-[#38bfbe] mt-0.5 shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M21.75 6.75v10.5a2.25 2.25 0 0 1-2.25 2.25h-15a2.25 2.25 0 0 1-2.25-2.25V6.75m19.5 0A2.25 2.25 0 0 0 19.5 4.5h-15a2.25 2.25 0 0 0-2.25 2.25m19.5 0v.243a2.25 2.25 0 0 1-1.07 1.916l-7.5 4.615a2.25 2.25 0 0 1-2.36 0L3.32 8.91a2.25 2.25 0 0 1-1.07-1.916V6.75" /></svg>
                <span class="text-gray-400">{{ content.contact.info.email }}</span>
              </li>
              <li class="flex items-start gap-3">
                <svg class="w-5 h-5 text-[#38bfbe] mt-0.5 shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M2.25 6.75c0 8.284 6.716 15 15 15h2.25a2.25 2.25 0 0 0 2.25-2.25v-1.372c0-.516-.351-.966-.852-1.091l-4.423-1.106c-.44-.11-.902.055-1.173.417l-.97 1.293c-.282.376-.769.542-1.21.38a12.035 12.035 0 0 1-7.143-7.143c-.162-.441.004-.928.38-1.21l1.293-.97c.363-.271.527-.734.417-1.173L6.963 3.102a1.125 1.125 0 0 0-1.091-.852H4.5A2.25 2.25 0 0 0 2.25 4.5v2.25Z" /></svg>
                <span class="text-gray-400" dir="ltr">{{ content.contact.info.phone1 }}</span>
              </li>
              <li class="flex items-start gap-3">
                <svg class="w-5 h-5 text-[#38bfbe] mt-0.5 shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M15 10.5a3 3 0 1 1-6 0 3 3 0 0 1 6 0Z" /><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M19.5 10.5c0 7.142-7.5 11.25-7.5 11.25S4.5 17.642 4.5 10.5a7.5 7.5 0 1 1 15 0Z" /></svg>
                <span class="text-gray-400">{{ content.contact.info.address }}</span>
              </li>
            </ul>
          </div>
        </div>

        <!-- Copyright -->
        <div class="py-6 border-t border-white/5 flex flex-col md:flex-row justify-between items-center gap-4">
          <p class="text-gray-500 text-sm">&copy; {{ new Date().getFullYear() }} {{ content.footer.company }}. {{ content.footer.rights }}.</p>
          <p class="text-gray-600 text-xs">{{ isRtl ? 'الموزع الرائد في العراق' : 'Leading Distributor in Iraq' }}</p>
        </div>
      </div>
    </footer>

    <!-- WhatsApp Floating Button -->
    <a href="https://wa.me/9647850556677" target="_blank" class="fixed bottom-6 z-50 w-16 h-16 bg-[#25D366] rounded-full flex items-center justify-center shadow-2xl shadow-[#25D366]/40 hover:scale-110 transition-all duration-300 group" :class="isRtl ? 'left-6' : 'right-6'">
      <svg class="w-8 h-8 text-white" fill="currentColor" viewBox="0 0 24 24"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>
      <span class="absolute -top-2 -right-2 w-5 h-5 bg-red-500 rounded-full flex items-center justify-center text-white text-xs font-bold animate-pulse">1</span>
    </a>
  </div>
</template>
