---
тип: приложение
тема: Словарь Figma → код — ключевые концепции и их CSS/React-аналоги
статус: to-read
связано: "[[01.4-Контекст-для-дизайнеров]], [[01.5-Как-макет-становится-сайтом]], [[Маршрут-для-дизайнера]]"
---

# Словарь: Figma → код

Большая часть того, что ты делаешь в Figma, существует в CSS и React почти 1:1 — просто другими словами. Этот словарь — мост: видишь концепт из Figma → находишь его аналог в коде. Используй на любом этапе курса как справочник.

> **Зачем.** Дизайнер уже умеет 60–70% того, что делает разработчик при вёрстке: думать в раскладке, токенах, компонентах, состояниях. Не хватает только нотации. Этот словарь сокращает «выучить вёрстку с нуля» до «выучить синтаксис того, что я уже умею».

---

## 1. Раскладка — Auto layout, Frame, Group

| Figma | CSS / HTML | Заметки |
|---|---|---|
| **Frame** (с auto layout) | `<div style="display: flex">` или `<section>` | Frame — универсальный контейнер. В коде это `div`/`section`/`article`/`header`/`footer` с `display: flex` или `display: grid`. |
| **Frame** (без auto layout) | `<div>` с `position: relative` внутри которого позиционируешь элементы абсолютно | Это редкий случай в проде — почти всегда лучше использовать flex/grid. |
| **Group** | `<div>` без специальных стилей | Просто обёртка для группировки. В коде создаётся, только если действительно нужна для группового отступа/класса. |
| **Auto layout horizontal** | `display: flex; flex-direction: row` | По умолчанию `flex-direction` уже `row`, можно не писать. |
| **Auto layout vertical** | `display: flex; flex-direction: column` | — |
| **Auto layout wrap** | `display: flex; flex-wrap: wrap` | Для чипов, тегов, карточек, переносящихся на новую строку. |
| **Auto layout grid** (новый Figma grid) | `display: grid; grid-template-columns: ...` | CSS Grid мощнее Figma-grid, особенно для сложных раскладок. |
| **Spacing between items** (gap) | `gap: 16px` | Один в один. |
| **Padding** (top/right/bottom/left) | `padding: 16px 24px 16px 24px` или `padding: 16px 24px` | В CSS короткая запись: 4 значения = top right bottom left, 2 значения = vertical horizontal. |
| **Distribute: space between** | `justify-content: space-between` | — |
| **Align: center** (по поперечной оси) | `align-items: center` | В flex-row это вертикальное центрирование, в flex-column — горизонтальное. |
| **Align: center** (по основной оси) | `justify-content: center` | — |

---

## 2. Размеры — Fill, Hug, Fixed

| Figma | CSS | Заметки |
|---|---|---|
| **Fill container** (горизонтально, в flex-row) | `flex: 1` или `width: 100%` | `flex: 1` правильнее в flex-контексте — равномерно делит свободное место. |
| **Hug contents** | `width: fit-content` или `width: auto` | Размер по содержимому. По умолчанию у inline-элементов это уже так. |
| **Fixed width: 320** | `width: 320px` | — |
| **Min width / Max width** | `min-width: ...; max-width: ...` | Часто комбинируют: `width: 100%; max-width: 1200px;` — растягивается, но не безгранично. |
| **Constraints** (Top, Right, Bottom, Left, Center, Scale) | `position: absolute; top/right/bottom/left: ...` | Используется, если родитель `position: relative`. В современной вёрстке используют редко — почти всё решается через flex/grid. |

---

## 3. Дизайн-токены — стили в Figma → переменные в коде

| Figma | CSS / Tailwind | Заметки |
|---|---|---|
| **Local style — Color** (`--color-primary` в Figma Variables) | `--color-primary: #3B82F6` (CSS custom property) или `text-primary` (Tailwind) | Переменная, которую можно использовать везде и менять в одном месте. |
| **Local style — Text** (Heading 1, Body M, Caption…) | CSS-классы `.text-h1`, `.text-body-m` или Tailwind `text-2xl font-semibold leading-tight` | В коде токен текста — это набор: `font-size + font-weight + line-height + letter-spacing`. |
| **Effects — Drop shadow** | `box-shadow: 0 4px 12px rgba(0,0,0,0.1)` | Один в один. Inner shadow — `box-shadow: inset ...`. |
| **Effects — Layer blur** | `filter: blur(8px)` | Применяется ко всему элементу. |
| **Effects — Background blur** | `backdrop-filter: blur(12px)` | Замыливает то, что **под** элементом — для glassmorphism. |
| **Spacing scale** (4, 8, 12, 16, 24, 32…) | CSS-переменные `--space-1: 4px` или Tailwind `p-1`, `p-2`, `p-4` | Tailwind по умолчанию идёт по 4px-сетке: `p-1 = 4px, p-2 = 8px, p-4 = 16px`. |
| **Variables (modes)** — light/dark, brand A / brand B | CSS-переменные + класс на `<html>` | Переключается одним классом: `<html class="dark">` → `--color-bg: #000` вместо `#fff`. |

---

## 4. Компоненты — Component, Variant, Property

| Figma | React | Заметки |
|---|---|---|
| **Component** (мастер-компонент) | `function Button(props) { ... }` | React-компонент — это функция, которая возвращает разметку. Мастер-компонент в Figma — её визуальное определение. |
| **Instance** (использование компонента) | `<Button />` в JSX | Каждый раз, когда ты вставляешь компонент в макет — это `<Button />` в коде. |
| **Component property — Variant** (Primary / Secondary / Tertiary) | `<Button variant="primary" />` (string-проп) | Variant в Figma = string-property в React. |
| **Component property — Boolean** (icon: on/off) | `<Button hasIcon={true} />` | Boolean-проп. |
| **Component property — Instance swap** | `<Button icon={<HeartIcon />} />` | В JSX можно передать другой компонент через проп. |
| **Component property — Text** | `<Button label="Купить" />` или `<Button>Купить</Button>` | Текст передаётся пропом или children. |
| **Override** (переопределение в инстансе) | Пропы при вызове компонента | Каждое использование `<Button>` может переопределить любые пропы. |
| **Detached instance** | Inline-разметка вместо переиспользования компонента | Когда что-то «отвязали от компонента» в Figma — в коде это просто div со стилями, не компонент. |

---

## 5. Состояния — интерактивные prototypes → CSS pseudo-classes / React state

| Figma | CSS / React | Заметки |
|---|---|---|
| **Default state** | базовые стили элемента | — |
| **Hover state** в prototype | `:hover` псевдо-класс | `button:hover { background: ... }` |
| **Pressed / Active state** | `:active` псевдо-класс | Применяется только во время клика. |
| **Focused state** | `:focus` или `:focus-visible` | `:focus-visible` показывает обводку только при навигации с клавиатуры — это правильнее для аксессибилити. |
| **Disabled state** | атрибут `disabled` + CSS-селектор `[disabled]` или `:disabled` | `<button disabled>`. |
| **Selected / Active in toggle** | React state (`useState`) + условный класс | Не CSS-only — нужно JavaScript состояние. |
| **Loading state** | React state + условный рендер | Тоже на React, не на CSS. |

---

## 6. Адаптив — Constraints / Breakpoints в Figma → media queries / container queries

| Figma | CSS | Заметки |
|---|---|---|
| **Frame размером 1440** (десктоп) | `@media (min-width: 1440px) { ... }` или `lg:`/`xl:` в Tailwind | Десктопный размер обычно — базовое состояние. |
| **Frame размером 768** (планшет) | `@media (min-width: 768px)` или `md:` | — |
| **Frame размером 375** (мобайл) | базовое состояние + `@media (max-width: 767px)` или mobile-first без media query | Современная практика — mobile-first: пишешь стили для мобилки, потом добавляешь `md:`/`lg:` для бóльших экранов. |
| **Constraints: Scale** (растягивается с фреймом) | `width: 100%` + флекс/грид | — |
| **Constraints: Left & Right** (прижат к обоим краям) | `width: auto` в потоке flex / `left: 0; right: 0` в absolute | — |

---

## 7. Прочее — мелочи, которые часто всплывают

| Figma | CSS | Заметки |
|---|---|---|
| **Stroke** (обводка) | `border: 1px solid #...` или `outline: ...` | Border занимает место в раскладке (если нет `box-sizing: border-box`), outline — нет. |
| **Corner radius** | `border-radius: 8px` | Можно по углам отдельно: `border-radius: 8px 0 8px 0`. |
| **Mask / Clip with shape** | `clip-path: ...` или `mask-image: ...` | Сложнее, чем в Figma — обычно нужны конкретные SVG-формы. |
| **Image fill — Fill / Fit / Crop** | `object-fit: cover / contain / none` | `cover` обрезает по аспект-рейтио; `contain` вписывает с полями. |
| **Anchor link** в prototype | `<a href="#section">` + `id="section"` на цели | — |
| **Fixed position в prototype** (sticky-хедер) | `position: sticky` или `position: fixed` | `sticky` прилипает только пока виден родитель; `fixed` — всегда. |
| **Dropdown / Tooltip / Modal в prototype** | React-компонент + state + `position: absolute` или library (Radix UI, headless-ui) | На вёрстку обычно берут готовую библиотеку компонентов — самому делать выпадающие меню с правильным аксессибилити сложно. |
| **Auto layout: ignore / absolute position** | `position: absolute` внутри `position: relative`-родителя | Используется для значков «1» на иконках уведомлений, badges, наклеек. |

---

## Обратное направление — если разработчик сказал слово, а ты не знаешь, что это

| Слово разработчика | На языке Figma |
|---|---|
| Flexbox | Auto layout |
| Grid | Auto layout grid (новый) или ручная сетка из направляющих |
| `gap` | Spacing between items в auto layout |
| `padding` | Padding в auto layout |
| `margin` | Между двумя элементами без auto layout — отступ вручную |
| Селектор / класс | Имя стиля или компонента |
| CSS variable / token | Local style / Variable в Figma |
| Component | Мастер-компонент |
| Props | Component properties |
| State | Состояние в prototype (hover/pressed/...) |
| Pseudo-class (`:hover`) | Hover-state в prototype |
| Media query / breakpoint | Разные frames для desktop/tablet/mobile |
| `position: absolute` | Constraints в Figma |
| `z-index` | Layer order — слой выше в панели Layers |
| `box-shadow` | Effect: drop shadow |
| `border-radius` | Corner radius |
| `object-fit: cover` | Image fill: Fill |
| Container query | Этого в Figma пока нет — экспериментальный CSS |

---

## Где это пригодится в курсе

- [[01.5-Как-макет-становится-сайтом]] — общий обзор, как Figma превращается в код. Этот словарь — справочник к нему.
- Модуль 03 (CSS база) — большая часть таблицы про раскладку и размеры применяется здесь.
- Модуль 04 (CSS продвинутый) — таблица дизайн-токенов и переменных пригодится в уроке про CSS custom properties и Tailwind.
- Модуль 09 (React база) — таблица компонентов и пропсов применяется при чтении первых React-уроков.

Возвращайся к этой странице, когда видишь незнакомый термин — почти наверняка ты уже знаешь концепт из Figma, нужно только сопоставить.
