# Bahandisation: что загружать в GitHub

Есть два разных варианта. Выбери один.

## Вариант 1: GitHub Pages, чтобы сайт просто открылся

GitHub Pages показывает только статические файлы. Он не запускает backend и не умеет хранить `ROBOFLOW_API_KEY`.

Загружай в корень репозитория содержимое архива `UPLOAD_TO_GITHUB_PAGES_*.zip`:

- `index.html`
- `app.js`
- `styles.css`
- `404.html`
- `.nojekyll`

Важно: файлы должны лежать прямо в корне репозитория, не внутри папки.

Правильно:

```text
repo/
  index.html
  app.js
  styles.css
  404.html
  .nojekyll
```

Неправильно:

```text
repo/
  public/
    index.html
    app.js
    styles.css
```

Настройка GitHub Pages:

1. Открой репозиторий на GitHub.
2. Нажми `Add file` -> `Upload files`.
3. Перетащи файлы из архива, не сам zip.
4. Нажми `Commit changes`.
5. Открой `Settings` -> `Pages`.
6. В `Build and deployment` выбери `Deploy from a branch`.
7. Branch: `main`, Folder: `/root`.
8. Нажми `Save`.
9. Подожди 1-3 минуты и открой ссылку Pages.

Если снова 404:

- проверь, что `index.html` лежит в корне;
- проверь, что выбран branch `main`;
- проверь, что folder стоит `/root`;
- открой ссылку без лишнего пути после имени репозитория.

## Вариант 2: Render/Railway, чтобы работал Roboflow

Для настоящего AI-анализа фото нужен backend. Для этого загружай полный проект из архива `UPLOAD_FULL_NODE_APP_*.zip`.

Внутри должны быть:

- `public/`
- `services/`
- `server.js`
- `package.json`
- `README.md`
- `.env.example`
- `.gitignore`

На хостинге добавь environment variable:

```env
ROBOFLOW_API_KEY=твой_ключ_roboflow
```

Не загружай настоящий API key в GitHub.

Команды для Node-хостинга:

```bash
npm install
npm start
```

Если сайт открывается, но Roboflow не анализирует:

- проверь, что `ROBOFLOW_API_KEY` добавлен в Environment Variables;
- перезапусти deploy после добавления ключа;
- проверь, что backend URL открывается, например `/api/health`.

