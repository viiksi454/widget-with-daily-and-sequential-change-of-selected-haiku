---
cssclasses:
    - haiku
---
```dataviewjs

// Конфигурация
const FOLDER = "test";

// Функция для генерации seed
function getDailySeed(date) {
    const dateStr = date.toISOString().split('T')[0];
    let hash = 0;
    for (let i = 0; i < dateStr.length; i++) {
        hash = ((hash << 5) - hash) + dateStr.charCodeAt(i);
        hash |= 0;
    }
    return Math.abs(hash);
}

// Получаем хокку
const allHaiku = dv.pages(`"${FOLDER}"`)
    .where(p => p.author && p.kanji && p.line1 && p.line2 && p.line3)
    .sort(p => p.file.name);

const today = new Date();
const dailyIndex = getDailySeed(today) % allHaiku.length;
let currentHaiku = allHaiku[dailyIndex];

// Создаем контейнер
const container = dv.el('div', '', { cls: 'haiku-widget' });

// Добавляем текст хокку
container.appendChild(dv.el('div', `**${currentHaiku.kanji}**`, { cls: 'kanji' }));

container.appendChild(dv.el('div', `*${currentHaiku.transcription}*`, { cls: 'transcription' }));

container.appendChild(dv.el('hr', '', { cls: 'divider' }));

[1, 2, 3].forEach(line => {
    container.appendChild(dv.el('div', currentHaiku[`line${line}`], { cls: 'line' }));
});

container.appendChild(dv.el('div', `— ${currentHaiku.author}`, { cls: 'author' }));

// Кнопка для смены хокку
const button = dv.el('button', '俳句へ進む', {
    cls: 'next-button',
    onclick: async () => {
        // Добавляем анимацию исчезновения
        container.style.opacity = '0';
        container.style.transition = 'opacity 0.3s ease';
        
        // Ждём завершения анимации
        await new Promise(resolve => setTimeout(resolve, 300));
        
        // Получаем текущий индекс
        const currentIndex = allHaiku.indexOf(currentHaiku);
        
        // Вычисляем следующий индекс с проверкой на границы массива
        const newIndex = (currentIndex + 1) >= allHaiku.length ? 0 : currentIndex + 1;
        
        // Обновляем текущее хокку
        currentHaiku = allHaiku[newIndex];
        
        // Полностью пересоздаём содержимое
        container.innerHTML = '';
        
        // Добавляем текст хокку (повторяем структуру)
        container.appendChild(dv.el('div', `**${currentHaiku.kanji}**`, { cls: 'kanji' }));
        container.appendChild(dv.el('div', `*${currentHaiku.transcription}*`, { cls: 'transcription' }));
        container.appendChild(dv.el('hr', '', { cls: 'divider' }));
        
        [1, 2, 3].forEach(line => {
            container.appendChild(dv.el('div', currentHaiku[`line${line}`], { cls: 'line' }));
        });
        
        container.appendChild(dv.el('div', `— ${currentHaiku.author}`, { cls: 'author' }));
        container.appendChild(button); // Добавляем кнопку обратно
        
        // Анимация появления
        container.style.opacity = '0';
        setTimeout(() => {
            container.style.opacity = '1';
        }, 10);
        
        // Сохраняем последнее показанное хокку в localStorage
        window.localStorage.setItem('lastHaikuIndex', newIndex);
    }
});

container.appendChild(button);

```