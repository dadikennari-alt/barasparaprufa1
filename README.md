<!DOCTYPE html>
<html lang="is">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Orðaspjöld - Stafurinn Þ</title>
    <style>
        :root {
            --primary-color: #2c3e50;
            --bg-color: #f4f7f6;
            --card-bg: #ffffff;
            --shadow: 0 4px 6px rgba(0,0,0,0.1);
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg-color);
            margin: 0;
            padding: 20px;
            color: var(--primary-color);
        }

        h1 {
            text-align: center;
            font-size: 2.5rem;
            margin-bottom: 30px;
            color: #2980b9;
        }

        .grid-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
            gap: 25px;
            max-width: 1200px;
            margin: 0 auto;
        }

        .card {
            background-color: var(--card-bg);
            border-radius: 15px;
            overflow: hidden;
            box-shadow: var(--shadow);
            transition: transform 0.3s ease;
            display: flex;
            flex-direction: column;
        }

        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 15px rgba(0,0,0,0.15);
        }

        .card img {
            width: 100%;
            height: 220px;
            object-fit: cover;
            border-bottom: 3px solid #3498db;
        }

        .icelandic-word {
            font-size: 2.5rem;
            font-weight: bold;
            text-align: center;
            padding: 15px 10px;
            margin: 0;
            background-color: #ecf0f1;
            color: #2c3e50;
            border-bottom: 1px solid #ddd;
        }

        .translations {
            padding: 15px;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            flex-grow: 1;
        }

        .translation-item {
            font-size: 1rem;
            display: flex;
            align-items: center;
            gap: 8px;
            padding: 5px 0;
        }

        .emoji {
            font-size: 1.2rem;
        }

        /* Responsive adjustments */
        @media (max-width: 600px) {
            .translations {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>

    <h1>Íslenskur Orðaforði - Stafurinn Þ</h1>
    <div class="grid-container" id="flashcards"></div>

    <script>
        const wordsData = [
            {
                is: "Þak", img: "thak.jpg",
                translations: [
                    { lang: "Enska", flag: "🇬🇧", word: "Roof" },
                    { lang: "Spænska", flag: "🇪🇸", word: "Techo" },
                    { lang: "Arabíska", flag: "🇸🇦", word: "سقف" },
                    { lang: "Víetnamska", flag: "🇻🇳", word: "Mái nhà" },
                    { lang: "Portúgalska", flag: "🇵🇹", word: "Telhado" },
                    { lang: "Pólska", flag: "🇵🇱", word: "Dach" },
                    { lang: "Persneska", flag: "🇮🇷", word: "سقف" },
                    { lang: "Úkraínska", flag: "🇺🇦", word: "Дах" },
                    { lang: "Rússneska", flag: "🇷🇺", word: "Крыша" }
                ]
            },
            {
                is: "Þari", img: "thari.jpg",
                translations: [
                    { lang: "Enska", flag: "🇬🇧", word: "Seaweed" },
                    { lang: "Spænska", flag: "🇪🇸", word: "Algas" },
                    { lang: "Arabíska", flag: "🇸🇦", word: "أعشاب بحرية" },
                    { lang: "Víetnamska", flag: "🇻🇳", word: "Rong biển" },
                    { lang: "Portúgalska", flag: "🇵🇹", word: "Algas marinhas" },
                    { lang: "Pólska", flag: "🇵🇱", word: "Wodorosty" },
                    { lang: "Persneska", flag: "🇮🇷", word: "جلبک دریایی" },
                    { lang: "Úkraínska", flag: "🇺🇦", word: "Водорості" },
                    { lang: "Rússneska", flag: "🇷🇺", word: "Водоросли" }
                ]
            },
            {
                is: "Þeytari", img: "theytari.jpg",
                translations: [
                    { lang: "Enska", flag: "🇬🇧", word: "Mixer" },
                    { lang: "Spænska", flag: "🇪🇸", word: "Batidora" },
                    { lang: "Arabíska", flag: "🇸🇦", word: "خلاط" },
                    { lang: "Víetnamska", flag: "🇻🇳", word: "Máy đánh trứng" },
                    { lang: "Portúgalska", flag: "🇵🇹", word: "Batedeira" },
                    { lang: "Pólska", flag: "🇵🇱", word: "Mikser" },
                    { lang: "Persneska", flag: "🇮🇷", word: "همزن" },
                    { lang: "Úkraínska", flag: "🇺🇦", word: "Міксер" },
                    { lang: "Rússneska", flag: "🇷🇺", word: "Миксер" }
                ]
            },
            {
                is: "Þorp", img: "thorp.jpg",
                translations: [
                    { lang: "Enska", flag: "🇬🇧", word: "Village" },
                    { lang: "Spænska", flag: "🇪🇸", word: "Pueblo" },
                    { lang: "Arabíska", flag: "🇸🇦", word: "قرية" },
                    { lang: "Víetnamska", flag: "🇻🇳", word: "Ngôi làng" },
                    { lang: "Portúgalska", flag: "🇵🇹", word: "Aldeia" },
                    { lang: "Pólska", flag: "🇵🇱", word: "Wioska" },
                    { lang: "Persneska", flag: "🇮🇷", word: "روستا" },
                    { lang: "Úkraínska", flag: "🇺🇦", word: "Село" },
                    { lang: "Rússneska", flag: "🇷🇺", word: "Деревня" }
                ]
            },
            {
                is: "Þorskur", img: "thorskur.jpg",
                translations: [
                    { lang: "Enska", flag: "🇬🇧", word: "Cod" },
                    { lang: "Spænska", flag: "🇪🇸", word: "Bacalao" },
                    { lang: "Arabíska", flag: "🇸🇦", word: "سمك القد" },
                    { lang: "Víetnamska", flag: "🇻🇳", word: "Cá tuyết" },
                    { lang: "Portúgalska", flag: "🇵🇹", word: "Bacalhau" },
                    { lang: "Pólska", flag: "🇵🇱", word: "Dorsz" },
                    { lang: "Persneska", flag: "🇮🇷", word: "ماهی کاد" },
                    { lang: "Úkraínska", flag: "🇺🇦", word: "Тріска" },
                    { lang: "Rússneska", flag: "🇷🇺", word: "Треска" }
                ]
            },
            {
                is: "Þota", img: "thota.jpg",
                translations: [
                    { lang: "Enska", flag: "🇬🇧", word: "Jet" },
                    { lang: "Spænska", flag: "🇪🇸", word: "Avión" },
                    { lang: "Arabíska", flag: "🇸🇦", word: "طائرة نفاثة" },
                    { lang: "Víetnamska", flag: "🇻🇳", word: "Máy bay phản lực" },
                    { lang: "Portúgalska", flag: "🇵🇹", word: "Jato" },
                    { lang: "Pólska", flag: "🇵🇱", word: "Odrzutowiec" },
                    { lang: "Persneska", flag: "🇮🇷", word: "جت" },
                    { lang: "Úkraínska", flag: "🇺🇦", word: "Реактивний літак" },
                    { lang: "Rússneska", flag: "🇷🇺", word: "Реактивный самолет" }
                ]
            },
            {
                is: "Þumall", img: "thumall.jpg",
                translations: [
                    { lang: "Enska", flag: "🇬🇧", word: "Thumb" },
                    { lang: "Spænska", flag: "🇪🇸", word: "Pulgar" },
                    { lang: "Arabíska", flag: "🇸🇦", word: "إبهام" },
                    { lang: "Víetnamska", flag: "🇻🇳", word: "Ngón cái" },
                    { lang: "Portúgalska", flag: "🇵🇹", word: "Polegar" },
                    { lang: "Pólska", flag: "🇵🇱", word: "Kciuk" },
                    { lang: "Persneska", flag: "🇮🇷", word: "شست" },
                    { lang: "Úkraínska", flag: "🇺🇦", word: "Великий палець" },
                    { lang: "Rússneska", flag: "🇷🇺", word: "Большой палец" }
                ]
            },
            {
                is: "Þúfur", img: "thufur.jpg",
                translations: [
                    { lang: "Enska", flag: "🇬🇧", word: "Tussocks" },
                    { lang: "Spænska", flag: "🇪🇸", word: "Matas" },
                    { lang: "Arabíska", flag: "🇸🇦", word: "خصلات عشب" },
                    { lang: "Víetnamska", flag: "🇻🇳", word: "Bụi cỏ" },
                    { lang: "Portúgalska", flag: "🇵🇹", word: "Tufos" },
                    { lang: "Pólska", flag: "🇵🇱", word: "Kępy" },
                    { lang: "Persneska", flag: "🇮🇷", word: "کلاف‌های چمن" },
                    { lang: "Úkraínska", flag: "🇺🇦", word: "Купини" },
                    { lang: "Rússneska", flag: "🇷🇺", word: "Кочки" }
                ]
            },
            {
                is: "Þyrla", img: "thyrla.jpg",
                translations: [
                    { lang: "Enska", flag: "🇬🇧", word: "Helicopter" },
                    { lang: "Spænska", flag: "🇪🇸", word: "Helicóptero" },
                    { lang: "Arabíska", flag: "🇸🇦", word: "مروحية" },
                    { lang: "Víetnamska", flag: "🇻🇳", word: "Trực thăng" },
                    { lang: "Portúgalska", flag: "🇵🇹", word: "Helicóptero" },
                    { lang: "Pólska", flag: "🇵🇱", word: "Helikopter" },
                    { lang: "Persneska", flag: "🇮🇷", word: "هلیکوپتر" },
                    { lang: "Úkraínska", flag: "🇺🇦", word: "Вертоліт" },
                    { lang: "Rússneska", flag: "🇷🇺", word: "Вертолет" }
                ]
            },
            {
                is: "Þúsund", img: "thusund.jpg",
                translations: [
                    { lang: "Enska", flag: "🇬🇧", word: "Thousand" },
                    { lang: "Spænska", flag: "🇪🇸", word: "Mil" },
                    { lang: "Arabíska", flag: "🇸🇦", word: "ألف" },
                    { lang: "Víetnamska", flag: "🇻🇳", word: "Một nghìn" },
                    { lang: "Portúgalska", flag: "🇵🇹", word: "Mil" },
                    { lang: "Pólska", flag: "🇵🇱", word: "Tysiąc" },
                    { lang: "Persneska", flag: "🇮🇷", word: "هزار" },
                    { lang: "Úkraínska", flag: "🇺🇦", word: "Тисяча" },
                    { lang: "Rússneska", flag: "🇷🇺", word: "Тысяча" }
                ]
            }
        ];

        const container = document.getElementById('flashcards');

        wordsData.forEach(wordObj => {
            const card = document.createElement('div');
            card.className = 'card';

            // Mynd
            const img = document.createElement('img');
            img.src = wordObj.img;
            img.alt = wordObj.is;
            img.onerror = function() {
                // Setur inn gráan ramma ef myndin finnst ekki í möppunni
                this.src = 'https://via.placeholder.com/400x220?text=Mynd+vantar';
            };
            card.appendChild(img);

            // Stórt íslenskt orð
            const title = document.createElement('h2');
            title.className = 'icelandic-word';
            title.innerHTML = `🇮🇸 ${wordObj.is}`;
            card.appendChild(title);

            // Þýðingar
            const transContainer = document.createElement('div');
            transContainer.className = 'translations';

            wordObj.translations.forEach(t => {
                const item = document.createElement('div');
                item.className = 'translation-item';
                item.innerHTML = `<span class="emoji">${t.flag}</span> <span>${t.word}</span>`;
                transContainer.appendChild(item);
            });

            card.appendChild(transContainer);
            container.appendChild(card);
        });
    </script>
</body>
</html>
