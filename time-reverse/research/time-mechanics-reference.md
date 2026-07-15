# Механики времени в играх: референсы и находки

Дата: 2026-07-13. Ресёрч собран в рамках работы над аркадной игрой с физическим рулём,
управляющим ходом времени. Это самостоятельный обзор существующих игр и подходов —
источник референсов для дизайна и продакшена.

Метод: multi-agent workflow — 5 поисковых направлений, 22 источника прочитаны целиком,
извлечено ~108 фактов с точными цитатами, 25 ключевых утверждений прошли адверсариальную
проверку (3 независимых верификатора на факт; все 25 подтверждены). Цитаты разработчиков
и прессы приводятся в оригинале. Сжатая версия с проектными выводами — в
`docs/research/time-mechanics.md`.

---

## Карта подходов

Игры с управлением временем распадаются на четыре семейства механик, которые почти
не смешиваются (Braid — редкое исключение, он проходит через три из четырёх):

| Семейство | Суть | Ключевые игры |
|---|---|---|
| «Мир тикает от игрока» | Время течёт только когда игрок действует | SUPERHOT, Enter the Chronosphere, Time4Cat, поджанр roguetime |
| Перемотка (rewind) | Откат мира назад по записанной истории | Braid, Prince of Persia: The Sands of Time |
| Скраб таймлайна | Время — шкала, по которой игрок «ездит» в обе стороны | Crankin's Time Travel Adventure, The Gardens Between, Timelie |
| Переключение эпох | Мир существует в 2+ дискретных временных состояниях | Titanfall 2, Dishonored 2, Chronology, The Messenger, YesterMorrow |

### Плейлист для команды

Семь самых показательных видео — по одному-два на семейство механик (все ссылки
проверены на доступность; подробные блоки «Посмотреть» — в секциях игр ниже):

1. [SUPERHOT — Launch Trailer](https://www.youtube.com/watch?v=vrS86l_CtAY) —
   «мир тикает от игрока» в чистом виде: пули замирают, пока стоишь.
2. [Enter the Chronosphere — Early Access Launch Trailer](https://www.youtube.com/watch?v=C57NCAxSgn8) —
   та же идея в тиковой, пошаговой форме.
3. [Braid, Anniversary Edition — Launch Trailer](https://www.youtube.com/watch?v=cxT4Mews1ro) —
   rewind как головоломочное измерение.
4. [Crankin Presents: Time Travel Adventure — Playdate Season One](https://www.youtube.com/watch?v=qy1aQ0UXwgM) —
   физическая крутилка Playdate скрабит таймлайн персонажа в обе стороны.
5. [Timelie — Official Trailer](https://www.youtube.com/watch?v=4FX_j2Ot9D8) —
   «время как медиаплеер», таймлайн-скраббер прямо в интерфейсе.
6. [Titanfall 2 — «Effect & Cause», прохождение миссии](https://www.youtube.com/watch?v=2ohg2PNrocc) —
   переключение эпох на лету, в том числе посреди платформинга.
7. [Dishonored 2 — «A Crack in the Slab», прохождение миссии](https://www.youtube.com/watch?v=9W9o8sRIm_o) —
   линза-превью другой эпохи и каузальные головоломки 1849/1852.

---

## 1. «Мир тикает только от действий игрока»

### SUPERHOT (2016)

Каноничный пример того, как одно чистое правило несёт целую игру. Геймдиректор
Piotr Iwanicki в докладе «Game Design and Mind Control in SUPERHOT»
([GDC 2016](https://gdcvault.com/play/1023483/Game-Design-and-Mind-Control)) описывает
подход прямо:

> «SUPERHOT is an experimental FPS with the core idea of 'time moves only when you
> move'. We allowed this basic principle to resonate through the entire game design,
> with a view to crafting a unique gameplay experience.»

Главная находка — эмерджентность: боевые сценарии не проектировались поштучно, они
сами выросли из правила. Iwanicki перечисляет: «Dodging bullets, grabbing weapons
mid-air, using random items as improvised weapons are some of the things that
resulted». Второй эффект — сжатие масштаба: «the game features intense combat on
a much tighter scale than the typical FPS» — когда время в руках игрока, каждое
микродвижение значимо, и арена может быть размером с комнату.

Важный нюанс из сообщества роглайков
([RogueBasin](https://roguebasin.com/index.php/Roguetime)): формально SUPERHOT своему
слогану не соответствует — «contrary to the slogan, the bullets still move when you
don't move». Время не останавливается полностью, а сильно замедляется. Это осознанное
решение: лёгкое «подтекание» времени создаёт давление и не даёт игроку зависнуть
навсегда. А вот Time4Cat — маленькая flash-игра, вдохновившая SUPERHOT, — реализует
правило строго.

**Посмотреть:** [Launch Trailer (YouTube)](https://www.youtube.com/watch?v=vrS86l_CtAY) —
застывшие пули и осколки, время движется только с игроком ·
[Steam — скриншоты](https://store.steampowered.com/app/322500/SUPERHOT/)

### Enter the Chronosphere (бета — 2024)

Тот же паттерн в тактическом роглайке.
[PC Gamer](https://www.pcgamer.com/games/roguelike/enter-the-chronosphere-is-a-super-creative-roguelike-strategy-game-where-time-only-moves-when-you-move-and-you-can-try-the-open-beta-now/)
описывает механику предельно конкретно:

> «Time only moves when you move. Until you decide on what you're doing next, bullets
> hang in the air, enemies stand in place, bombs hang on their timers. But once you've
> decided to move, or shoot, or reload, or any other action, the whole world takes
> a step forward.»

Под капотом это дискретная (тиковая) модель, а не непрерывное замедление как в
SUPERHOT: автор сравнивает её с «turn-based combat system where all turns happen
simultaneously» — пошаговая система, где ходы игрока и всех врагов/снарядов исполняются
одновременно. Как ощущается — главное достоинство: ритм чередования обдумывания и
хаоса, «frenetic and strategic all at the same time as you shift from pondering your
next move to setting the whole world into mad, chaotic action».

Механика хорошо стыкуется с системой апгрейдов: способности начинают взаимодействовать
с самим тиком времени (например, авто-перезарядка при каждом движении), и решения
обостряются по мере прогресса. Предупреждение из ревью: вне напряжённых моментов
stop-and-go темп может утомлять — за паузами нужно следить.

**Посмотреть:** [Early Access Launch Trailer (YouTube)](https://www.youtube.com/watch?v=C57NCAxSgn8) —
висящие в воздухе пули и «шаг мира» за каждое действие ·
[Steam — скриншоты и демо](https://store.steampowered.com/app/1969810/Enter_the_Chronosphere/)
(с мая 2026 игра доступна в раннем доступе)

### Поджанр roguetime / «I move you move»

У паттерна есть имя и своя теория —
[RogueBasin](https://roguebasin.com/index.php/Roguetime) ведёт каталог «roguetime»-игр.
Определение: игрок управляет самим потоком времени темпом своих вводов —

> «In classic roguetime games, you press a single key to move once... Press keys
> slower, you move slower. Press keys faster, you move faster.»

То есть скорость нажатий буквально и есть скорость времени — по сути гранулярная
прокрутка времени игроком, только через клавиши, а не через крутилку. Там же —
объяснение, почему механика «работает» на ощущениях:

> «If the situation is difficult, you can think about your next action for as long as
> you want. This allows complexity that is impossible in action games. If the situation
> is trivial, you can just press the keys quickly.»

Игрок сам регулирует собственную сложность темпом — это позволяет глубину решений,
недостижимую в чистом экшене, не наказывая за тривиальные участки. Примеры за пределами
классических роглайков: платформер Bump! Аарона Стида («platformers in which you
control time... some do exist»), непрерывные «time moves only when you move» игры
WazHack и «догматический» режим Red Rogue.

### Урок из Cogmind: гранулярность тика — это дизайн-риск

Разработчик Cogmind (блог
[Grid Sage Games](https://www.gridsagegames.com/blog/2019/04/turn-time-systems/))
подробно разбирает эволюцию своей тиковой системы. Оригинальная схема (2012–2018):
ход = 100 единиц времени, действия стоят разное количество единиц, актор может
сцепить несколько непрерываемых действий внутри одного хода. Итог — конкретный
эксплойт: «it was possible to game subturn actions... to guarantee free peeks around
corners without being spotted» — игрок бесплатно выглядывал за угол, оставаясь
незамеченным. С Beta 8.1 систему заменили на простую очередь с пересортировкой
после каждого действия. Общий вывод автора:

> «as a time system grows increasingly nuanced, the more oddities arise and the more
> opaque or confusing [it becomes]»

Чем изощрённее правила течения времени (дробные ходы, переменные длительности),
тем больше краевых странностей и тем хуже игрок понимает, что происходит. Простое
правило тика — не только дешевле, но и читаемее.

---

## 2. Перемотка времени (rewind)

### Braid (2008) — эталон rewind как головоломочного измерения

Подробный разбор дизайна — у Станислава Станковича
([Game Mechanics of Braid, Medium](https://stanislav-stankovic.medium.com/game-mechanics-braid-78c289e95410)).
Ключевые ходы Braid, по порядку:

**Rewind сначала — прощение, потом — инструмент.** Перемотка доступна в любой момент
и без ограничений: «The time can be rewind at any moment and the player can repeat any
action and undo any mistake made in the level». Смерть перестаёт быть наказанием —
и игра может позволить себе жёсткие головоломки, потому что цена ошибки — ноль.

**Объекты-исключения превращают удобство в головоломку.** В World 3 появляются
объекты с зелёным свечением, не подверженные перемотке:

> «If a key is a normal key and the player first picks it up and then rewinds time,
> the key will drop to its original position. ... Time manipulation becomes necessary
> for puzzle-solving for the first time.»

Именно исключение из правила («это НЕ отматывается») впервые делает манипуляцию
временем обязательной, а не опциональной. Приём переносится на любую time-механику:
самое интересное начинается там, где часть мира не подчиняется времени игрока.

**World 4: движение игрока = ход времени.** Прямой родственник SUPERHOT-паттерна,
за 8 лет до SUPERHOT: «Time flows in the normal direction as the player moves from
left to right... Time moves backward if the direction of the player's movement
reverses... time stops flowing if the protagonist remains stationary». Позиция игрока
по горизонтали буквально является позицией на таймлайне уровня.

**Одна система — много механик.** Из той же записи/воспроизведения состояний Braid
собирает вариации по мирам: World 5 — теневой клон, повторяющий записанный путь
игрока после перемотки («Once the flow of time continues in the normal direction
the clone will follow the path that the player has traversed previously»); World 6 —
кольцо, создающее локальный «пузырь» замедления времени. Инфраструктура записи
состояний окупается несколько раз.

**Подача механик — инкрементальная и вне хронологии.** Игра начинается с World 2,
каждый мир добавляет ровно одну временную вариацию поверх освоенных, а финальный
World 1, где время само течёт назад, «beautifully uniting the time manipulation
gameplay with the narrative of the game». Образец поэтапного введения time-механик,
пригодный и для короткой игры.

О технической стороне Braid — в разделе 5: это самый дорогой rewind в истории жанра
и сознательный анти-образец для малых команд.

**Посмотреть:** [Braid, Anniversary Edition — Launch Trailer (YouTube)](https://www.youtube.com/watch?v=cxT4Mews1ro) —
перемотка и вариации механики в движении ·
[Steam — Braid, Anniversary Edition, скриншоты](https://store.steampowered.com/app/499180/Braid_Anniversary_Edition/)

### Prince of Persia: The Sands of Time (2003)

Родоначальник rewind в мейнстриме — туториал tutsplus
([How to Build a Prince of Persia-Style Time Rewind System](https://gamedevelopment.tutsplus.com/tutorials/how-to-build-a-prince-of-persia-style-time-rewind-system-part-1--cms-26090))
называет её «one of the first games to truly integrate a time-rewinding mechanic into
its gameplay». Формула PoP: rewind — ограниченный ресурс (песок), тратящийся на отмену
последних секунд, прежде всего смертельной ошибки. В отличие от Braid здесь перемотка —
не головоломочное измерение, а «страховка» с экономикой: игрок решает, когда ошибка
стоит заряда. Тот же туториал — базовый источник по реализации короткого окна отмотки
(см. раздел 5).

**Посмотреть:** [«How Prince of Persia: The Sands of Time Mastered Time Reversal» (YouTube)](https://www.youtube.com/watch?v=bE6l4_LxFBE) —
видеоразбор именно rewind-механики ·
[Steam — оригинал 2003 года, скриншоты](https://store.steampowered.com/app/13600/Prince_of_Persia_The_Sands_of_Time/)

---

## 3. Скраб таймлайна

Отдельное семейство: время — это шкала, по которой игрок перемещается в обе стороны
как по записи, и позиция на шкале — основной орган управления.

### Crankin's Time Travel Adventure (Playdate, 2022) — физическая крутилка времени

Самый близкий существующий прецедент «времени в руке». Игра студии uvula — Кейта
Такахаси (создатель Katamari Damacy) и аниматор Райан Молер — для консоли Playdate
с торчащей сбоку физической ручкой-крутилкой (crank).

**Как устроено.** Крутилка напрямую скрабит таймлайн персонажа: вращение вперёд —
Crankin идёт вперёд, назад — его движения отматываются, скорость времени равна
скорости вращения. Из интервью с инженером Shaun Inman
([Game Developer](https://www.gamedeveloper.com/playdate-launch/literally-spinning-a-yarn-in-time-bending-puzzler-crankin-s-time-travel-adventure)):

> «You have one timeline that enemies are on. It's always moving forwards... Then you
> have the timeline that Crankin and Crankette are on, which is powered by the crank.
> ... you only advance it as you crank, and that's dependent on the speed of the crank.»

Архитектурно это **два раздельных таймлайна**: враги и препятствия живут в реальном
времени по своим фиксированным циклам, а персонаж — на отдельном таймлайне, питаемом
только вращением. Ревью
[The Game Hoard](https://thegamehoard.com/2023/09/12/crankins-time-travel-adventure-playdate/)
уточняет тактильную деталь: если перестать крутить, персонаж замирает где есть —
«if you stop spinning entirely, Crankin will stay in place even if that might leave
him floating in midair». Персонаж, висящий в воздухе, пока рука не крутит, — очень
сильное «ощущение времени в руке».

**На чём строятся головоломки.** Не на управлении персонажем (его маршрут предзаписан),
а на позиционировании его во времени относительно живых угроз. По пути Crankin
автоматически выполняет контекстные действия — нюхает цветок, повисает на перекладине —
и это не декорации, а ключ к выживанию: в этих позах угрозы пролетают над или под ним.
Игрок скрабом подбирает нужную позу в нужный момент реального времени. Это чистая
головоломка на «докрутить до нужного кадра».

**Инженерные находки.** Главной технической проблемой оказалась не обратимость
логики, а скорость доступа к данным при скрабе: Inman «faced significant bandwidth
and memory issues accessing animation frames quickly enough», пришлось писать кастовую
работу с файлами в обход SDK и собственный визуальный редактор уровней для
секвенсирования действий. Урок: скраб требует мгновенного произвольного доступа
к любому кадру — заранее записанные/подготовленные состояния, а не пересимуляция.

**Команда.** Игру сделали фактически 2–4 человека: uvula (Такахаси + Молер), один
инженер Panic (Inman) и саунд-дизайнер. Молер о жёстких ограничениях (спрайтовая
анимация, один тип ввода): ограничения не мешают, а фокусируют — «ease you up to worry
about the right things».

**Критика — тоже урок.** The Game Hoard поставил игре разгромную оценку: лимит времени
на уровень, мгновенная смерть от касания врага «even a pixel of his deliberately tall
and awkward body», ограниченная видимость экрана — вместе это вынуждает заучивать
уровни наизусть. Вывод от противного: скраб-механика по природе своей — про
эксперименты и подбор, и карающий дизайн (таймеры, one-hit death, заучивание) с ней
конфликтует. Сама крутилка при этом в ревью не критикуется — претензии к обвесу.

**Посмотреть:** [официальная страница на play.date](https://play.date/games/crankin/) —
скриншоты и описание управления («uses only the crank, and requires a fair amount of
precision with it») ·
[геймплей с крутилкой (YouTube)](https://www.youtube.com/watch?v=qy1aQ0UXwgM) — видно
главное: как вращение ручки ведёт таймлайн персонажа вперёд и назад ·
[видео «Advance/rewind the timeline» (YouTube)](https://www.youtube.com/watch?v=x_9UudUAQNs)

### The Gardens Between (2018)

Пазл The Voxel Agents: игрок вообще не управляет персонажами напрямую — только двигает
их вперёд и назад по времени, попутно меняя состояние отдельных объектов
([Gamingscan](https://www.gamingscan.com/best-time-travel-games/)): «you don't control
the main characters directly but rather move them backward and forwards through time
while altering the state of different objects to progress». По сути «Crankin без
крутилки»: маршрут предзаписан, головоломка — в комбинации позиции на таймлайне
и объектов-исключений, которые времени не подчиняются (тот же ход, что зелёные объекты
Braid). 20 уровней, ~2.5 часа — компактный формат, целиком вывезенный одной механикой.

**Посмотреть:** [Release Date Trailer (YouTube)](https://www.youtube.com/watch?v=1WOZzU-4hNs) —
скраб времени: острова-виньетки прокручиваются вперёд/назад вместе с персонажами ·
[Steam — скриншоты](https://store.steampowered.com/app/600990/The_Gardens_Between/)

### Timelie (2020)

Стелс-головоломка, где героиня управляет потоком времени «как медиаплеером» —
«rewinding and fast-forwarding to gain new perspectives», перематывая мир в обе
стороны, чтобы менять препятствия и уходить от патрулей роботов
([Gamingscan](https://www.gamingscan.com/best-time-travel-games/)). Интерфейс — буквально
таймлайн-скраббер как в видеоредакторе. Полезный референс UI: игрок видит шкалу
и свободно ездит по ней, планируя маршрут, — «время как медиаплеер» это готовая
ментальная модель, которую не нужно объяснять.

**Посмотреть:** [Official Trailer (YouTube)](https://www.youtube.com/watch?v=4FX_j2Ot9D8) —
таймлайн-скраббер в интерфейсе и перемотка мира в обе стороны ·
[Steam — скриншоты](https://store.steampowered.com/app/1150950/Timelie/)

---

## 4. Переключение эпох

Семейство, где время — не непрерывная шкала, а 2+ дискретных состояния мира,
между которыми игрок переключается. Технически самое дешёвое из всех: обратимость
симуляции не нужна вообще, нужны две версии контента.

### Titanfall 2, миссия «Effect and Cause» (2016)

Один из самых хвалёных уровней десятилетия. Игрок получает наручное устройство
(снятое с тела майора Андерсона) и прыгает между прошлым (исследовательский комплекс
цел и полон охраны) и настоящим (комплекс разрушен и горит) — сначала сдвиги
непроизвольны, после находки устройства переключение произвольное, по кнопке
([Cultured Vultures](https://culturedvultures.com/memorable-mechanics-titanfall-2s-time-displacement/)).

**Головоломки на контрасте эпох.** В настоящем коридоры перекрыты «insurmountable
flames and debris», в прошлом путь чист, но патрулируется солдатами. Платформинг
требует прыгать между эпохами прямо в воздухе, чтобы дотягиваться до уступов,
существующих только в одной из версий; автор разбора сравнивает решение таких задач
с кубиком Рубика — многослойным перебором состояний.

**Бой в двух эпохах одновременно.** Таймлайны имеют раздельное состояние и разные
типы угроз ([разбор на MapCore](https://www.mapcore.org/articles/development/effect-and-cause-titanfall-2-level-breakdown-r96/)):
в настоящем — роботы и дикая фауна, в прошлом — вооружённая охрана. Критично:
«Eliminating the danger in one reality does not make it disappear in the other» —
убитый в одной эпохе враг никуда не девается из другой, и игрок вынужден постоянно
держать в голове свою позицию относительно обеих. Есть и засада, устроенная сразу
в обоих временных периодах.

**UX-находка: призраки другой эпохи.** Чтобы игрок не запоминал позиции врагов
вслепую, при переключении враги оставляют след:

> «Once you move from past to the present, enemies leave a small blue particle in the
> place where they had been standing. Although the effect lasts no longer than two
> seconds, it's enough to help players plan their next move.»

Двухсекундная голубая дымка на месте врагов из покинутой эпохи — дешёвый приём,
резко повышающий читаемость межэпохальной навигации.

**Обучение через безопасную песочницу.** В первом свободном энкаунтере враги есть
только в прошлом — «As there is no threat in the past timeline, players can experiment
with going back in time without punishment, 'escaping' the combat at any given moment
in order to reload, reposition and jump back». Игрок безнаказанно осваивает переключение
до того, как оно станет обязательным. Переключение используется и как гейтинг:
некоторые пространства непроходимы ни в одной эпохе по отдельности.

**Как сделано технически.** MapCore формулирует прямо:

> «time-shifting is nothing more than teleportation between two different levels, one
> layered on top of another, but the strong execution makes for a memorable experience.»

Комментатор Sigma (со ссылкой на материалы о создании уровня) уточняет: «two
(mirrored essentially) levels that were consistently offset from one another. The time
travel mechanic merely offsets the player, maintaining orientation and velocity,
between the two play areas» — две почти зеркальные копии уровня с постоянным смещением,
телепорт сохраняет ориентацию и скорость игрока, скриптинг в основном на триггерах
близости. Никакой симуляции времени — иллюзия целиком собрана из смещения игрока
и сильного арта/аудио.

**Посмотреть:** [прохождение миссии «Effect & Cause» (YouTube)](https://www.youtube.com/watch?v=2ohg2PNrocc) —
переключение эпох на лету, контраст «горящая руина / рабочий комплекс» ·
[разбор уровня со скриншотами (MapCore)](https://www.mapcore.org/articles/development/effect-and-cause-titanfall-2-level-breakdown-r96/) ·
[Steam — скриншоты](https://store.steampowered.com/app/1237970/Titanfall_2/)

### Dishonored 2, миссия «A Crack in the Slab» (2016)

Второй канонический уровень с переключением эпох
([Kotaku](https://kotaku.com/what-made-dishonored-2s-time-travel-level-so-good-1819596566)).
Игрок получает устройство-timepiece и переключается между 1849 (особняк жив, идёт
званый вечер) и 1852 (особняк — гниющая руина). Два приёма сверх Titanfall:

**Превью другой эпохи перед прыжком.** Timepiece работает как линза: «a tool that lets
you observe the year 1849 through its crystals and jump between the 1849 and...
1852» — игрок сначала подсматривает, что на этом месте в другой эпохе, и только потом
прыгает. Паттерн «превью + переключение» снимает главный страх механики — прыжок
вслепую в стену или к врагу.

**Каузальность между эпохами.** Головоломки строятся на микроразличиях состояний:
«You can walk into a small space between where the door ought to be and where the
grate is, jump through time, and find yourself on the other side of the locked door» —
дверь заперта в одной эпохе, решётка стоит в другой, а зазор между их позициями
и есть решение. Но главное — действия в прошлом меняют настоящее в реальном времени:

> «If you knock the bust over in 1849, breaking it, it's no longer blocking the passage
> in 1852, allowing you to advance through the level.»

Kotaku резюмирует: «The entire level is like this, full of clever, mind-bending puzzles
and actions that ripple throughout the past and present». Технически (по независимым
разборам) — те же две копии карты в одной сцене с телепортом между ними, что и
в Titanfall 2; каузальность — скриптованные связки конкретных объектов, а не симуляция.

**Посмотреть:** [прохождение миссии «A Crack in the Slab» (YouTube)](https://www.youtube.com/watch?v=9W9o8sRIm_o) —
линза-превью timepiece и переключение 1849/1852 ·
[статья Kotaku со скриншотами уровня](https://kotaku.com/what-made-dishonored-2s-time-travel-level-so-good-1819596566) ·
[Steam — скриншоты](https://store.steampowered.com/app/403640/Dishonored_2/)

### Chronology (2014)

Пазл-платформер Bedtime Digital Games (Дания), целиком построенный на переключении
эпох. Официальное позиционирование
([Steam](https://store.steampowered.com/app/269330/Chronology/)):

> «a mind-bending mix of puzzle, platform and adventure where you defy time by
> manipulating the past and the future, in order to fix the present» ...
> «Time changes everything — Solve puzzle by travelling back and forth in — or
> freezing — time.»

Мир существует в двух состояниях — идиллическое прошлое и тёмное антиутопичное
будущее, — и головоломки строятся на переключении между ними («в одной эпохе цело,
в другой разрушено»). Вторая механика — заморозка времени; третье измерение
головоломок — переключение между двумя персонажами с разными способностями (Старый
Изобретатель путешествует по времени, Улитка замораживает время):
«Switch between two lovable characters with different abilities and combine their
strengths» ([Wikipedia](https://en.wikipedia.org/wiki/Chronology_(video_game))).

Команда маленькая (в титрах названы продюсер, дизайнер и программист); релиз — Windows
12 мая 2014, iOS 12 сентября 2014. Приём: 89% положительных из 528 обзоров Steam,
Metacritic 77/100 (iOS) и 64/100 (PC), рецензенты сравнивали с Braid и LIMBO, отмечая:
«Time travel is an underused gameplay mechanic, and I hope more games use it like
Chronology does». Нюансы: переключение бинарное (прошлое/будущее, без промежуточных
состояний), а общая эстетика яркая — «magical, colorful, vibrant» — антиутопична только
эпоха будущего.

**Посмотреть:** [Launch Trailer (YouTube)](https://www.youtube.com/watch?v=jdKB_XSpM6Q) —
переключение «идиллическое прошлое / антиутопичное будущее» и заморозка времени ·
[Steam — скриншоты](https://store.steampowered.com/app/269330/Chronology/)

### The Messenger (2018)

Платформер Sabotage Studio (Квебек, сделан на Unity), где эпоха маркируется самим
рендером ([Wikipedia](https://en.wikipedia.org/wiki/The_Messenger_(2018_video_game))):
прошлое — 8-битная графика и звук, будущее — 16-битное. Смена эпохи считывается
мгновенно и без UI — стиль и есть индикатор. Переключение напрямую меняет геометрию:
«special warps to move between the past and present, changing the layout of each level
and allowing them to access new areas». Интересен масштабированием механики: в середине
игра превращается из линейного платформера в метроидванию, где игрок свободно ходит
между эпохами в любом порядке в поисках ключевых предметов — эра-свитчинг работает и
как уровневая головоломка, и как основа нелинейного исследования. Ранний прототип
механики один дизайнер собрал примерно за шесть месяцев.

**Посмотреть:** [Gameplay Trailer (YouTube)](https://www.youtube.com/watch?v=2vaYsgOHTlI) —
смена эпох как смена рендера: 8-бит против 16-бит в одном уровне ·
[Steam — скриншоты](https://store.steampowered.com/app/764790/The_Messenger/)

### YesterMorrow (2020)

2D-платформер Bitmap Galaxy (издатель Blowfish Studios, Switch — 5 ноября 2020,
$19.99) на двух таймлайнах с выраженным постапокалиптическим настроением
([Nintendo Life](https://www.nintendolife.com/news/2020/11/time-travelling_2d_platformer_yestermorrow_launches_on_switch_this_week)):
«Traverse across two different timelines, enjoying the serene calmness of the past and
battling her way through the corrupted world of the future». Мир героини Yui уничтожен
сущностями Shadows, семья похищена; классический платформинг + экшен-эпизоды +
головоломки на использование окружения, то есть переключение таймлайнов встроено
в паззл-дизайн. Четыре островных биома, включая «Остров Времени», и сюжет про Орден
Хранителей Времени — время здесь и механика, и тема.

**Посмотреть:** [Launch Trailer (YouTube)](https://www.youtube.com/watch?v=3BAhPAxGvWk) —
безмятежное прошлое против разрушенного будущего ·
[Steam — скриншоты](https://store.steampowered.com/app/1210490/YesterMorrow/)

### Reminiscence (2021)

Психологический хоррор-пазл (Windows), найден в подборке
[Gamingscan](https://www.gamingscan.com/best-time-travel-games/):

> «you stumble upon a watch that lets you travel between two epochs: the
> post-apocalyptic present, and 1950s American suburbia. By switching back and forth
> between both realities, you're able to alter the state of certain objects to solve
> puzzles and advance the story.»

Интересен контрастом эпох как настроением: не «прошлое/будущее одной локации»,
а постапокалипсис против уютных 1950-х — переключение само по себе несёт хоррор-эффект.

**Посмотреть:** [Steam — скриншоты обеих эпох](https://store.steampowered.com/app/1675140/Reminiscence/)
(игра бесплатная; надёжного официального трейлера не нашлось)

### Инди-пул и прочие кандидаты

Каталог itch.io показывает, насколько это «джемовое» семейство механик:
[697 платформеров с тегом time-travel](https://itch.io/games/genre-platformer/tag-time-travel).
Из заметного: игры целиком на rewind — Undo (lunadyedred, «Rewind physics to solve
puzzles») и Retrograde (ooooggll, «A puzzle platformer where you invert time»);
переключение периодов — Bobby Six Seven (calgames, «Run, jump and shoot through time
periods») и TimeLoop (GrayMansion); механика записанных прошлых прогонов/«призраков»
как основа головоломок — Looper (Maytch, «Use your past movement Loops to get to the
finish!») и Tempus Locus (nubitoad, «What if you could replay the past?»); time-loop
метроидвания — Vision Soft Reset (Seafloor Games). Масштаб пула — прямое свидетельство,
что все эти механики регулярно поднимаются соло-разработчиками и в геймджем-формате.

В верифицированную выборку не попали, но регулярно всплывали в поиске и заслуживают
взгляда: Quantum Conundrum (переключение «измерений» с разной физикой), The Silent Age
(point-and-click с переключением настоящее/постапокалиптическое будущее),
The Legend of Zelda: Oracle of Ages и Chrono Trigger (классика эпох в Zelda/JRPG-форме).

---

## 5. Физические и альтернативные контроллеры

### Playdate crank — единственная серийная «крутилка времени»

Playdate — единственная массовая платформа с аналоговой ручкой-крутилкой как
полноценным органом управления, и Crankin's Time Travel Adventure (раздел 3) — главный
пример её использования именно как контроллера времени. Что даёт физическая крутилка
по сравнению с кнопкой/стиком, по опыту Crankin:

- **Непрерывность**: скорость времени = скорость вращения, направление = знак. Это
  аналоговый маппинг, который кнопкой не воспроизводится в принципе.
- **Останов как состояние**: отпустил — мир (или персонаж) замер, хоть в воздухе.
  Пауза не режим меню, а естественное положение руки.
- **Тактильная драматургия**: «докрутить до нужного кадра» ощущается физическим
  micro-adjustment, как фокусировка объектива — сама моторика становится геймплеем.

Инженерное следствие (из интервью Inman, раздел 3): физический скраб беспощаден
к задержкам — любой кадр таймлайна должен быть доступен мгновенно, в обе стороны,
на любой скорости вращения.

### GDC 2023: методология alt-ctrl дизайна

Доклад Tatiana Vilela dos Santos (студия MechBird) «Alternative Controller Game
Design: From Game Design to Controller Design»
([GDC 2023](https://gdcvault.com/play/1028935/Alternative-Controller-Game-Design-From)) —
основной методологический источник по alt-ctrl (сокращение от alternative controllers —
самодельные/нестандартные физические контроллеры). Ядро доклада — четыре способа
сделать контроллер игровым элементом, а не средством доступа к игре:

> «four ways to design game experiences apprehending the controller—not just as a mean
> to experience the game, but as a game element in itself»

1. **Контроллер как механика** — свойства железа (сопротивление, инерция, форма) сами
   являются правилами игры;
2. **Контроллер как сенсорный опыт** — тактильность и моторика как содержание;
3. **Контроллер как нарративный инструмент** — предмет в руках рассказывает историю;
4. **Контроллер как переопределитель физического пространства** — железо меняет то,
   как игроки стоят/двигаются вокруг игры.

Два поддерживающих тезиса. Во-первых, alt-ctrl — устоявшееся движение, а не экзотика:
«At the confluence of the indie game movement and maker culture, some developers are
building custom DIY controllers, using electronics and hijacking technologies, to
create unique game experiences». Во-вторых, история индустрии — это история взаимного
влияния геймдизайна и контроллеров («From the advent of the D-pad to the emergence of
the twin-stick gamepad»), из чего следует практический принцип: механику и физический
интерфейс нужно проектировать совместно, а не последовательно. Оговорка: видео доклада
на GDC Vault за платной подпиской, публично доступна аннотация.

---

## 6. Как это делают технически (обзорно)

### Два лагеря: запись состояний vs детерминированная симуляция

Обратимое время реализуют двумя принципиально разными способами. Первый — **запись
состояний (снапшоты)**: игра периодически сохраняет слепки состояния объектов и при
отмотке воспроизводит их в обратном порядке; «назад» — это плеер, а не симуляция.
Второй — **детерминированная симуляция**: мир пересчитывается заново из начальных
условий (детерминированность означает, что при тех же входах симуляция всегда даёт
байт-в-байт тот же результат). Второй путь экономит память, но требует, чтобы вся
игра — физика, ИИ, случайности — была построена детерминированной с первого дня.

Практика однозначна: все найденные решения малых команд — про запись состояний.
Автор разбора механик Braid в
[Game Developer](https://www.gamedeveloper.com/programming/recreating-the-time-mechanics-of-braid-part-1-)
формулирует итог исследования подхода Джонатана Блоу одной фразой: «He saved off
relevant pieces of the game state» — даже Braid в основе своей записывает состояния,
а не «крутит физику назад».

### Стандартные приёмы записи

Из туториалов и открытых решений складывается устойчивый набор приёмов (без кода,
по сути):

- **Запись на фиксированном тике.** Состояние пишется в шаге физики (в Unity —
  FixedUpdate, по умолчанию 50 раз в секунду), а не в кадре рендера: фиксированный
  интервал даёт ровное воспроизведение независимо от FPS
  ([tutsplus](https://gamedevelopment.tutsplus.com/tutorials/how-to-build-a-prince-of-persia-style-time-rewind-system-part-1--cms-26090)).
- **Ключевые кадры + интерполяция.** Писать не каждый тик, а каждый N-й (в туториале
  tutsplus — примерно каждый 12-й), между записями интерполировать. Режет объём данных
  на порядок при визуально гладкой отмотке
  ([Game Developer](https://www.gamedeveloper.com/programming/recreating-the-time-mechanics-of-braid-part-1-)).
- **Запись только изменений.** Не писать состояние объекта, пока оно не поменялось:
  «This allows for objects that hardly move to use hardly any data» — статичная часть
  сцены почти ничего не стоит (там же).
- **Отключение физики на время отмотки.** Ключевой трюк против конфликта физдвижка
  с обратным движением: на время перемотки твёрдое тело переводится в кинематический
  режим (физика его не трогает), объект ведётся вручную по записи, после отмотки
  физика включается обратно. Физику никогда не «симулируют назад» — только
  воспроизводят записанное ([Brackeys](https://github.com/Brackeys/Rewind-Time)).
- **Анимация при отмотке.** Два рабочих ответа: записывать параметры аниматора вместе
  с остальным состоянием и восстанавливать их (путь UnityTimeRewinder, см. ниже) —
  либо покадровые спрайты, где «кадр анимации» просто часть записанного состояния
  (путь Crankin).

### Цена по памяти: окно записи

Память наивной записи растёт линейно: количество объектов × частота записи ×
длительность окна. Поэтому все малые решения ограничивают историю **кольцевым
буфером** (фиксированный буфер, где новые записи затирают самые старые): у Brackeys
окно по умолчанию — 5 секунд, самый старый кадр выбрасывается при переполнении;
туториал tutsplus держит порядка 75 записей и прямо предупреждает, что неограниченный
список «в лоб» — путь к падению игры. Типичное окно в таких системах — секунды,
максимум десятки секунд. Оценка из практики: переход от 2D к 3D добавляет к объёму
записи примерно 50% (третья координата).

### Braid — исключение, подтверждающее правило

Верхняя планка жанра задокументирована самим Джонатаном Блоу в докладе
[«The Implementation of Rewind in Braid» (GDC 2010)](https://gdcvault.com/play/1012210/The-Implementation-of-Rewind-in)
(запись в GDC Vault помечена как бесплатная — можно смотреть целиком). Требования,
которые он себе поставил: отмотка **30–60 минут** непрерывного геймплея — фактически
вся сессия уровня; вся история — в **40 МБ** памяти на консолях; отмотка строго
точная — «robust, exactly reproducing the game scene at each given time», никаких
приблизительных реплеев. Достигнуто это тяжёлой инженерией: пообъектная компрессия,
селективная запись с детерминированной регенерацией того, что можно не хранить; доклад
разбирает рассмотренные альтернативы и почему победил именно этот метод. Блоу отмечал,
что за 14 лет эквивалентную систему никто не повторил. Для оценки «сколько стоит
rewind» цифры Braid использовать нельзя — это результат многолетней оптимизации,
а не цена наивных снапшотов. Практический стандарт малых команд противоположен:
короткое окно в кольцевом буфере.

### Готовые решения для Unity

Минимальный образец — [Brackeys Rewind-Time](https://github.com/Brackeys/Rewind-Time)
(public domain, можно использовать в том числе коммерчески): один компонент примерно
на 70 строк, который каждый физический тик пишет позицию и поворот объекта в список,
а при отмотке проигрывает записи в обратном порядке; окно 5 секунд, физика на время
отмотки отключается. Записывает только позицию/поворот — скорости, анимации и игровая
логика остаются за рамками, это скелет для расширения. Более полное решение —
[UnityTimeRewinder](https://github.com/SitronX/UnityTimeRewinder) (MIT, Unity 2019+,
315 звёзд, последний релиз v3.2 — август 2024): кольцевой буфер снапшотов, из коробки
отматывает активность объектов, transform, скорости твёрдых тел, аниматоры со всеми
слоями и параметрами (то есть проблема обратной анимации решена), аудио и системы
частиц; расширяется на произвольные пользовательские переменные вплоть до шейдеров.
Поддерживает два режима: мгновенный откат на N секунд и **скраб по таймлайну с превью
и выбором снапшота** — редкий готовый аналог «джога» по времени. Скрабит только назад;
с августа 2024 коммитов нет.

---

## 7. Сквозные наблюдения

Паттерны, повторяющиеся у независимых команд в разных семействах механик:

1. **Одно чистое правило времени несёт целую игру.** SUPERHOT, Chronosphere, Braid
   World 4, Crankin — в каждом случае весь дизайн — резонанс одного правила, и
   ситуации возникают эмерджентно, а не проектируются поштучно.
2. **Механика становится головоломкой через исключения.** Зелёные объекты Braid,
   враги в реальном времени у Crankin, объекты-константы Gardens Between: интересно
   не «всё подчиняется времени», а «кое-что — нет».
3. **Показывать другую эпоху/состояние до и после переключения.** Линза-превью
   Dishonored 2 перед прыжком, двухсекундные голубые призраки врагов в Titanfall 2
   после него — читаемость межвременной навигации делается дёшево, но именно она
   отличает «магию» от дезориентации.
4. **Переключение эпох — это телепорт между двумя копиями контента.** И Titanfall 2,
   и Dishonored 2 под капотом держат две версии карты и перемещают игрока между ними,
   сохраняя ориентацию и скорость. Никакой симуляции времени.
5. **Обучение — в безопасной песочнице.** Первый энкаунтер «Effect and Cause» держит
   врагов только в одной эпохе, чтобы игрок безнаказанно освоил переключение; Braid
   вводит по одной вариации за мир.
6. **Rewind снимает наказание — и этим развязывает руки сложности.** Braid и PoP:
   когда ошибка отменяема, головоломки можно делать жёстче. Обратный урок Crankin:
   карающий обвес (таймеры, one-hit death) конфликтует с экспериментальной природой
   скраба.
7. **Время в руках игрока = игрок сам регулирует сложность темпом.** Тезис RogueBasin:
   думать можно сколько угодно, тривиальное проходится быстро. Оборотная сторона
   (ревью Chronosphere): вне напряжения stop-and-go утомляет — темп спокойных секций
   требует отдельного внимания.
8. **Технический консенсус малых команд: записывай и воспроизводи, не пересчитывай.**
   Снапшоты в кольцевом буфере с коротким окном, физика отключается на отмотке,
   анимация — из записанных параметров или покадровых спрайтов. Детерминированная
   пересимуляция и Braid-масштаб — отдельная лига со своей ценой.

---

## Открытые вопросы: на подумать команде

Механика игры решена и строится сначала как грейбокс; мир, сюжет и арт будут
накладываться сверху. Вот вопросы, которые пока никак не решены, — думать над ними
можно параллельно, отталкиваясь от референсов выше:

1. **Кто персонаж** — человек, робот, дух, абстрактное существо? По механике на него
   не действует время (у уровня есть таймлайн, персонаж существует вне его). Почему
   так: просто данность — или за этим стоит история? История задаст тон всей игре.
2. **Что за место мы проходим** — руины города, музей (автомат будет стоять в музее —
   это может сыграть), завод, природа, поглотившая цивилизацию?
3. **Температура постапокалипсиса** — тёплый и меланхоличный (как в Chronology:
   «починить настоящее»), холодный и тревожный, или вовсе без трагедии — просто
   застывший мир, который ждёт, чтобы его прокрутили?
4. **Визуальный стиль** — пиксель-арт, рисованная 2D-графика, силуэты? Отдельно
   стоит смотреть, как The Messenger сделал стиль маркером эпохи (8-бит прошлое /
   16-бит будущее) — у нас стиль мог бы аналогично реагировать на руль.
5. **Финальная сцена** — игра конечная (N экранов + финал). Каким должен быть
   финальный образ, чтобы посетитель музея ушёл с впечатлением? Связано с ответами
   на вопросы выше.

## Источники

**Первичные (разработчики, код, магазины):**
- [GDC 2016 — Piotr Iwanicki, «Game Design and Mind Control in SUPERHOT»](https://gdcvault.com/play/1023483/Game-Design-and-Mind-Control)
- [GDC 2010 — Jonathan Blow, «The Implementation of Rewind in Braid»](https://gdcvault.com/play/1012210/The-Implementation-of-Rewind-in) (запись бесплатная)
- [GDC 2023 — Tatiana Vilela dos Santos, «Alternative Controller Game Design»](https://gdcvault.com/play/1028935/Alternative-Controller-Game-Design-From)
- [Brackeys — Rewind-Time (public domain)](https://github.com/Brackeys/Rewind-Time)
- [SitronX — UnityTimeRewinder (MIT)](https://github.com/SitronX/UnityTimeRewinder)
- [Chronology в Steam](https://store.steampowered.com/app/269330/Chronology/)

**Интервью и разборы:**
- [Game Developer — интервью с инженером Crankin's Time Travel Adventure](https://www.gamedeveloper.com/playdate-launch/literally-spinning-a-yarn-in-time-bending-puzzler-crankin-s-time-travel-adventure)
- [MapCore — «Effect and Cause»: level breakdown](https://www.mapcore.org/articles/development/effect-and-cause-titanfall-2-level-breakdown-r96/)
- [Cultured Vultures — Titanfall 2's Time Displacement](https://culturedvultures.com/memorable-mechanics-titanfall-2s-time-displacement/)
- [Kotaku — What Made Dishonored 2's Time Travel Level So Good](https://kotaku.com/what-made-dishonored-2s-time-travel-level-so-good-1819596566)
- [Stanislav Stankovic — Game Mechanics of Braid](https://stanislav-stankovic.medium.com/game-mechanics-braid-78c289e95410)
- [Game Developer — Recreating the Time Mechanics of Braid](https://www.gamedeveloper.com/programming/recreating-the-time-mechanics-of-braid-part-1-)
- [tutsplus — Prince of Persia-Style Time Rewind System](https://gamedevelopment.tutsplus.com/tutorials/how-to-build-a-prince-of-persia-style-time-rewind-system-part-1--cms-26090)
- [Grid Sage Games — Turn & Time Systems (Cogmind)](https://www.gridsagegames.com/blog/2019/04/turn-time-systems/)

**Пресса и каталоги:**
- [PC Gamer — Enter the Chronosphere](https://www.pcgamer.com/games/roguelike/enter-the-chronosphere-is-a-super-creative-roguelike-strategy-game-where-time-only-moves-when-you-move-and-you-can-try-the-open-beta-now/)
- [RogueBasin — Roguetime](https://roguebasin.com/index.php/Roguetime)
- [The Game Hoard — ревью Crankin's Time Travel Adventure](https://thegamehoard.com/2023/09/12/crankins-time-travel-adventure-playdate/)
- [Wikipedia — Chronology](https://en.wikipedia.org/wiki/Chronology_(video_game)) · [The Messenger](https://en.wikipedia.org/wiki/The_Messenger_(2018_video_game))
- [Nintendo Life — YesterMorrow](https://www.nintendolife.com/news/2020/11/time-travelling_2d_platformer_yestermorrow_launches_on_switch_this_week)
- [Gamingscan — Best Time Travel Games](https://www.gamingscan.com/best-time-travel-games/)
- [itch.io — платформеры с тегом time-travel](https://itch.io/games/genre-platformer/tag-time-travel)

**О надёжности.** Утверждения о SUPERHOT, Braid (реализация) и alt-ctrl методологии
опираются на первичные источники (доклады самих разработчиков, код). Разборы
Dishonored 2, Titanfall 2, Chronosphere и Crankin — игровая пресса и комьюнити-разборы
(вторичные источники, подтверждены независимой корроборацией при верификации).
Деталь о реализации Titanfall 2 «двумя смещёнными уровнями» — комментарий на MapCore
со ссылкой на материалы о создании уровня, не прямое заявление Respawn.
