# FRONTEND MANIFEST & TECHNICAL STANDARDS

Этот документ определяет технический стандарт для генерации кода в рамках AI Landing Pipeline.

## 1. PROJECT STRUCTURE (File Organization)
Все файлы финальной сборки должны находиться в директории `code/`.

```text
code/
├── index.html          # Главный файл (Entry Point). Содержит HTML, CSS (Tailwind) и JS.
├── MANIFEST.md         # Этот документ (Технические стандарты).
└── assets/             # Папка для статических ресурсов.
    ├── images/         # Изображения (логотипы, фото товаров).
    │   └── placeholder.png
    └── css/            # (Опционально) Кастомные стили, если Tailwind недостаточно.
```

**Правила именования:**
*   Файлы и папки: `kebab-case` (например, `my-landing-page.html`, `main-banner.jpg`).
*   HTML ID и классы: `kebab-case`.
*   JS переменные: `camelCase`.

## 2. TECHNOLOGY STACK
*   **Core:** HTML5 (Semantic).
*   **Styling:** Tailwind CSS (via CDN for MVP).
*   **Logic:** Vanilla JavaScript (ES6+).
*   **Format:** Single File Output (`index.html`). Весь CSS и JS должен быть внутри этого файла (для удобства передачи клиенту на этапе прототипа).

## 3. EXTERNAL RESOURCES (CDNs)

### Tailwind CSS
Использовать скрипт-тег для подключения и конфигурации:
```html
<script src="https://cdn.tailwindcss.com"></script>
<script>
    tailwind.config = {
      theme: {
        extend: {
          colors: { 
            /* Значения брать строго из design.md */ 
          },
          fontFamily: {
             /* Значения брать строго из design.md */ 
          }
        }
      }
    }
</script>
```

### Fonts
*   Только **Google Fonts**.
*   Подключать через `<link rel="preconnect">` и `<link href="...">`.

### Icons
*   Использовать **FontAwesome Free** (CDN).
*   Ссылка: `<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">`
*   Использование: `<i class="fa-solid fa-check text-primary"></i>`

### Images / Placeholders
*   На этапе прототипа использовать сервис **placehold.co**.
*   Формат URL: `https://placehold.co/{WIDTH}x{HEIGHT}/{BG_COLOR_HEX}/{TEXT_COLOR_HEX}?text={TEXT}`
*   Пример: `https://placehold.co/600x400/D97706/FFFFFF?text=Product+Image` (Цвета брать из дизайн-системы!).
*   В будущем: реальные картинки класть в `assets/images/` и ссылаться как `./assets/images/filename.jpg`.

## 4. CODING GUIDELINES

### Structure
1.  `<!DOCTYPE html>`
2.  `<html lang="ru" class="scroll-smooth">` (Плавный скролл обязателен).
3.  `<head>`: Meta tags, Title, CDNs, Tailwind Config.
4.  `<body>`:
    *   `<header>` (Fixed/Sticky). Обязательно наличие мобильного меню (Burger).
    *   `<main>`:
        *   `<section id="...">`: Каждая логическая часть лендинга.
    *   `<footer>`.
    *   `<script>`: Логика (мобильное меню, аккордеоны, модалки).

### Responsiveness (Mobile First)
*   Никаких медиа-запросов в `<style>`. Только классы Tailwind.
*   Верстаем сначала для мобильного.
*   Расширяем для десктопа через префиксы `md:`, `lg:`.
*   Пример сетки: `grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3`.

### Interactive Elements
*   **Mobile Menu:** Обязательно для адаптива. Реализовать на чистом JS (toggle class `hidden`).
*   **FAQ:** Использовать нативный тег `<details>` и `<summary>` (стилизовать через Tailwind group-open).
*   **Buttons:** Должны иметь состояние `:hover` и `transition`.

### SEO (Minimum viable)
*   `title` и `meta name="description"` должны отражать оффер (из `sources/analysis.md`).
*   Добавить базовые OpenGraph теги: `og:title`, `og:description`, `og:image` (можно плейсхолдер на этапе прототипа).

## 5. QUALITY ASSURANCE
*   Проверить контрастность текста.
*   Все картинки должны иметь `alt`.
*   Все ссылки в меню должны вести на соответствующие `id` секций.
*   Интерактивные элементы (меню/кнопки) должны иметь `aria-*` где уместно и заметный `focus`-стиль.
