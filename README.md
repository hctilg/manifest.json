# آموزش فارسی و کامل manifest.json در وب اپلیکیشن های PWA

شما میتونید با استفاده از فایل manifest.json و service-worker.js به راحتی وبسایت خودتون رو به وب اپلیکیشن تبدیل کنید و قابلیت بارگذاری آفلاین و کش کردن فایل ها و نصب و پشتیبانی روی سیستم عامل های مختلف رو داشته باشید.

کافیه فایل های مورد نظر بسازید و تگ زیر رو به تگ head تویی صفحات وبتون اضافه کنید:
```html
<link rel="manifest" href="manifest.json"/>
```

## نمونه کامل :
```json
{
  "id": "/",
  "name": "My Awesome Progressive Web App",
  "short_name": "MyPWA",
  "description": "A modern installable Progressive Web Application.",

  "lang": "en",
  "dir": "ltr",

  "start_url": "/?source=pwa",
  "scope": "/",

  "display": "standalone",
  "display_override": [
    "window-controls-overlay",
    "standalone",
    "minimal-ui",
    "browser"
  ],

  "orientation": "portrait",

  "background_color": "#ffffff",
  "theme_color": "#2563eb",

  "categories": [
    "productivity",
    "utilities",
    "education"
  ],

  "iarc_rating_id": "",

  "prefer_related_applications": false,
  "related_applications": [],

  "launch_handler": {
    "client_mode": "navigate-existing"
  },

  "edge_side_panel": {
    "preferred_width": 420
  },

  "protocol_handlers": [
    {
      "protocol": "web+myapp",
      "url": "/open?url=%s"
    }
  ],

  "file_handlers": [
    {
      "action": "/open-file",
      "accept": {
        "text/plain": [".txt"],
        "application/json": [".json"]
      }
    }
  ],

  "shortcuts": [
    {
      "name": "Dashboard",
      "short_name": "Dashboard",
      "description": "Open dashboard",
      "url": "/dashboard",
      "icons": [
        {
          "src": "/icons/dashboard.png",
          "sizes": "96x96"
        }
      ]
    },
    {
      "name": "Settings",
      "url": "/settings",
      "icons": [
        {
          "src": "/icons/settings.png",
          "sizes": "96x96"
        }
      ]
    }
  ],

  "screenshots": [
    {
      "src": "/screenshots/home.png",
      "sizes": "1080x1920",
      "type": "image/png",
      "form_factor": "narrow"
    },
    {
      "src": "/screenshots/desktop.png",
      "sizes": "1920x1080",
      "type": "image/png",
      "form_factor": "wide"
    }
  ],

  "icons": [
    {
      "src": "/icons/icon-72.png",
      "sizes": "72x72",
      "type": "image/png"
    },
    {
      "src": "/icons/icon-96.png",
      "sizes": "96x96",
      "type": "image/png"
    },
    {
      "src": "/icons/icon-128.png",
      "sizes": "128x128",
      "type": "image/png"
    },
    {
      "src": "/icons/icon-144.png",
      "sizes": "144x144",
      "type": "image/png"
    },
    {
      "src": "/icons/icon-152.png",
      "sizes": "152x152",
      "type": "image/png"
    },
    {
      "src": "/icons/icon-192.png",
      "sizes": "192x192",
      "type": "image/png",
      "purpose": "any"
    },
    {
      "src": "/icons/icon-192-maskable.png",
      "sizes": "192x192",
      "type": "image/png",
      "purpose": "maskable"
    },
    {
      "src": "/icons/icon-384.png",
      "sizes": "384x384",
      "type": "image/png"
    },
    {
      "src": "/icons/icon-512.png",
      "sizes": "512x512",
      "type": "image/png",
      "purpose": "any"
    },
    {
      "src": "/icons/icon-512-maskable.png",
      "sizes": "512x512",
      "type": "image/png",
      "purpose": "maskable"
    },
    {
      "src": "/icons/icon.svg",
      "sizes": "any",
      "type": "image/svg+xml"
    }
  ]
}
```

---

## 1. id

شناسه یکتای برنامه هستش و بدون اون بعضی مرورگرها از `start_url` به عنوان شناسه استفاده می‌کنن.

```json
/* Absolute URL */
"id": "https://myapp.example.com/"

/* Relative URL */
"id": "myapp/v2"

/* URL with query parameters */
"id": "myapp?version=2&mode=trial"
```

## 2. name

اسم کامل برنامه:

```json
"name": "My Awesome Progressive Web App"
```

مثلا:
```
Telegram Desktop
```

## 3. short_name

اسم کوتاه برنامه که وقتی جا کمتر بود یا تو گوشی نمایش داده بشه.

```json
"short_name": "MyPWA"
```

## 4. description

توضیحی راجب اپلیکیشن.


## 5. lang

زبان پیش‌فرض برنامه.

```json
"lang": "fa"
```

## 6. dir

جهت متن، مثلا است چین یا چپ چین

```
ltr
rtl
auto
```

## 7. start_url

اولین صفحه‌ای که بعد از نصب باز میشه.

مثلا:

```
"/dashboard"

"/?source=pwa"
```


## 8. scope

مشخص می‌کند چه URLهایی متعلق به برنامه هستند.

مثلا:

```
"/" کل سایت

"https://telegram.org/" چندتا دامنه خاص
"https://telegram.me/"
"https://t.me/"

"https://myapp.example.com/" ساب دامنه

"https://example.com/myapp" یه صفحه توی سایت
```

## 9. display

نحوه نمایش سایت:

```
browser
```

مثل سایت معمولی، صرفا قابلیت کش کردن و آفلاین لود شدن داره.


```
minimal-ui
```

نوار مرورگر باقی میمونه.


```
standalone
```

کاملاً شبیه اپلیکیشن.


```
fullscreen
```

بدون هیچ نواری و تمام صفحه.


## 10. display_override

اولویت حالت‌های نمایش.

اگر مرورگر از یکی پشتیبانی نکند، بعدیشو انتخاب میکنه.

## 11. orientation

افقی یا عمودی بودن اپلیکیشن شما رو اجباری میکنه.

فقط عمودی: portrait
فقط افقی: landscape

## 12. theme_color

رنگ نوار بالا یا کنار برنامه.

## 13. background_color

رنگ پس زمینه صفحه ای که موقع لود اولیه دیده میشه.

## 14. categories

برای مشخص کردن دسته بندی و کاربرد اپلیکیشن شما برای استور ها و اینترنت و جستجوگرها.

```
books
business
education
entertainment
finance
games
health
music
navigation
news
photo
productivity
shopping
social
sports
travel
utilities
weather
```

## 15. icons

آیکون اپلیکیشن با سایز های مختلف رو قرار میدی تا توی هر سیستم آیکون مناسب همون سایز رو استفاده کنه.

## purpose

قالب آیکون هارو مشخص میکنه.

آیکون معمولی: any
آیکون مناسب موبایل: maskable
برای دسکتاپ ها مثل ویندوز و مک و لینوکس: monochrome

## 16. screenshots
اگر داشته باشی توی کروم پنجره نصب حرفه‌ای‌تر می‌شود.

## 17. shortcuts

با نگه داشتن انگشت روی آیکون برنامه اینارو بهت یسری صفحه پیشنهاد میکنه. مثلا:

```
New Chat

Settings

Profile

Dashboard
```

## 18. protocol_handlers

دپ لینک با پرتوکل اختصاصی شما رو به برنامه هدایت میکنه:

```
myapp://segmentquery?key=value&...#hash
```

## 19. file_handlers

به سیستم عامل میگه که برنامه چچه نوع فایل هایی میتونه باز کنه.

مثلا یه تکست ادیتور اینارو میتونه:

```
.txt
.json
.md
.csv
```
یا مثلا یه موزیک پلیر اینارو میتونه:

```
.mp3
.ogg
.aac
.wav
```

## 20. launch_handler

وقتی برنامه از قبل باز هستش و بخوای دوباره بازش کنی مشخص میکنه که همون صفحه استفاده بشه یا صفحه جدید باز بشه یا یه رفتار دیگه نشون بده.

## 21. related_applications

اگر نسخه اندروید یا ویندوز یا مک یا لینوکس جدا داری میتونی پیشنهاد بدی کاربرهای اون سیستم همون نرم افزارش رو نصب کنن،‌ مثل:

```
Google Play
Microsoft Store
App Store
```

## 22. prefer_related_applications

اگه true باشه مرورگر ترجیح میده نسخه نیتیو نصب بشه و اگه false باشه نسخه PWA نصب میشه.

## فیچر‌هایی که توی Manifest نیستند

این فیچر ها به **Service Worker** و APIهای مرورگر وابستن :

* Push Notifications
* Offline Cache
* Background Sync
* Periodic Background Sync
* Web Share Target
* Camera Share
* Badging API
* Window Controls Overlay (نیازمند API تکمیلی)
* Clipboard API
* File System Access API
* Video/Audio Recording
* Screen Wake Lock
* Web Bluetooth
* WebUSB
* Web NFC

## پیشنهاد برای حدکثر سازگاری

* `id`
* `name`
* `short_name`
* `description`
* `lang`
* `dir`
* `start_url`
* `scope`
* `display`
* `display_override`
* `orientation`
* `theme_color`
* `background_color`
* `categories`
* `icons` (به‌ویژه نسخه‌های `maskable`)
* `screenshots`
* `shortcuts`
* `protocol_handlers`
* `file_handlers`
* `launch_handler`
* `related_applications`
