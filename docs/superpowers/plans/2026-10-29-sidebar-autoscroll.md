# План реализации: Умный автоскролл левой панели и интерактивный трекер чтения

> **Назначение:** Синхронизация прокрутки оглавления в сайдбаре с чтением статьи на сайте «Библия Параноика» (`site/index.html`), устранение зависания панели и добавление быстрого возврата фокуса.  
> **Спецификация:** `docs/superpowers/specs/2026-10-29-sidebar-autoscroll-design.md`

---

## 1. Описание задачи и архитектурный подход

- **Проблема:** При прокрутке статьи вниз активная глава (например, 53) отмечается в заголовке сайдбара, но список ссылок не прокручивается, и активная ссылка остаётся за пределами видимости (скрыта внизу). Причина — агрессивный `Hover Lock` (`isSidebarHovered = true`), блокирующий скролл при любом нахождении мыши над панелью, и ненадежные формулы смещения `getBoundingClientRect`.
- **Решение:**
  1. Заменить устаревший механизм `revealInNav` на детерминированный алгоритм центрирования на базе `offsetTop` относительно контейнера прокрутки (`.sidebar-nav`).
  2. Убрать блокировку по пассивному наведению мыши (`mouseenter`/`mouseleave`). Отслеживать только активную ручную прокрутку колесиком (`wheel`) или касанием (`touchmove`), уступая пользователю на 2.5 секунды, после чего автоматически возвращать плавное следование за чтением.
  3. Сделать бейдж `.sidebar-current` («Чтение: [Глава]») вверху сайдбара интерактивным: при клике панель моментально и плавно центрирует текущую главу с мягким акцентным пульсом.
  4. Обновить Service Worker (`site/sw.js`) и зафиксировать изменения в git-репозитории на GitHub.

---

## 2. Предлагаемые изменения по компонентам

### Component 1: Стили сайдбара и интерактивного бейджа (`site/index.html`)
- Добавить стили курсора, фокуса, ховера и анимации пульсации для `.sidebar-current`:
```css
.sidebar-current {
    cursor: pointer;
    transition: border-color 0.15s ease, background-color 0.15s ease, transform 0.1s ease;
    user-select: none;
}
.sidebar-current:hover {
    border-color: var(--color-accent);
    background: var(--color-panel);
}
.sidebar-current:active {
    transform: scale(0.98);
}
.sidebar-current:focus-visible {
    outline: 2px solid var(--color-accent);
    outline-offset: 2px;
}
.sidebar-nav .nav-link.pulse-highlight {
    animation: navPulse 1.2s ease-out;
}
@keyframes navPulse {
    0% { background: var(--color-accent-dim-hover); box-shadow: 0 0 12px var(--color-accent); }
    100% { background: var(--color-accent-dim); box-shadow: none; }
}
```

### Component 2: Модуль навигации (Modern Navigation Engine в `site/index.html`)
- **Удаление Hover Lock:** Удалить `mouseenter` / `mouseleave` слушатели, которые ложно блокировали автоскролл.
- **Детектор ручного вмешательства:** Использовать флаг `isUserScrollingNav` только при событиях `wheel` и `touchmove` внутри панели с таймером сброса 2500 мс.
- **Новая функция `revealInNav`:**
```javascript
function revealInNav(targetNav, linkEl, force) {
    if (!targetNav || !linkEl) return;
    if (targetNav.scrollHeight <= targetNav.clientHeight + 4) return;

    var navScrollTop = targetNav.scrollTop;
    var navClientHeight = targetNav.clientHeight;
    
    // Положение ссылки относительно содержимого контейнера
    var linkRelativeTop = linkEl.offsetTop - targetNav.offsetTop;
    var linkHeight = linkEl.offsetHeight || 32;

    // Комфортные границы (25% сверху и снизу)
    var comfortTop = navScrollTop + (navClientHeight * 0.25);
    var comfortBottom = navScrollTop + navClientHeight - (navClientHeight * 0.25) - linkHeight;

    // Если требуется принудительное центрирование или ссылка вышла за зону комфорта
    if (force || linkRelativeTop < comfortTop || linkRelativeTop > comfortBottom) {
        var targetCenter = linkRelativeTop - (navClientHeight / 2) + (linkHeight / 2);
        var prefersReduced = window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches;
        targetNav.scrollTo({
            top: Math.max(0, targetCenter),
            behavior: (prefersReduced || force === 'instant') ? 'auto' : 'smooth'
        });
    }
}
```
- **Слушатель клика на `.sidebar-current`:**
  - При клике на индикатор текущей главы вызывается `revealActive(currentActiveId, true)`.
  - Активная ссылка получает класс `pulse-highlight` на 1.2 секунды для мгновенной ориентации взгляда.

### Component 3: Service Worker (`site/sw.js`)
- Повышение версии кэша `CACHE_NAME` до `'paranoid-bible-v15'`.

---

## 3. План тестирования и верификации

### Автоматизированная проверка
1. Проверка синтаксиса JavaScript через Node.js:
   ```bash
   node scratch/verify_scripts_v10.js
   node -c site/sw.js
   ```
2. Проверка баланса парных HTML-тегов:
   ```bash
   python scratch/check_all_tags.py
   ```
3. Проверка логики позиционирования ссылок (эмуляция расчетов смещения в `scratch/test_autoscroll.py`).

### Ручная проверка в браузере
1. Открыть `site/index.html` и прокручивать страницу от главы 1 вниз до главы 50, 53, 100 и 153.
2. Убедиться, что активная ссылка в левой панели плавно подтягивается и всегда находится в центральной части сайдбара.
3. Прокрутить колесико мыши внутри сайдбара вручную на другие главы — убедиться, что автоскролл уступает читателю на 2.5 секунды.
4. Кликнуть по плашке «Чтение: [Глава]» вверху сайдбара — убедиться, что список мгновенно плавно центрирует текущую читаемую главу и подсвечивает её пульсирующей анимацией.

---

## 4. Git и релиз
- Создание коммита с подробным описанием:
  `feat: add smart centering auto-scroll to sidebar and clickable tracker button`
- Отправка в удаленный репозиторий `origin/main` на GitHub.
