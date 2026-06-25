<%*
const rawUrl = await tp.system.prompt("Вставь YouTube-ссылку");

function getYouTubeId(input) {
  if (!input) return "";
  const value = input.trim();
  const patterns = [
    /(?:youtube\.com\/watch\?v=)([A-Za-z0-9_-]{11})/,
    /(?:youtu\.be\/)([A-Za-z0-9_-]{11})/,
    /(?:youtube\.com\/embed\/)([A-Za-z0-9_-]{11})/,
    /(?:youtube\.com\/shorts\/)([A-Za-z0-9_-]{11})/,
  ];

  for (const pattern of patterns) {
    const match = value.match(pattern);
    if (match) return match[1];
  }

  return value.match(/^[A-Za-z0-9_-]{11}$/) ? value : "";
}

const videoId = getYouTubeId(rawUrl);

if (!videoId) {
  new Notice("Не смог распознать YouTube-ссылку");
  tR += rawUrl || "";
} else {
  const watchUrl = `https://www.youtube.com/watch?v=${videoId}`;
  const embedUrl = `https://www.youtube.com/embed/${videoId}`;
  const thumbUrl = `https://img.youtube.com/vi/${videoId}/hqdefault.jpg`;
  const today = tp.date.now("YYYY-MM-DD");

  tR += `## YouTube Source

<div class="youtube-learning-card">
  <a class="youtube-learning-thumb" href="${watchUrl}">
    <img src="${thumbUrl}" alt="YouTube preview">
  </a>
  <iframe src="${embedUrl}" title="YouTube video" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share; fullscreen" allowfullscreen></iframe>
</div>

> [!info] Источник
> Ссылка: ${watchUrl}  
> Добавлено: ${today}

## Быстрый Конспект

> [!summary] Запомнить
> Короткая выжимка видео появится здесь после обработки AI.

**Главное:**

- 

**Практика после видео:**

- [ ] 

## Transcript

> [!workflow] Как использовать
> 1. Вставь ссылку выше или выдели её.
> 2. Запусти свой \`Ytranscript plugin.\`
> 3. Вставь транскрипт ниже.
> 4. Потом попроси AI: \`вытащи идеи без воды и сравни с моим vault\`.

Вставь транскрипт здесь:


## Идеи Без Воды

> [!ai] AI extraction
> Главные мысли, которые реально стоит оставить в Obsidian.

- 

## Что Применить На Практике

- [ ] 

## Термины

| Термин | Простое объяснение |
| --- | --- |
|  |  |

## Связанные Заметки

- [[Home]]
`;
}
%>
