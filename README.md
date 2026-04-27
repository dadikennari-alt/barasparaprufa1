<!DOCTYPE html>
<html lang="is">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sagnorð í þátíð - Ég í gær</title>
    <style>
        * {
            box-sizing: border-box;
        }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f0f4f8;
            margin: 0;
            padding: 20px;
            color: #333;
        }
        h1 {
            text-align: center;
            color: #2c3e50;
            margin-bottom: 30px;
            font-size: 2.5rem;
        }
        .container {
            max-width: 1000px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: 1fr;
            gap: 25px;
        }
        .card {
            background: #ffffff;
            border-radius: 12px;
            padding: 25px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
            border-top: 5px solid #3498db;
        }
        .icelandic {
            font-size: 3rem; /* Gerir íslenskuna langstærsta */
            font-weight: bold;
            text-align: center;
            color: #2c3e50;
            margin-bottom: 25px;
            padding-bottom: 15px;
            border-bottom: 2px solid #ecf0f1;
        }
        .translations {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
            gap: 15px;
        }
        .trans-item {
            background: #f8f9fa;
            padding: 12px;
            border-radius: 8px;
            border: 1px solid #e9ecef;
            text-align: center;
        }
        .lang-label {
            display: block;
            font-size: 0.75rem;
            text-transform: uppercase;
            color: #7f8c8d;
            font-weight: bold;
            margin-bottom: 5px;
            letter-spacing: 0.5px;
        }
        .trans-text {
            font-size: 1rem;
            color: #34495e;
            font-weight: 500;
        }
        
        /* Til að líta vel út á símum */
        @media (max-width: 600px) {
            .icelandic {
                font-size: 2.2rem;
            }
        }
    </style>
</head>
<body>

    <h1>Hvað gerði ég í gær?</h1>
    <div class="container" id="app"></div>

    <script>
        // Hér eru allar 20 setningarnar ásamt þýðingum
        const data = [
            { is: "Ég vaknaði í gær.", en: "I woke up yesterday.", es: "Me desperté ayer.", pl: "Obudziłem(am) się wczoraj.", pt: "Eu acordei ontem.", ar: "استيقظت أمس.", fa: "من دیروز بیدار شدم.", vi: "Tôi đã thức dậy hôm qua.", ru: "Я проснулся(лась) вчера.", uk: "Я прокинувся(лася) вчора." },
            { is: "Ég borðaði í gær.", en: "I ate yesterday.", es: "Comí ayer.", pl: "Jadłem(am) wczoraj.", pt: "Eu comi ontem.", ar: "أكلت أمس.", fa: "من دیروز غذا خوردم.", vi: "Tôi đã ăn hôm qua.", ru: "Я ел(а) вчера.", uk: "Я їв(ла) вчора." },
            { is: "Ég drakk í gær.", en: "I drank yesterday.", es: "Bebí ayer.", pl: "Piłem(am) wczoraj.", pt: "Eu bebi ontem.", ar: "شربت أمس.", fa: "من دیروز نوشیدم.", vi: "Tôi đã uống hôm qua.", ru: "Я пил(а) вчера.", uk: "Я пив(ла) вчора." },
            { is: "Ég svaf í gær.", en: "I slept yesterday.", es: "Dormí ayer.", pl: "Spałem(am) wczoraj.", pt: "Eu dormi ontem.", ar: "نمت أمس.", fa: "من دیروز خوابیدم.", vi: "Tôi đã ngủ hôm qua.", ru: "Я спал(а) вчера.", uk: "Я спав(ла) вчора." },
            { is: "Ég las í gær.", en: "I read yesterday.", es: "Leí ayer.", pl: "Czytałem(am) wczoraj.", pt: "Eu li ontem.", ar: "قرأت أمس.", fa: "من دیروز خواندم.", vi: "Tôi đã đọc hôm qua.", ru: "Я читал(а) вчера.", uk: "Я читав(ла) вчора." },
            { is: "Ég skrifaði í gær.", en: "I wrote yesterday.", es: "Escribí ayer.", pl: "Pisałem(am) wczoraj.", pt: "Eu escrevi ontem.", ar: "كتبت أمس.", fa: "من دیروز نوشتم.", vi: "Tôi đã viết hôm qua.", ru: "Я писал(а) вчера.", uk: "Я писав(ла) вчора." },
            { is: "Ég lék mér í gær.", en: "I played yesterday.", es: "Jugué ayer.", pl: "Bawiłem(am) się wczoraj.", pt: "Eu brinquei ontem.", ar: "لعبت أمس.", fa: "من دیروز بازی کردم.", vi: "Tôi đã chơi hôm qua.", ru: "Я играл(а) вчера.", uk: "Я грав(лася) вчора." },
            { is: "Ég hljóp í gær.", en: "I ran yesterday.", es: "Corrí ayer.", pl: "Biegałem(am) wczoraj.", pt: "Eu corri ontem.", ar: "ركضت أمس.", fa: "من دیروز دویدم.", vi: "Tôi đã chạy hôm qua.", ru: "Я бегал(а) вчера.", uk: "Я бігав(ла) вчора." },
            { is: "Ég gekk í gær.", en: "I walked yesterday.", es: "Caminé ayer.", pl: "Chodziłem(am) wczoraj.", pt: "Eu andei ontem.", ar: "مشيت أمس.", fa: "من دیروز راه رفتم.", vi: "Tôi đã đi bộ hôm qua.", ru: "Я гулял(а) вчера.", uk: "Я гуляв(ла) вчора." },
            { is: "Ég lærði í gær.", en: "I studied yesterday.", es: "Estudié ayer.", pl: "Uczyłem(am) się wczoraj.", pt: "Eu estudei ontem.", ar: "درست أمس.", fa: "من دیروز درس خواندم.", vi: "Tôi đã học hôm qua.", ru: "Я учился(лась) вчера.", uk: "Я вчився(лася) вчора." },
            { is: "Ég talaði í gær.", en: "I talked yesterday.", es: "Hablé ayer.", pl: "Rozmawiałem(am) wczoraj.", pt: "Eu falei ontem.", ar: "تحدثت أمس.", fa: "من دیروز صحبت کردم.", vi: "Tôi đã nói chuyện hôm qua.", ru: "Я говорил(а) вчера.", uk: "Я говорив(ла) вчора." },
            { is: "Ég hlustaði í gær.", en: "I listened yesterday.", es: "Escuché ayer.", pl: "Słuchałem(am) wczoraj.", pt: "Eu ouvi ontem.", ar: "استمعت أمس.", fa: "من دیروز گوش دادم.", vi: "Tôi đã nghe hôm qua.", ru: "Я слушал(а) вчера.", uk: "Я слухав(ла) вчора." },
            { is: "Ég horfði í gær.", en: "I watched yesterday.", es: "Miré ayer.", pl: "Oglądałem(am) wczoraj.", pt: "Eu assisti ontem.", ar: "شاهدت أمس.", fa: "من دیروز تماشا کردم.", vi: "Tôi đã xem hôm qua.", ru: "Я смотрел(а) вчера.", uk: "Я дивився(лася) вчора." },
            { is: "Ég fór í gær.", en: "I went yesterday.", es: "Fui ayer.", pl: "Poszedłem/Poszłam wczoraj.", pt: "Eu fui ontem.", ar: "ذهبت أمس.", fa: "من دیروز رفتم.", vi: "Tôi đã đi hôm qua.", ru: "Я ходил(а) вчера.", uk: "Я ходив(ла) вчора." },
            { is: "Ég kom í gær.", en: "I came yesterday.", es: "Vine ayer.", pl: "Przyszedłem/Przyszłam wczoraj.", pt: "Eu vim ontem.", ar: "جئت أمس.", fa: "من دیروز آمدم.", vi: "Tôi đã đến hôm qua.", ru: "Я пришел(ла) вчера.", uk: "Я прийшов(ла) вчора." },
            { is: "Ég vann í gær.", en: "I worked yesterday.", es: "Trabajé ayer.", pl: "Pracowałem(am) wczoraj.", pt: "Eu trabalhei ontem.", ar: "عملت أمس.", fa: "من دیروز کار کردم.", vi: "Tôi đã làm việc hôm qua.", ru: "Я работал(а) вчера.", uk: "Я працював(ла) вчора." },
            { is: "Ég söng í gær.", en: "I sang yesterday.", es: "Canté ayer.", pl: "Śpiewałem(am) wczoraj.", pt: "Eu cantei ontem.", ar: "غنيت أمس.", fa: "من دیروز آواز خواندم.", vi: "Tôi đã hát hôm qua.", ru: "Я пел(а) вчера.", uk: "Я співав(ла) вчора." },
            { is: "Ég hló í gær.", en: "I laughed yesterday.", es: "Me reí ayer.", pl: "Śmiałem(am) się wczoraj.", pt: "Eu ri ontem.", ar: "ضحكت أمس.", fa: "من دیروز خندیدم.", vi: "Tôi đã cười hôm qua.", ru: "Я смеялся(лась) вчера.", uk: "Я сміявся(лася) вчора." },
            { is: "Ég grét í gær.", en: "I cried yesterday.", es: "Lloré ayer.", pl: "Płakałem(am) wczoraj.", pt: "Eu chorei ontem.", ar: "بكيت أمس.", fa: "من دیروز گریه کردم.", vi: "Tôi đã khóc hôm qua.", ru: "Я плакал(а) вчера.", uk: "Я плакав(ла) вчора." },
            { is: "Ég hjálpaði í gær.", en: "I helped yesterday.", es: "Ayudé ayer.", pl: "Pomagałem(am) wczoraj.", pt: "Eu ajudei ontem.", ar: "ساعدت أمس.", fa: "من دیروز کمک کردم.", vi: "Tôi đã giúp đỡ hôm qua.", ru: "Я помогал(а) вчера.", uk: "Я допомагав(ла) вчора." }
        ];

        // Nöfnin á tungumálunum sem birtast fyrir ofan hverja þýðingu
        const langNames = {
            en: "Enska",
            es: "Spænska",
            pl: "Pólska",
            pt: "Portúgalska",
            ar: "Arabíska",
            fa: "Persneska",
            vi: "Víetnamska",
            ru: "Rússneska",
            uk: "Úkraínska"
        };

        const appContainer = document.getElementById('app');

        // Býr til HTML kóðann fyrir hvert spjald
        data.forEach(item => {
            const card = document.createElement('div');
            card.className = 'card';

            // Íslenski textinn (stærstur)
            const isText = document.createElement('div');
            isText.className = 'icelandic';
            isText.textContent = item.is;
            card.appendChild(isText);

            // Geymsla fyrir þýðingarnar
            const transGrid = document.createElement('div');
            transGrid.className = 'translations';

            // Fer í gegnum hvert tungumál og býr til lítinn kassa fyrir það
            Object.keys(langNames).forEach(langKey => {
                const transItem = document.createElement('div');
                transItem.className = 'trans-item';
                
                const label = document.createElement('span');
                label.className = 'lang-label';
                label.textContent = langNames[langKey];
                
                const text = document.createElement('div');
                text.className = 'trans-text';
                text.setAttribute('dir', 'auto'); // Tryggir að Arabíska og Persneska lesist frá hægri til vinstri
                text.textContent = item[langKey];

                transItem.appendChild(label);
                transItem.appendChild(text);
                transGrid.appendChild(transItem);
            });

            card.appendChild(transGrid);
            appContainer.appendChild(card);
        });
    </script>

</body>
</html>
