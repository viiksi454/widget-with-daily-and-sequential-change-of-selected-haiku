# Виджет для оформления базы японской поэзии.
![note_img](https://github.com/viiksi454/widget-with-daily-and-sequential-change-of-selected-haiku/blob/main/note_img.jpeg)
>Виджет может быть использован для оформления страниц тематической базы-сборника японской поэзии.
### Возможности:
- Ежедневная автоматическая смена контента
- Смена контента по кнопке
- Настраиваемый вид _[.css](https://github.com/viiksi454/widget-with-daily-and-sequential-change-of-selected-haiku/blob/main/haiku.css)_
### В основе:
- Код _dataviewjs_, осуществляющий поиск заметок, созданных по специальному формату, в определённой директории и собирающий из них необходимый контент для демонстрации.
  - [Пример кода фронтматтера заметки](https://github.com/viiksi454/widget-with-daily-and-sequential-change-of-selected-haiku/blob/main/note%20frontmatter)
### Отображение:
- Канджи хоку
- Транскрипция (на английском языке)
- Текст стихотворения
- Автор 
### Обязательные условия функционирования:
- Отдельная директория с заметками (Например: директория task; в ней находятся заметка1.md, заметка2.md ... заметка5.md и т.д.)
- Особенный формат заметок (все данные для отображения содежражтся во фронтматтере; заметка не имеет текста)
  - [Пример оформления заметки](https://github.com/viiksi454/widget-with-daily-and-sequential-change-of-selected-haiku/blob/main/%D0%B2%D0%B5%D1%81%D0%B5%D0%BD%D0%BD%D0%B5%D0%B5%20%D0%BC%D0%BE%D1%80%D0%B5.md)
>### Установка:
- **Размещение кода на странице заметки**. Создайте заметку с фронтматтером по шаблону.
- **Подключение _.css_ в свойстве _cssclasses_ фронтматтера**. В директорию _Snippets_ хранилища поместите файл _.css_ и подключите его (Настройки - Оформление - Фрагменты css кода - включиь - обновить).
---
### Работа виджета
![widget_work](https://github.com/viiksi454/widget-with-daily-and-sequential-change-of-selected-haiku/blob/main/widget_work.gif)
