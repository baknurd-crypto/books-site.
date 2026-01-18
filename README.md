# books-site.<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Библиотека 2009</title>
    <style>
        body { background: #121212; color: white; font-family: sans-serif; text-align: center; }
        input { padding: 15px; width: 80%; border-radius: 10px; margin-top: 20px; }
        button { padding: 15px; width: 85%; background: #007bff; color: white; border: none; border-radius: 10px; margin-top: 10px; font-weight: bold; }
        .book { background: #1e1e1e; padding: 15px; border-radius: 15px; margin: 15px; border: 1px solid #333; }
        .read-link { background: #28a745; color: white; padding: 10px; display: block; text-decoration: none; border-radius: 5px; margin-top: 10px; }
    </style>
</head>
<body>
    <h1>Библиотека 2009</h1>
    <input type="text" id="s" placeholder="Напиши название книги...">
    <button onclick="find()">Найти и читать</button>
    <div id="res"></div>

    <script>
        async function find() {
            const q = document.getElementById('s').value;
            const out = document.getElementById('res');
            out.innerHTML = 'Ищу...';
            const res = await fetch(`https://www.googleapis.com/books/v1/volumes?q=intitle:${encodeURIComponent(q)}&langRestrict=ru`);
            const data = await res.json();
            out.innerHTML = '';
            data.items.forEach(i => {
                const info = i.volumeInfo;
                out.innerHTML += `<div class="book">
                    <img src="${info.imageLinks ? info.imageLinks.thumbnail : ''}" width="100">
                    <h3>${info.title}</h3>
                    <a class="read-link" href="${info.previewLink}" target="_blank">ЧИТАТЬ СРАЗУ</a>
                </div>`;
            });
        }
    </script>
</body>
</html>
