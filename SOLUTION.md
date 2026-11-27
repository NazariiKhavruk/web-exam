# Білет № 2 - Вибір змін для коміту

**Вхідні дані:** у репозиторії `web-exam` поточна гілка `main`, `origin` і відстеження `origin/main` налаштовано.
Зміни в `index.html` і `style.css` не додано до індексу. `notes.txt` помилково додано до індексу,
але файл треба зберегти на комп'ютері. Віддалених змін немає.

## 1. Перевірка стану репозиторію та перегляд змін

```bash
git status
git diff index.html style.css
```

- `git status` - показує, що `notes.txt` в індексі (`new file`), а `index.html` і `style.css` змінені, але не в індексі.
- `git diff index.html style.css` - показує незбережені в індексі зміни в цих двох файлах.

## 2. Вилучення notes.txt з індексу і додавання index.html, style.css

```bash
git restore --staged notes.txt
git add index.html style.css
```

- `git restore --staged notes.txt` - прибирає файл тільки з індексу, сам файл лишається в робочій папці
  (альтернатива: `git rm --cached notes.txt`).
- `git add index.html style.css` - додає до індексу лише потрібні файли.

## 3. Список підготовлених файлів і коміт

```bash
git diff --cached --name-only
git commit -m "Update page styles"
```

- `git diff --cached --name-only` - виводить список файлів в індексі: `index.html`, `style.css`
  (можна також `git status`).
- `git commit -m "Update page styles"` - створює коміт лише з цими двома файлами.

## 4. Надсилання на GitHub і повторна перевірка

```bash
git push origin main
git status
```

- `git push origin main` - надсилає коміт у віддалений репозиторій.
- `git status` - підтверджує результат.

## Результат

```text
$ git status
On branch main
Your branch is up to date with 'origin/main'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	notes.txt

nothing added to commit but untracked files present (use "git add" to track)

$ git log -1 --format=%s --stat
Update page styles

 index.html |  1 +
 style.css  | 10 +++++++++-
 2 files changed, 10 insertions(+), 1 deletion(-)
```

- Коміт `Update page styles` містить зміни лише в `index.html` і `style.css`.
- Гілка `main` синхронізована з `origin/main`.
- `notes.txt` лишився в робочій папці і відображається як невідстежуваний файл.

## Повна послідовність команд

```bash
git status
git diff index.html style.css
git restore --staged notes.txt
git add index.html style.css
git diff --cached --name-only
git commit -m "Update page styles"
git push origin main
git status
```
