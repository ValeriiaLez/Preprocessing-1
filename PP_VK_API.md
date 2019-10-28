
## VK API

API -- an application programming interface, an interface or communication protocol between a client and a server intended to simplify the building of client-side software. The client makes a request in a specific format, they get a response in a specific format or initiate a defined action.

Twitter, VK, YouTube etc. have APIs -- great for us, since we, as linguists, are interested in the live data. Today we will study the VK API.

* The VK API documentation: https://vk.com/dev/openapi

* VK API was originally developed so that different web-applications can interact with VK, we will be using it for downloading the data

* vk.com has special pages that handle automatic requests

* Remember how we were downloading stuff from the Internet?


```python
import urllib.request  # importing the module
req = urllib.request.Request('https://habrahabr.ru/') # sending a request
with urllib.request.urlopen(req) as response: # opening a connection with the web-page
   html = response.read().decode('utf-8') # reading the response into the html variable
print(html[:210])
```

    <!DOCTYPE html>
    <html lang="ru" class="no-js">
      <head>
        <meta http-equiv="content-type" content="text/html; charset=utf-8" />
    <meta content='width=1024' name='viewport'>
    <title>Лучшие публикации за сутки / 
    

* To interact with vk.com, we will be using the same module -- urllib.request, the pages that we will be sending our requests to are described in the documentation of the VK API.

* In our requests we will have to specify certain parameters.

* First, we specify the page: https://api.vk.com/method/wall.get 

* Then, after a `?`, we include the parameters (key=value pairs).

* For example, https://api.vk.com/method/wall.get?owner_id=1 -- here the `owner_id` parameter is set to `1` -- the id of the user we are interested in -- https://vk.com/id1

* To join multiple parameters, use the `&`: https://api.vk.com/method/wall.get?owner_id=1&count=10 -- here the `count` parameter is set to `10` which means that we want to download 10 posts from the owner's wall.

* You will also need an access token. You can get it [here](https://vk.com/login?u=2&to=YXBwcz9hY3Q9bWFuYWdl).

* The version of the API -- the `v` parameter -- https://vk.com/dev/versions -- e.g., `v=5.92`

* Let's play with the VK API. First, let's download 20 posts from the Durov's wall using the `wall.get` method (the list of all the methods -- https://vk.com/dev/methods):


```python
import urllib.request 
req = urllib.request.Request('https://api.vk.com/method/wall.get?owner_id=1&count=20&v=5.92&access_token=8423c2448423c2448423c244d08441f2a1884238423c244dee1644d9e90529494134bf8') 
response = urllib.request.urlopen(req) 
result = response.read().decode('utf-8')
```


```python
print(result)
```

    {"response":{"count":283,"items":[{"id":2442097,"from_id":1,"owner_id":1,"date":1525805964,"post_type":"post","text":"Иногда говорят, что Telegram был заблокирован в России, так как “закон есть закон”. Однако Telegram заблокирован в России как раз вопреки главному закону страны – Конституции. Решения судов и законы, противоречащие Конституции, не имеют силы. А это значит, что и сама блокировка Telegram незаконна. \n\nЕсли бы ФСБ ограничилась запросом информации о нескольких террористах, то ее требование вписывалось бы в рамки Конституции. Однако речь идет о передаче универсальных ключей шифрования с целью последующего бесконтрольного доступа к переписке неограниченного круга лиц. A это – прямое нарушение 23-й статьи Конституции о праве каждого на тайну переписки.\n\nПо этой причине юристы из “Агоры” сегодня обжаловали решение Верховного суда России о законности приказа ФСБ. Надеюсь, власти России откажутся от языка неисполнимых ультиматумов, на котором сегодня ведется диалог с технологическими компаниями.\n\nНезависимо от этого, мы продолжим борьбу за Telegram в России. История наших предков учит биться до победного конца. \n\nС Днем Победы!","post_source":{"type":"vk"},"comments":{"count":388139,"can_post":1,"groups_can_post":true},"likes":{"count":152024,"user_likes":0,"can_like":1,"can_publish":1},"reposts":{"count":3367,"user_reposted":0},"views":{"count":8407358}},{"id":2431591,"from_id":1,"owner_id":1,"date":1525352753,"post_type":"post","text":"Михаил Светов, организатор прошедшего митинга за свободу интернета, объявил конкурс на наиболее вдохновляющую обработку видеоматериалов с митинга. Призовой фонд – 1 биткоин.\n\n#digitalresistance","attachments":[{"type":"video","video":{"id":456239033,"owner_id":1,"title":"КОНКУРС НА БИТКОИН","duration":113,"description":"Мне пришёл целевой анонимный донат на проведение конкурса. Разыгрываю целый биткоин [не кликбейт, на самом деле].\n\nКонкурс на лучшую видео и аудио обработку речей и кадров с митинга 30 апреля. Подходит любой формат, главное, в максимально мемичной форме распространить основные тезисы наших выступлений по интернету, и обратить внимание на критическую значимость блокировок. Все слова сказаны. Их нужно донести. Срок — 10 дней. Постите свои видео с хэштегом #digitalresistance во всех соцсетях и присылайте ссылк","date":1525352754,"comments":120,"views":42456,"local_views":42456,"photo_130":"https:\/\/sun1-89.userapi.com\/c840722\/v840722964\/8039f\/kunM7m6I7w4.jpg","photo_320":"https:\/\/sun1-26.userapi.com\/c840722\/v840722964\/803a1\/OGFig-5UNjY.jpg","photo_640":"https:\/\/sun1-23.userapi.com\/c840722\/v840722964\/803a2\/T2SKhzbHheQ.jpg","photo_800":"https:\/\/sun1-23.userapi.com\/c840722\/v840722964\/803a2\/T2SKhzbHheQ.jpg","access_key":"b6751e4a53ef7bd286","platform":"YouTube","can_add":1,"track_code":"video_da87f69bmHodSzncSuDYrnr5c0YaNF6HsA6_d5nQQkYonwcB"}}],"post_source":{"type":"vk"},"comments":{"count":12992,"can_post":1,"groups_can_post":true},"likes":{"count":18349,"user_likes":0,"can_like":1,"can_publish":1},"reposts":{"count":283,"user_reposted":0},"views":{"count":4190227}},{"id":2422169,"from_id":1,"owner_id":1,"date":1525187997,"post_type":"post","text":"","attachments":[{"type":"photo","photo":{"id":456316241,"album_id":-7,"owner_id":1,"sizes":[{"type":"m","url":"https:\/\/sun1-84.userapi.com\/c623900\/v623900095\/1160af\/p5M94AlMuIk.jpg","width":130,"height":97},{"type":"o","url":"https:\/\/sun1-28.userapi.com\/c623900\/v623900095\/1160b3\/VZ8lWO9IliA.jpg","width":130,"height":98},{"type":"p","url":"https:\/\/sun1-83.userapi.com\/c623900\/v623900095\/1160b4\/zNdk9cy2yB8.jpg","width":200,"height":150},{"type":"q","url":"https:\/\/sun1-85.userapi.com\/c623900\/v623900095\/1160b5\/IuFfBtlIc9o.jpg","width":320,"height":240},{"type":"r","url":"https:\/\/sun1-83.userapi.com\/c623900\/v623900095\/1160b6\/9vODfb2MJ8o.jpg","width":510,"height":382},{"type":"s","url":"https:\/\/sun1-19.userapi.com\/c623900\/v623900095\/1160ae\/4oqrxkIA8sU.jpg","width":75,"height":56},{"type":"x","url":"https:\/\/sun1-88.userapi.com\/c623900\/v623900095\/1160b0\/lKYaPpXh0sI.jpg","width":604,"height":453},{"type":"y","url":"https:\/\/sun1-28.userapi.com\/c623900\/v623900095\/1160b1\/bu7-9BElh6g.jpg","width":807,"height":605},{"type":"z","url":"https:\/\/sun1-94.userapi.com\/c623900\/v623900095\/1160b2\/39ZyjmEB_1Y.jpg","width":1279,"height":959}],"text":"","date":1525187973,"access_key":"882117b1daeb20d383"}}],"post_source":{"type":"vk"},"comments":{"count":9685,"can_post":1,"groups_can_post":true},"likes":{"count":86813,"user_likes":0,"can_like":1,"can_publish":1},"reposts":{"count":1331,"user_reposted":0},"views":{"count":5838943}},{"id":2418560,"from_id":1,"owner_id":1,"date":1525168885,"post_type":"post","text":"Наблюдаю, как несмотря на проливной дождь, по Невскому проспекту в данный момент движется огромная колонна, которая скандирует лозунги в защиту свободного интернета. Подобное сочетание природных условий и энергии людей возможно только в Петербурге. \n\nОбновлено: спасибо петербуржцам за стойкость и смелость.\n#digitalresistance","post_source":{"type":"vk"},"comments":{"count":6689,"can_post":1,"groups_can_post":true},"likes":{"count":39523,"user_likes":0,"can_like":1,"can_publish":1},"reposts":{"count":444,"user_reposted":0},"views":{"count":5431326}},{"id":2412029,"from_id":1,"owner_id":1,"date":1525107823,"post_type":"post","text":"Потрясающая акция в Москве. Более 12,000 человек выступили за свободный интернет. Спасибо каждому, кто нашел время, – мы в Telegram очень ценим эту поддержку. \n\nПоразила пассионарность спикеров – такие речи создают историю стран. https:\/\/www.youtube.com\/watch?v=D9dPg3ofmyQ\n\nНеважно, прислушаются ли сейчас власти России к голосу общества. Важно, что мы всегда будем продолжать отстаивать те ценности, в которые верим.\n\nПомните: завтра – 1 мая – шествие и митинг в Петербурге.","attachments":[{"type":"video","video":{"id":456239027,"owner_id":1,"title":"НЕ СДАДИМ ИНТЕРНЕТ - РЕЖИМУ ЛЮСТРАЦИЯ! : СВЕТОВ","duration":469,"description":"Выступление Михаила Светов на митинге \"Против Роскомнадзора и блокировки Telegram\" в Москве","date":1525107823,"comments":303,"views":31931,"local_views":31931,"photo_130":"https:\/\/sun1-83.userapi.com\/c834303\/v834303343\/12d44f\/DOiNeG_3DDU.jpg","photo_320":"https:\/\/sun1-84.userapi.com\/c834303\/v834303343\/12d451\/etCrt-Y8waQ.jpg","photo_640":"https:\/\/sun1-89.userapi.com\/c834303\/v834303343\/12d452\/hjIAImcvr-I.jpg","photo_800":"https:\/\/sun1-89.userapi.com\/c834303\/v834303343\/12d452\/hjIAImcvr-I.jpg","access_key":"adcc1fa1c7c69bad50","platform":"YouTube","can_add":1,"track_code":"video_2e49fbb5GjRpm4uSwElYi2J8yz3s9FiLFwXKSrR5arUb6lh_"}}],"post_source":{"type":"vk"},"comments":{"count":5306,"can_post":1,"groups_can_post":true},"likes":{"count":24715,"user_likes":0,"can_like":1,"can_publish":1},"reposts":{"count":928,"user_reposted":0},"views":{"count":2859556}},{"id":2407925,"from_id":1,"owner_id":1,"date":1525090324,"post_type":"post","text":"Тысячи молодых и прогрессивных людей в данный момент выступают в защиту свободы интернета в Москве. Тысячи еще продолжают подходить.\n\nЭто беспрецедентно. Я горжусь тем, что родился в одной стране с этими людьми. \n\nВаша энергия меняет мир.\n\n#digitalresistance","attachments":[{"type":"photo","photo":{"id":456315566,"album_id":-7,"owner_id":1,"sizes":[{"type":"m","url":"https:\/\/sun1-22.userapi.com\/c846021\/v846021276\/38d2a\/4BaEsjAZFiQ.jpg","width":130,"height":97},{"type":"o","url":"https:\/\/sun1-30.userapi.com\/c846021\/v846021276\/38d2e\/8aQ5ji7H98g.jpg","width":130,"height":98},{"type":"p","url":"https:\/\/sun1-29.userapi.com\/c846021\/v846021276\/38d2f\/SQQCW_QJNJI.jpg","width":200,"height":150},{"type":"q","url":"https:\/\/sun1-84.userapi.com\/c846021\/v846021276\/38d30\/GVGyP_ffBCE.jpg","width":320,"height":240},{"type":"r","url":"https:\/\/sun1-16.userapi.com\/c846021\/v846021276\/38d31\/xn5JdZycJyk.jpg","width":510,"height":383},{"type":"s","url":"https:\/\/sun1-92.userapi.com\/c846021\/v846021276\/38d29\/wjurvCxIBF0.jpg","width":75,"height":56},{"type":"x","url":"https:\/\/sun1-86.userapi.com\/c846021\/v846021276\/38d2b\/nW8A1lSGHqs.jpg","width":604,"height":453},{"type":"y","url":"https:\/\/sun1-89.userapi.com\/c846021\/v846021276\/38d2c\/lxprfpdEWMY.jpg","width":807,"height":605},{"type":"z","url":"https:\/\/sun1-21.userapi.com\/c846021\/v846021276\/38d2d\/ybgiwGxzjnQ.jpg","width":1280,"height":960}],"text":"","date":1525089150,"access_key":"81ccd0f9fc969bdb01"}}],"post_source":{"type":"vk"},"comments":{"count":9533,"can_post":1,"groups_can_post":true},"likes":{"count":81901,"user_likes":0,"can_like":1,"can_publish":1},"reposts":{"count":2237,"user_reposted":0},"views":{"count":5467183}},{"id":2405336,"from_id":1,"owner_id":1,"date":1525048713,"post_type":"post","text":"https:\/\/youtu.be\/FT6TVvAQ5OY\n\n30 апреля (понедельник) в Москве:\n\n13:00 – Сбор по адресу ул. Маши Порываевой, 38. \n14:00-15:00 – Шествие от ул. Маши Порываевой, 38, до пр. Академика Сахарова. \n15:00-16:00 – Митинг на пр. Академика Сахарова, 9.\n\nАналогичная акция в Петербурге – 1 мая.","attachments":[{"type":"video","video":{"id":456239026,"owner_id":1,"title":"МИТИНГ ЗА ТЕЛЕГРАМ","duration":172,"description":"30 АПРЕЛЯ, 14:00 ПРОСПЕКТ САХАРОВА, МОСКВА\n\nhttp:\/\/digitalresistance.moscow\n\nТвиттер https:\/\/twitter.com\/msvetov\n\nКанал в телеграме https:\/\/t.me\/mrlibertarian\n\nПаблик вконтакте http:\/\/vk.com\/svtvofficial\n\nЕсли вам нравится что я делаю, помогите каналу криптовалютой!\n\nBTC 154H8UAG9EgBPHNFuW8u6h56JdqpSsAYmS\nLTC LgAYmdCfta3csv7Ahi6pN1Rz4za48fViw6\nBCH 16VEgMz15eza5sjLyBZBLZuX5rBYX6zueJ\nDASH Xut9jPe5jbv1wbr394N6xfJNDoA2QEN7BG\nETH 0x0CbE5dC38a1f453547D67238680c250b8Ce58b40\nEOS. 0x0CbE5dC38a1f453547D67238680c250b8","date":1525048713,"comments":94,"views":22285,"local_views":22285,"photo_130":"https:\/\/sun1-84.userapi.com\/c834102\/v834102746\/12a32d\/YU4Nr613Cko.jpg","photo_320":"https:\/\/sun1-19.userapi.com\/c834102\/v834102746\/12a32f\/PPGGUKr4FRg.jpg","photo_640":"https:\/\/sun1-19.userapi.com\/c834102\/v834102746\/12a330\/B8cRHnhkI9I.jpg","photo_800":"https:\/\/sun1-19.userapi.com\/c834102\/v834102746\/12a330\/B8cRHnhkI9I.jpg","access_key":"234bba7361822a6d77","platform":"YouTube","can_add":1,"track_code":"video_b051474d3wZ2LAsvQnnje9AxKQge0BDSD6R6O8Y_Im2yQiml"}}],"post_source":{"type":"vk"},"comments":{"count":2716,"can_post":1,"groups_can_post":true},"likes":{"count":11101,"user_likes":0,"can_like":1,"can_publish":1},"reposts":{"count":291,"user_reposted":0},"views":{"count":1625066}},{"id":2401719,"from_id":1,"owner_id":1,"date":1525012261,"post_type":"post","text":"Видеозапись, присланная сторонниками акции #sundaypaperplane.","attachments":[{"type":"video","video":{"id":456239025,"owner_id":1,"title":"#sundaypaperplane","duration":59,"description":"Видео, присланное сторонниками акции #sundaypaperplane","date":1525009959,"comments":338,"views":3758450,"width":1280,"height":720,"photo_130":"https:\/\/sun1-25.userapi.com\/c834302\/v834302714\/127274\/cAAnK4yYfDk.jpg","photo_320":"https:\/\/sun1-93.userapi.com\/c834302\/v834302714\/127272\/fehorJva6Ek.jpg","photo_800":"https:\/\/sun1-86.userapi.com\/c834302\/v834302714\/127271\/aUePw7nN1Lg.jpg","first_frame_320":"https:\/\/sun1-21.userapi.com\/c845018\/v845018714\/3dc9d\/JOxOnDEXDYA.jpg","first_frame_160":"https:\/\/sun1-88.userapi.com\/c845018\/v845018714\/3dc9e\/SBl3ws19v_U.jpg","first_frame_130":"https:\/\/sun1-28.userapi.com\/c845018\/v845018714\/3dc9f\/m_iwRKEwSGo.jpg","first_frame_800":"https:\/\/sun1-16.userapi.com\/c845018\/v845018714\/3dc9c\/yPygF5p1t2M.jpg","access_key":"58a4fdf3bd91ac7ebb","can_add":1,"track_code":"video_119d0237OOK5VfLd4R1TlDNkMfVNNPEAF97sm4sl-TaOQfCm"}}],"post_source":{"type":"vk"},"comments":{"count":3603,"can_post":1,"groups_can_post":true},"likes":{"count":19940,"user_likes":0,"can_like":1,"can_publish":1},"reposts":{"count":459,"user_reposted":0},"views":{"count":7870452}},{"id":2401089,"from_id":1,"owner_id":1,"date":1525009304,"post_type":"post","text":"Завтра (30 апреля) в 14:00 в Москве на проспекте Сахарова состоится согласованный митинг за свободу интернета. Это исторический шанс для москвичей выразить общую позицию. Послезавтра может быть уже поздно.\n\nПоследние 2 недели мы вели неравный бой с интернет-цензором. Мы делали это ради вас – наших российских пользователей. Однако будущее российского интернета находится, в конечном счете, в ваших руках. \n\nКто-то скажет, что митинг ничего не изменит. Это не так. Россия находится на перепутье – полномасштабная цензура еще не была введена. Если бездействовать, Россия потеряет Telegram и другие популярные сервисы. Ваше активное участие может поменять ход истории.","copy_history":[{"id":8,"owner_id":-165675366,"from_id":-165675366,"date":1524755130,"post_type":"post","text":"Митинг против блокировки Telegram. Проспект Сахарова, 30 апреля, 14:00 — 16:00 \n \nБлокировка Telegram – это национальный позор: ни одно государство, претендующее на лидерство в XXI веке, не должно препятствовать развитию собственных технологий и цифровому прогрессу. \n \nРоскомнадзор нарушает нормы Конституции РФ и фундаментальные права и свободы человека. Блокировки, цензура и уголовные преследования за лайки и репосты недопустимы. Единственными реальными результатами «блокировки» будут только рост угрозы национальной безопасности, долгосрочный ущерб экономике и изоляция России от прогресса. \n \nМетоды, которыми власть «развивает интернет» и новые законы о соцсетях не оставляют надежд, что ситуация разрешится сама собой. \n \nЕсли вы используете Telegram, поддерживаете свободу слова, вас достали блокировки, вы за свободный интернет и цифровой прогресс — приходите на митинг. \n \n30 апреля, 14:00. проспект академика Сахарова. Сбор с 13:00 по адресу: ул. Маши Порываевой, 38). Не забудьте пару бумажных самолетиков! \n \nМитинг организовывается Либертарианской партией России. Согласовано с мэрией Москвы. \n \n• Поддержать нас рублем: http:\/\/digitalresistance.moscow \n• Наши ивенты в VK и в FB \n• По вопросам участия в организации и для обратной связи пишите на info@libertarian-party.ru или в бота обратной связи: @digitalresistance_moscow","attachments":[{"type":"link","link":{"url":"https:\/\/vk.com\/app5575136_-165675366","title":"Митинг за свободу интернета #DigitalResistance","caption":"Application","description":"Вся информация: digitalresistance.moscow","photo":{"id":456242045,"album_id":-2,"owner_id":100,"sizes":[{"type":"m","url":"https:\/\/sun1-30.userapi.com\/c840334\/v840334770\/7b6e9\/pi8vUUo_Atw.jpg","width":130,"height":58},{"type":"o","url":"https:\/\/sun1-25.userapi.com\/c840334\/v840334770\/7b6ed\/ivETWN2O51g.jpg","width":130,"height":87},{"type":"p","url":"https:\/\/sun1-87.userapi.com\/c840334\/v840334770\/7b6ee\/35N6X4AgvfQ.jpg","width":200,"height":133},{"type":"q","url":"https:\/\/sun1-23.userapi.com\/c840334\/v840334770\/7b6ef\/ZPjm2XSfdm4.jpg","width":320,"height":213},{"type":"r","url":"https:\/\/sun1-23.userapi.com\/c840334\/v840334770\/7b6f0\/FLnQB4mgddA.jpg","width":510,"height":340},{"type":"s","url":"https:\/\/sun1-18.userapi.com\/c840334\/v840334770\/7b6e8\/PYpIpkn41pQ.jpg","width":75,"height":33},{"type":"x","url":"https:\/\/sun1-87.userapi.com\/c840334\/v840334770\/7b6ea\/vbFs7yBS3Ck.jpg","width":604,"height":270},{"type":"y","url":"https:\/\/sun1-84.userapi.com\/c840334\/v840334770\/7b6eb\/CrCbFu7DoeM.jpg","width":807,"height":361},{"type":"z","url":"https:\/\/sun1-84.userapi.com\/c840334\/v840334770\/7b6ec\/cuTc-FyX2CA.jpg","width":1280,"height":573}],"text":"","date":1524755117},"button":{"title":"Open","action":{"type":"open_url","url":"https:\/\/vk.com\/app5575136_-165675366"}}}}],"post_source":{"type":"vk"}}],"post_source":{"type":"vk"},"comments":{"count":2184,"can_post":1,"groups_can_post":true},"likes":{"count":21127,"user_likes":0,"can_like":1,"can_publish":1},"reposts":{"count":956,"user_reposted":0},"views":{"count":1966020}},{"id":2389655,"from_id":1,"owner_id":1,"date":1524838659,"post_type":"post","text":"https:\/\/www.youtube.com\/watch?v=FCbPGhUxDiQ\n(при просмотре нужно включить русские субтитры)","attachments":[{"type":"video","video":{"id":456239024,"owner_id":1,"title":"Совещание в РКН","duration":240,"description":"Включите русские субтитры!","date":1524838659,"comments":587,"views":187028,"local_views":187028,"photo_130":"https:\/\/sun1-90.userapi.com\/c844521\/v844521881\/3be8f\/CAs8vZb_b8I.jpg","photo_320":"https:\/\/sun1-18.userapi.com\/c844521\/v844521881\/3be91\/XEPyjlFQ_Y4.jpg","photo_640":"https:\/\/sun1-88.userapi.com\/c844521\/v844521881\/3be92\/AxXaeifW8_w.jpg","photo_800":"https:\/\/sun1-88.userapi.com\/c844521\/v844521881\/3be92\/AxXaeifW8_w.jpg","access_key":"d41f154fa71177c8fb","platform":"YouTube","can_add":1,"track_code":"video_2d503459zlOBsmAkDpfT_oGqtw4r9tM5GZLX5QNdYnn6_MyP"}}],"post_source":{"type":"vk"},"comments":{"count":9350,"can_post":1,"groups_can_post":true},"likes":{"count":47499,"user_likes":0,"can_like":1,"can_publish":1},"reposts":{"count":3031,"user_reposted":0},"views":{"count":2941285}},{"id":2382822,"from_id":1,"owner_id":1,"date":1524761880,"post_type":"post","text":"11-й день продолжаются попытки блокировать Telegram на территории России. Многие спрашивают, возможен ли был некий компромисс. Думаю, что едва ли.\n\nКлючи для расшифровки переписки всех своих пользователей ни Telegram, ни другие мессенджеры, не могли бы выдать при всем желании. Это обусловлено техническими особенностями шифрования в 2018 году.\n\nДаже если бы запрос ФСБ ограничивался помощью в поимке 6 террористов, участвовавших в теракте в Петербурге, мы вряд ли могли быть полезны: часть интересующих ФСБ мобильных номеров никогда не имели аккаунта в Telegram, другая их часть была автоматически удалена за неактивностью еще в прошлом году. \n\nВпрочем, согласно материалам дела, ставшим доступными Republic.ru в октябре, для координации теракта в большей степени использовался не Telegram, а WhatsApp.","post_source":{"type":"vk"},"comments":{"count":6958,"can_post":1,"groups_can_post":true},"likes":{"count":37351,"user_likes":0,"can_like":1,"can_publish":1},"reposts":{"count":1066,"user_reposted":0},"views":{"count":4470808}},{"id":2358781,"from_id":1,"owner_id":1,"date":1524440871,"post_type":"post","text":"Эту неделю мы боролись не с Роскомнадзором или ФСБ. Мы боролись за цифровое будущее России. Свободный интернет и оконечное шифрование – неотъемлемые части этого будущего. \n\nНи одна развитая страна не блокирует мессенджеры за отказ выдать спецслужбам ключи шифрования. Отмена права на конфиденциальность – лекарство, которое опаснее самой болезни. \n\nКак только некая служба получает возможность бесконтрольно мониторить личную переписку граждан, очень скоро этот доступ оказывается в руках у третьих сторон – взяткодателей, хакеров, агентов других государств. В результате требование предоставить универсальные пути обхода шифрования через выдачу “ключей” снижает информационную безопасность как элит, так и общества в целом.\n\nP. S. Если у Вас есть инсайды о причинах, планах и методах блокировки, сообщайте нам по адресу arequest2@gmail.com.","post_source":{"type":"vk"},"comments":{"count":15148,"can_post":1,"groups_can_post":true},"likes":{"count":47828,"user_likes":0,"can_like":1,"can_publish":1},"reposts":{"count":1671,"user_reposted":0},"views":{"count":4567700}},{"id":2358485,"from_id":1,"owner_id":1,"date":1524439551,"post_type":"post","text":"Огромное спасибо жителям десятков городов России за поддержку свободного интернета. \n\nВидеоролики с прошедшей акции предлагаю выкладывать под хэштегом #sundaypaperplane во всех соцсетях.\n\nСледующий раз? Воскресенье, 29 апреля в 19:00 по местному времени.","attachments":[{"type":"video","video":{"id":456239442,"owner_id":-6726778,"title":"«Смотри, как летит!» Как прошла акция в поддержку Telegram","duration":59,"description":"Сегодня Telegram разослал уведомления: «Если вы поддерживаете свободный интернет, запустите из окна бумажный самолетик сегодня ровно в 7 вечера». Вот, что из этого вышло","date":1524423074,"comments":0,"views":6955347,"width":1920,"height":1080,"photo_130":"https:\/\/sun1-14.userapi.com\/c844320\/v844320005\/3501b\/l0ZyprH86uA.jpg","photo_320":"https:\/\/sun1-23.userapi.com\/c844320\/v844320005\/35019\/vZwfgZWMf5Q.jpg","photo_800":"https:\/\/sun1-90.userapi.com\/c844320\/v844320005\/35018\/kcpAsbrL250.jpg","first_frame_320":"https:\/\/sun1-24.userapi.com\/c847020\/v847020484\/2e434\/zwfKl2_dY4k.jpg","first_frame_160":"https:\/\/sun1-86.userapi.com\/c847020\/v847020484\/2e435\/ibEkU5wC1NY.jpg","first_frame_130":"https:\/\/sun1-24.userapi.com\/c847020\/v847020484\/2e436\/DS96-esVSxU.jpg","first_frame_800":"https:\/\/sun1-83.userapi.com\/c847020\/v847020484\/2e433\/7c-xI13cYeQ.jpg","access_key":"44088de20a1d3dd9b7","can_add":1,"track_code":"video_d069a2e9y73R_PiNOcz5yk3SZg2V1Elur18t_a7TeolCg4_bnhzJr_zKzw"}}],"post_source":{"type":"vk"},"comments":{"count":5852,"can_post":1,"groups_can_post":true},"likes":{"count":38329,"user_likes":0,"can_like":1,"can_publish":1},"reposts":{"count":1067,"user_reposted":0},"views":{"count":7448006}},{"id":2348522,"from_id":1,"owner_id":1,"date":1524402346,"post_type":"post","text":"Мы продержались 7 дней под самым масштабным актом интернет-цензуры за историю России.\n\nВсех, кто поддерживает свободный интернет, призываем запустить из окна бумажный самолетик сегодня ровно в 7 вечера по местному времени.\n\nЧерез час после акции имеет смысл устроить небольшой субботник – собрать те самолетики, которые Вы найдете у Вашего дома. \n\nСпасибо за поддержку. Эта неделя останется в истории.","attachments":[{"type":"photo","photo":{"id":456311287,"album_id":-7,"owner_id":1,"sizes":[{"type":"m","url":"https:\/\/sun9-41.userapi.com\/c840331\/v840331315\/7980a\/elqYxlBXDt4.jpg","width":109,"height":130},{"type":"o","url":"https:\/\/sun9-14.userapi.com\/c840331\/v840331315\/7980f\/mi_6yzkjOgk.jpg","width":130,"height":155},{"type":"p","url":"https:\/\/sun9-38.userapi.com\/c840331\/v840331315\/79810\/gZWd0AydnT0.jpg","width":200,"height":238},{"type":"q","url":"https:\/\/sun9-37.userapi.com\/c840331\/v840331315\/79811\/GMuDaXj73zc.jpg","width":320,"height":381},{"type":"r","url":"https:\/\/sun9-61.userapi.com\/c840331\/v840331315\/79812\/L3RbhPkNcTA.jpg","width":510,"height":607},{"type":"s","url":"https:\/\/sun9-64.userapi.com\/c840331\/v840331315\/79809\/wemzIrvo93Q.jpg","width":63,"height":75},{"type":"w","url":"https:\/\/sun9-55.userapi.com\/c840331\/v840331315\/7980e\/kp8MdNLCQIk.jpg","width":1816,"height":2160},{"type":"x","url":"https:\/\/sun9-6.userapi.com\/c840331\/v840331315\/7980b\/wEMNpAbN5Ac.jpg","width":507,"height":604},{"type":"y","url":"https:\/\/sun9-12.userapi.com\/c840331\/v840331315\/7980c\/dEI_cC4qgZY.jpg","width":678,"height":807},{"type":"z","url":"https:\/\/sun9-34.userapi.com\/c840331\/v840331315\/7980d\/Ph9yi54v5FI.jpg","width":908,"height":1080}],"text":"","date":1524406529,"access_key":"e8d2843ab80866361c"}},{"type":"photo","photo":{"id":456311217,"album_id":-7,"owner_id":1,"sizes":[{"type":"m","url":"https:\/\/sun1-17.userapi.com\/c845216\/v845216315\/33ec9\/l_0acnvR2Lw.jpg","width":130,"height":130},{"type":"o","url":"https:\/\/sun1-91.userapi.com\/c845216\/v845216315\/33ece\/ZaHA5l-UQ9s.jpg","width":130,"height":130},{"type":"p","url":"https:\/\/sun1-20.userapi.com\/c845216\/v845216315\/33ecf\/lVgexBBK4iA.jpg","width":200,"height":200},{"type":"q","url":"https:\/\/sun1-19.userapi.com\/c845216\/v845216315\/33ed0\/ovUJ9nyzqc4.jpg","width":320,"height":320},{"type":"r","url":"https:\/\/sun1-18.userapi.com\/c845216\/v845216315\/33ed1\/-6cnhavwq6Q.jpg","width":510,"height":510},{"type":"s","url":"https:\/\/sun1-27.userapi.com\/c845216\/v845216315\/33ec8\/nMXu21wxVL8.jpg","width":75,"height":75},{"type":"w","url":"https:\/\/sun1-85.userapi.com\/c845216\/v845216315\/33ecd\/8y5bkHbPrO4.jpg","width":1276,"height":1276},{"type":"x","url":"https:\/\/sun1-87.userapi.com\/c845216\/v845216315\/33eca\/f1QfPVeYCfg.jpg","width":604,"height":604},{"type":"y","url":"https:\/\/sun1-84.userapi.com\/c845216\/v845216315\/33ecb\/ccP98flufCc.jpg","width":807,"height":807},{"type":"z","url":"https:\/\/sun1-16.userapi.com\/c845216\/v845216315\/33ecc\/zJ6-nZvpO8A.jpg","width":1080,"height":1080}],"text":"","date":1524405864,"access_key":"16c7801b5c9f97c4a5"}}],"post_source":{"type":"vk"},"comments":{"count":9016,"can_post":1,"groups_can_post":true},"likes":{"count":89539,"user_likes":0,"can_like":1,"can_publish":1},"reposts":{"count":2670,"user_reposted":0},"views":{"count":4457657}},{"id":2331162,"from_id":1,"owner_id":1,"date":1524147382,"post_type":"post","text":"Telegram продолжает оставаться доступным российским пользователям, несмотря на блокировку властями РФ более 18 миллионов IP-адресов за последние 4 дня. \n\nСпасибо всем, кто участвует в Цифровом Сопротивлении. Все больше IT-предпринимателей, программистов, системных администраторов делом помогают обеспечивать гарантированные Конституцией права россиян.","post_source":{"type":"vk"},"comments":{"count":13244,"can_post":1,"groups_can_post":true},"likes":{"count":88176,"user_likes":0,"can_like":1,"can_publish":1},"reposts":{"count":1906,"user_reposted":0},"views":{"count":5225750}},{"id":2307813,"from_id":1,"owner_id":1,"date":1523971038,"post_type":"post","text":"Спасибо за поддержку и преданность Telegram – вместе нам удалось пережить первые 24 часа блокировки.\n\nКак показали последние сутки, в своей войне с прогрессом надзорные органы России готовы блокировать миллионы IP-адресов облачных хостингов, не считаясь с потерями посторонних проектов. \n\nПомимо этого, власти России борются и с независимыми сервисами proxy\/VPN, многие из которых перестают работать (если это произошло, отключите прокси в настройках Telegram и попробуйте найти другой).\n\nХотя российский рынок не составляет существенной доли пользовательской базы Telegram, он важен нам по личным соображениям. \n\nВ рамках Цифрового Сопротивления – децентрализованного движения в защиту цифровых свобод и прогресса – я начал выплачивать биткоин-гранты администраторам proxy и vpn. В течение этого года буду рад пожертвовать миллионы долларов личных средств на эти цели. Призываю всех присоединяться и участвовать – настройкой прокси\/vpn серверов или их финансированием.","post_source":{"type":"vk"},"comments":{"count":19469,"can_post":1,"groups_can_post":true},"likes":{"count":173108,"user_likes":0,"can_like":1,"can_publish":1},"reposts":{"count":4693,"user_reposted":0},"views":{"count":7057472}},{"id":2296940,"from_id":1,"owner_id":1,"date":1523881233,"post_type":"post","text":"Сегодня утром власти России начали блокировать Telegram, поэтому на некоторых операторах связи сервис может работать нестабильно. Последствия блокировки: \n\n1. Качество жизни 15 миллионов россиян ухудшится, так как Telegram без VPN может быть временами недоступен. \n\n2. Террористическая угроза в России останется на прежнем уровне, так как экстремисты продолжат пользоваться шифрованными каналами связи – в других мессенджерах, либо через VPN.\n\n3. Национальная безопасность России снизится, так как часть личных данных россиян перейдет из нейтральной к РФ площадки в контролируемые из США WhatsApp\/Facebook. \n\nМы считаем решение о блокировке антиконституционным и продолжим отстаивать право на тайну переписки россиян. ✊🏼","post_source":{"type":"vk"},"comments":{"count":12333,"can_post":1,"groups_can_post":true},"likes":{"count":160402,"user_likes":0,"can_like":1,"can_publish":1},"reposts":{"count":4625,"user_reposted":0},"views":{"count":6582593}},{"id":2285269,"from_id":1,"owner_id":1,"date":1523619298,"post_type":"post","text":"Таганский суд Москвы вынес решение о блокировке Telegram на территории РФ. Что стоит иметь в виду пользователям:\n\n1. Telegram будет использовать встроенные методы обхода блокировок, которые не требуют действий от пользователей, однако 100%-ая доступность сервиса без VPN не гарантирована.\n2. В первые часы блокировки сторонние VPN\/Proxy-сервисы могут быть перегружены и с большой вероятностью будут работать медленно.\n3. Независимо от наличия блокировки, Telegram сохранит возможность централизованно рассылать уведомления всем российским пользователям, информируя о развитии ситуации. \n\nВажно: не удаляйте и не переустанавливайте Telegram при возникновении проблем со связью. Старайтесь своевременно скачивать обновления Telegram в AppStore или Google Play.\n\n💪","post_source":{"type":"vk"},"comments":{"count":11751,"can_post":1,"groups_can_post":true},"likes":{"count":106713,"user_likes":0,"can_like":1,"can_publish":1},"reposts":{"count":5229,"user_reposted":0},"views":{"count":6607659}},{"id":2236210,"from_id":1,"owner_id":1,"date":1519549711,"post_type":"post","text":"","copy_history":[{"id":30344,"owner_id":-35769930,"from_id":-35769930,"date":1519520066,"post_type":"post","text":"Сегодня ВКонтакте запустил набор «Election girl», полностью срисовав стикеры с моих. Получилось, правда, не очень, но не отчаивайся, дорогой автор! Пару лет срисовки моих стикеров и ты станешь даже вполне себе ничего - у меня их очень много. 😌\n\nХочешь по-взрослому? Работай сам, а не сиди на чужой шее, как пиявка. По иронии судьбы этот набор посвящен выборам и призывает повзрослеть. \n\nОригинальный набор тут: t.me\/addstickers\/pinup_girl\n💕","attachments":[{"type":"photo","photo":{"id":456239215,"album_id":-7,"owner_id":-35769930,"user_id":100,"sizes":[{"type":"m","url":"https:\/\/sun1-22.userapi.com\/c824503\/v824503538\/cfa91\/lkMea8ehuJA.jpg","width":130,"height":92},{"type":"o","url":"https:\/\/sun1-25.userapi.com\/c824503\/v824503538\/cfa93\/0ek4PTEofLw.jpg","width":130,"height":92},{"type":"p","url":"https:\/\/sun1-30.userapi.com\/c824503\/v824503538\/cfa94\/NjaGxeohRBk.jpg","width":200,"height":141},{"type":"q","url":"https:\/\/sun1-93.userapi.com\/c824503\/v824503538\/cfa95\/i1UwI5nop2s.jpg","width":320,"height":226},{"type":"r","url":"https:\/\/sun1-14.userapi.com\/c824503\/v824503538\/cfa96\/AQlm-6NOxyM.jpg","width":510,"height":360},{"type":"s","url":"https:\/\/sun1-25.userapi.com\/c824503\/v824503538\/cfa90\/EreWNC9mgj4.jpg","width":75,"height":53},{"type":"x","url":"https:\/\/sun1-26.userapi.com\/c824503\/v824503538\/cfa92\/zCbJn0iygCE.jpg","width":524,"height":370}],"text":"","date":1519520066,"access_key":"a48f44fbbab4802f8c"}},{"type":"photo","photo":{"id":456239216,"album_id":-7,"owner_id":-35769930,"user_id":100,"sizes":[{"type":"m","url":"https:\/\/sun1-94.userapi.com\/c824503\/v824503538\/cfa8a\/vltV2SSpc7E.jpg","width":130,"height":92},{"type":"o","url":"https:\/\/sun1-86.userapi.com\/c824503\/v824503538\/cfa8c\/UXtsy0gRq0c.jpg","width":130,"height":92},{"type":"p","url":"https:\/\/sun1-90.userapi.com\/c824503\/v824503538\/cfa8d\/a3RTr4JKGMs.jpg","width":200,"height":141},{"type":"q","url":"https:\/\/sun1-16.userapi.com\/c824503\/v824503538\/cfa8e\/v74fHOaKrhs.jpg","width":320,"height":226},{"type":"r","url":"https:\/\/sun1-17.userapi.com\/c824503\/v824503538\/cfa8f\/YjvF6eslIzk.jpg","width":510,"height":360},{"type":"s","url":"https:\/\/sun1-14.userapi.com\/c824503\/v824503538\/cfa89\/p71fhfZ8-Mo.jpg","width":75,"height":53},{"type":"x","url":"https:\/\/sun1-29.userapi.com\/c824503\/v824503538\/cfa8b\/oBN7hoNR1xQ.jpg","width":524,"height":370}],"text":"","date":1519520066,"access_key":"17d876b8a46e3223fc"}},{"type":"photo","photo":{"id":456239217,"album_id":-7,"owner_id":-35769930,"user_id":100,"sizes":[{"type":"m","url":"https:\/\/sun1-18.userapi.com\/c824503\/v824503538\/cfa98\/Dx2fJmedw5U.jpg","width":130,"height":92},{"type":"o","url":"https:\/\/sun1-94.userapi.com\/c824503\/v824503538\/cfa9a\/W1epMq1GSC0.jpg","width":130,"height":92},{"type":"p","url":"https:\/\/sun1-16.userapi.com\/c824503\/v824503538\/cfa9b\/Z8OwHC2TJnU.jpg","width":200,"height":141},{"type":"q","url":"https:\/\/sun1-93.userapi.com\/c824503\/v824503538\/cfa9c\/jY2jzQrvdZk.jpg","width":320,"height":226},{"type":"r","url":"https:\/\/sun1-83.userapi.com\/c824503\/v824503538\/cfa9d\/2nMv6Ehaqn4.jpg","width":510,"height":360},{"type":"s","url":"https:\/\/sun1-90.userapi.com\/c824503\/v824503538\/cfa97\/9MBiG28Ht1c.jpg","width":75,"height":53},{"type":"x","url":"https:\/\/sun1-85.userapi.com\/c824503\/v824503538\/cfa99\/OKrx6uAzo7Y.jpg","width":524,"height":370}],"text":"","date":1519520066,"access_key":"7a16532dfd9dd87ab2"}},{"type":"photo","photo":{"id":456239218,"album_id":-7,"owner_id":-35769930,"user_id":100,"sizes":[{"type":"m","url":"https:\/\/sun1-16.userapi.com\/c824503\/v824503538\/cfa83\/p-699MHN-JA.jpg","width":130,"height":92},{"type":"o","url":"https:\/\/sun1-91.userapi.com\/c824503\/v824503538\/cfa85\/2dk7AuAFfYU.jpg","width":130,"height":92},{"type":"p","url":"https:\/\/sun1-29.userapi.com\/c824503\/v824503538\/cfa86\/62JtBBTJYHY.jpg","width":200,"height":141},{"type":"q","url":"https:\/\/sun1-94.userapi.com\/c824503\/v824503538\/cfa87\/SlmnZNj1Pks.jpg","width":320,"height":226},{"type":"r","url":"https:\/\/sun1-86.userapi.com\/c824503\/v824503538\/cfa88\/xVIMW5MqVBE.jpg","width":510,"height":360},{"type":"s","url":"https:\/\/sun1-90.userapi.com\/c824503\/v824503538\/cfa82\/OFw5ND5l6z4.jpg","width":75,"height":53},{"type":"x","url":"https:\/\/sun1-23.userapi.com\/c824503\/v824503538\/cfa84\/RhWbp9eFklk.jpg","width":524,"height":370}],"text":"","date":1519520066,"access_key":"25a4b39360c9c23530"}},{"type":"photo","photo":{"id":456239220,"album_id":-7,"owner_id":-35769930,"user_id":100,"sizes":[{"type":"m","url":"https:\/\/sun1-28.userapi.com\/c830408\/v830408556\/8cf8c\/xFEGH7SnXgg.jpg","width":130,"height":92},{"type":"o","url":"https:\/\/sun1-14.userapi.com\/c830408\/v830408556\/8cf8e\/FjA6lwXFvSU.jpg","width":130,"height":92},{"type":"p","url":"https:\/\/sun1-30.userapi.com\/c830408\/v830408556\/8cf8f\/RwP-lhZ8XRA.jpg","width":200,"height":141},{"type":"q","url":"https:\/\/sun1-88.userapi.com\/c830408\/v830408556\/8cf90\/piZdy0NRn10.jpg","width":320,"height":226},{"type":"r","url":"https:\/\/sun1-86.userapi.com\/c830408\/v830408556\/8cf91\/BJq-Xy74Jn0.jpg","width":510,"height":360},{"type":"s","url":"https:\/\/sun1-91.userapi.com\/c830408\/v830408556\/8cf8b\/gWHRp1EYhpo.jpg","width":75,"height":53},{"type":"x","url":"https:\/\/sun1-88.userapi.com\/c830408\/v830408556\/8cf8d\/Qk4tzgPb3tA.jpg","width":524,"height":370}],"text":"","date":1519523929,"access_key":"0894b321edf007b026"}},{"type":"link","link":{"url":"http:\/\/t.me","title":"Telegram – a new era of messaging","description":"","target":"internal","photo":{"id":456239123,"album_id":-2,"owner_id":100,"sizes":[{"type":"m","url":"https:\/\/sun1-28.userapi.com\/c840629\/v840629865\/58b0e\/Bpzq42bY9Lg.jpg","width":130,"height":130},{"type":"s","url":"https:\/\/sun1-23.userapi.com\/c840629\/v840629865\/58b0d\/YHJSk3TlX6s.jpg","width":75,"height":75},{"type":"x","url":"https:\/\/sun1-91.userapi.com\/c840629\/v840629865\/58b0f\/dReJxmEWgf4.jpg","width":150,"height":150}],"text":"","date":1519196573}}}],"post_source":{"type":"vk"}}],"post_source":{"type":"vk"},"comments":{"count":36617,"can_post":1,"groups_can_post":true},"likes":{"count":15867,"user_likes":0,"can_like":1,"can_publish":1},"reposts":{"count":233,"user_reposted":0},"views":{"count":2313721}},{"id":2083400,"from_id":1,"owner_id":1,"date":1509059043,"post_type":"post","text":"Советник Президента России по вопросам развития интернета заявил о том, что Telegram якобы игнорирует запросы от российских государственных органов, но сотрудничает с властями других стран, например, Индонезии.\n\nЭто не так: уровень сотрудничества Telegram с властями не зависит от юрисдикции и везде строится на одних и тех же принципах. В отличие от своих российских коллег, индонезийские государственные службы не требовали от нас доступа к личной переписке. \n \nВо всем мире, включая Россию, Telegram обрабатывает запросы на удаление публично доступного противоправного контента, содержащего пропаганду терроризма, детскую порнографию и т. д. Вместе с тем, ни в одной стране мы не выдаем личные данные пользователей государственным органам. \n\nХотя весомая доля аудитории Telegram приходится на более консервативные страны, чем Россия, только в России Telegram был оштрафован за непредоставление ключей шифрования сообщений. Это единственный подобный прецедент за 4 года работы Telegram на глобальном рынке.","post_source":{"type":"vk"},"comments":{"count":106007,"can_post":1,"groups_can_post":true},"likes":{"count":41552,"user_likes":0,"can_like":1,"can_publish":1},"reposts":{"count":1075,"user_reposted":0},"views":{"count":4765584}}]}}
    

Looks like a python dictionary with the key -- response. Is that so?


```python
type(result)
```




    str




```python
import json
data = json.loads(result) 
print(type(data))
```

    <class 'dict'>
    

* Let's study the structure of the dictionary and extract the posts:


```python
data['response']['items']
```




    [{'id': 2442097,
      'from_id': 1,
      'owner_id': 1,
      'date': 1525805964,
      'post_type': 'post',
      'text': 'Иногда говорят, что Telegram был заблокирован в России, так как “закон есть закон”. Однако Telegram заблокирован в России как раз вопреки главному закону страны – Конституции. Решения судов и законы, противоречащие Конституции, не имеют силы. А это значит, что и сама блокировка Telegram незаконна. \n\nЕсли бы ФСБ ограничилась запросом информации о нескольких террористах, то ее требование вписывалось бы в рамки Конституции. Однако речь идет о передаче универсальных ключей шифрования с целью последующего бесконтрольного доступа к переписке неограниченного круга лиц. A это – прямое нарушение 23-й статьи Конституции о праве каждого на тайну переписки.\n\nПо этой причине юристы из “Агоры” сегодня обжаловали решение Верховного суда России о законности приказа ФСБ. Надеюсь, власти России откажутся от языка неисполнимых ультиматумов, на котором сегодня ведется диалог с технологическими компаниями.\n\nНезависимо от этого, мы продолжим борьбу за Telegram в России. История наших предков учит биться до победного конца. \n\nС Днем Победы!',
      'post_source': {'type': 'vk'},
      'comments': {'count': 388100, 'can_post': 1, 'groups_can_post': True},
      'likes': {'count': 152022, 'user_likes': 0, 'can_like': 1, 'can_publish': 1},
      'reposts': {'count': 3367, 'user_reposted': 0},
      'views': {'count': 8407053}},
     {'id': 2431591,
      'from_id': 1,
      'owner_id': 1,
      'date': 1525352753,
      'post_type': 'post',
      'text': 'Михаил Светов, организатор прошедшего митинга за свободу интернета, объявил конкурс на наиболее вдохновляющую обработку видеоматериалов с митинга. Призовой фонд – 1 биткоин.\n\n#digitalresistance',
      'attachments': [{'type': 'video',
        'video': {'id': 456239033,
         'owner_id': 1,
         'title': 'КОНКУРС НА БИТКОИН',
         'duration': 113,
         'description': 'Мне пришёл целевой анонимный донат на проведение конкурса. Разыгрываю целый биткоин [не кликбейт, на самом деле].\n\nКонкурс на лучшую видео и аудио обработку речей и кадров с митинга 30 апреля. Подходит любой формат, главное, в максимально мемичной форме распространить основные тезисы наших выступлений по интернету, и обратить внимание на критическую значимость блокировок. Все слова сказаны. Их нужно донести. Срок — 10 дней. Постите свои видео с хэштегом #digitalresistance во всех соцсетях и присылайте ссылк',
         'date': 1525352754,
         'comments': 120,
         'views': 42455,
         'local_views': 42455,
         'photo_130': 'https://sun1-89.userapi.com/c840722/v840722964/8039f/kunM7m6I7w4.jpg',
         'photo_320': 'https://sun1-26.userapi.com/c840722/v840722964/803a1/OGFig-5UNjY.jpg',
         'photo_640': 'https://sun1-23.userapi.com/c840722/v840722964/803a2/T2SKhzbHheQ.jpg',
         'photo_800': 'https://sun1-23.userapi.com/c840722/v840722964/803a2/T2SKhzbHheQ.jpg',
         'access_key': 'b6751e4a53ef7bd286',
         'platform': 'YouTube',
         'can_add': 1,
         'track_code': 'video_de9a36a19zr4b-mgLAKckJzAXajZWE7zK-CQXBCXxMMjob3G'}}],
      'post_source': {'type': 'vk'},
      'comments': {'count': 12992, 'can_post': 1, 'groups_can_post': True},
      'likes': {'count': 18349, 'user_likes': 0, 'can_like': 1, 'can_publish': 1},
      'reposts': {'count': 283, 'user_reposted': 0},
      'views': {'count': 4190108}},
     {'id': 2422169,
      'from_id': 1,
      'owner_id': 1,
      'date': 1525187997,
      'post_type': 'post',
      'text': '',
      'attachments': [{'type': 'photo',
        'photo': {'id': 456316241,
         'album_id': -7,
         'owner_id': 1,
         'sizes': [{'type': 'm',
           'url': 'https://sun1-84.userapi.com/c623900/v623900095/1160af/p5M94AlMuIk.jpg',
           'width': 130,
           'height': 97},
          {'type': 'o',
           'url': 'https://sun1-28.userapi.com/c623900/v623900095/1160b3/VZ8lWO9IliA.jpg',
           'width': 130,
           'height': 98},
          {'type': 'p',
           'url': 'https://sun1-83.userapi.com/c623900/v623900095/1160b4/zNdk9cy2yB8.jpg',
           'width': 200,
           'height': 150},
          {'type': 'q',
           'url': 'https://sun1-85.userapi.com/c623900/v623900095/1160b5/IuFfBtlIc9o.jpg',
           'width': 320,
           'height': 240},
          {'type': 'r',
           'url': 'https://sun1-83.userapi.com/c623900/v623900095/1160b6/9vODfb2MJ8o.jpg',
           'width': 510,
           'height': 382},
          {'type': 's',
           'url': 'https://sun1-19.userapi.com/c623900/v623900095/1160ae/4oqrxkIA8sU.jpg',
           'width': 75,
           'height': 56},
          {'type': 'x',
           'url': 'https://sun1-88.userapi.com/c623900/v623900095/1160b0/lKYaPpXh0sI.jpg',
           'width': 604,
           'height': 453},
          {'type': 'y',
           'url': 'https://sun1-28.userapi.com/c623900/v623900095/1160b1/bu7-9BElh6g.jpg',
           'width': 807,
           'height': 605},
          {'type': 'z',
           'url': 'https://sun1-94.userapi.com/c623900/v623900095/1160b2/39ZyjmEB_1Y.jpg',
           'width': 1279,
           'height': 959}],
         'text': '',
         'date': 1525187973,
         'access_key': '882117b1daeb20d383'}}],
      'post_source': {'type': 'vk'},
      'comments': {'count': 9685, 'can_post': 1, 'groups_can_post': True},
      'likes': {'count': 86813, 'user_likes': 0, 'can_like': 1, 'can_publish': 1},
      'reposts': {'count': 1331, 'user_reposted': 0},
      'views': {'count': 5838866}},
     {'id': 2418560,
      'from_id': 1,
      'owner_id': 1,
      'date': 1525168885,
      'post_type': 'post',
      'text': 'Наблюдаю, как несмотря на проливной дождь, по Невскому проспекту в данный момент движется огромная колонна, которая скандирует лозунги в защиту свободного интернета. Подобное сочетание природных условий и энергии людей возможно только в Петербурге. \n\nОбновлено: спасибо петербуржцам за стойкость и смелость.\n#digitalresistance',
      'post_source': {'type': 'vk'},
      'comments': {'count': 6689, 'can_post': 1, 'groups_can_post': True},
      'likes': {'count': 39523, 'user_likes': 0, 'can_like': 1, 'can_publish': 1},
      'reposts': {'count': 444, 'user_reposted': 0},
      'views': {'count': 5431265}},
     {'id': 2412029,
      'from_id': 1,
      'owner_id': 1,
      'date': 1525107823,
      'post_type': 'post',
      'text': 'Потрясающая акция в Москве. Более 12,000 человек выступили за свободный интернет. Спасибо каждому, кто нашел время, – мы в Telegram очень ценим эту поддержку. \n\nПоразила пассионарность спикеров – такие речи создают историю стран. https://www.youtube.com/watch?v=D9dPg3ofmyQ\n\nНеважно, прислушаются ли сейчас власти России к голосу общества. Важно, что мы всегда будем продолжать отстаивать те ценности, в которые верим.\n\nПомните: завтра – 1 мая – шествие и митинг в Петербурге.',
      'attachments': [{'type': 'video',
        'video': {'id': 456239027,
         'owner_id': 1,
         'title': 'НЕ СДАДИМ ИНТЕРНЕТ - РЕЖИМУ ЛЮСТРАЦИЯ! : СВЕТОВ',
         'duration': 469,
         'description': 'Выступление Михаила Светов на митинге "Против Роскомнадзора и блокировки Telegram" в Москве',
         'date': 1525107823,
         'comments': 303,
         'views': 31931,
         'local_views': 31931,
         'photo_130': 'https://sun1-83.userapi.com/c834303/v834303343/12d44f/DOiNeG_3DDU.jpg',
         'photo_320': 'https://sun1-84.userapi.com/c834303/v834303343/12d451/etCrt-Y8waQ.jpg',
         'photo_640': 'https://sun1-89.userapi.com/c834303/v834303343/12d452/hjIAImcvr-I.jpg',
         'photo_800': 'https://sun1-89.userapi.com/c834303/v834303343/12d452/hjIAImcvr-I.jpg',
         'access_key': 'adcc1fa1c7c69bad50',
         'platform': 'YouTube',
         'can_add': 1,
         'track_code': 'video_169beaa598ZZe2HZPFMBIWRwFqahDtMA3V3KnMoQMfRm5WMK'}}],
      'post_source': {'type': 'vk'},
      'comments': {'count': 5306, 'can_post': 1, 'groups_can_post': True},
      'likes': {'count': 24715, 'user_likes': 0, 'can_like': 1, 'can_publish': 1},
      'reposts': {'count': 928, 'user_reposted': 0},
      'views': {'count': 2859513}},
     {'id': 2407925,
      'from_id': 1,
      'owner_id': 1,
      'date': 1525090324,
      'post_type': 'post',
      'text': 'Тысячи молодых и прогрессивных людей в данный момент выступают в защиту свободы интернета в Москве. Тысячи еще продолжают подходить.\n\nЭто беспрецедентно. Я горжусь тем, что родился в одной стране с этими людьми. \n\nВаша энергия меняет мир.\n\n#digitalresistance',
      'attachments': [{'type': 'photo',
        'photo': {'id': 456315566,
         'album_id': -7,
         'owner_id': 1,
         'sizes': [{'type': 'm',
           'url': 'https://sun1-22.userapi.com/c846021/v846021276/38d2a/4BaEsjAZFiQ.jpg',
           'width': 130,
           'height': 97},
          {'type': 'o',
           'url': 'https://sun1-30.userapi.com/c846021/v846021276/38d2e/8aQ5ji7H98g.jpg',
           'width': 130,
           'height': 98},
          {'type': 'p',
           'url': 'https://sun1-29.userapi.com/c846021/v846021276/38d2f/SQQCW_QJNJI.jpg',
           'width': 200,
           'height': 150},
          {'type': 'q',
           'url': 'https://sun1-84.userapi.com/c846021/v846021276/38d30/GVGyP_ffBCE.jpg',
           'width': 320,
           'height': 240},
          {'type': 'r',
           'url': 'https://sun1-16.userapi.com/c846021/v846021276/38d31/xn5JdZycJyk.jpg',
           'width': 510,
           'height': 383},
          {'type': 's',
           'url': 'https://sun1-92.userapi.com/c846021/v846021276/38d29/wjurvCxIBF0.jpg',
           'width': 75,
           'height': 56},
          {'type': 'x',
           'url': 'https://sun1-86.userapi.com/c846021/v846021276/38d2b/nW8A1lSGHqs.jpg',
           'width': 604,
           'height': 453},
          {'type': 'y',
           'url': 'https://sun1-89.userapi.com/c846021/v846021276/38d2c/lxprfpdEWMY.jpg',
           'width': 807,
           'height': 605},
          {'type': 'z',
           'url': 'https://sun1-21.userapi.com/c846021/v846021276/38d2d/ybgiwGxzjnQ.jpg',
           'width': 1280,
           'height': 960}],
         'text': '',
         'date': 1525089150,
         'access_key': '81ccd0f9fc969bdb01'}}],
      'post_source': {'type': 'vk'},
      'comments': {'count': 9533, 'can_post': 1, 'groups_can_post': True},
      'likes': {'count': 81901, 'user_likes': 0, 'can_like': 1, 'can_publish': 1},
      'reposts': {'count': 2237, 'user_reposted': 0},
      'views': {'count': 5467149}},
     {'id': 2405336,
      'from_id': 1,
      'owner_id': 1,
      'date': 1525048713,
      'post_type': 'post',
      'text': 'https://youtu.be/FT6TVvAQ5OY\n\n30 апреля (понедельник) в Москве:\n\n13:00 – Сбор по адресу ул. Маши Порываевой, 38. \n14:00-15:00 – Шествие от ул. Маши Порываевой, 38, до пр. Академика Сахарова. \n15:00-16:00 – Митинг на пр. Академика Сахарова, 9.\n\nАналогичная акция в Петербурге – 1 мая.',
      'attachments': [{'type': 'video',
        'video': {'id': 456239026,
         'owner_id': 1,
         'title': 'МИТИНГ ЗА ТЕЛЕГРАМ',
         'duration': 172,
         'description': '30 АПРЕЛЯ, 14:00 ПРОСПЕКТ САХАРОВА, МОСКВА\n\nhttp://digitalresistance.moscow\n\nТвиттер https://twitter.com/msvetov\n\nКанал в телеграме https://t.me/mrlibertarian\n\nПаблик вконтакте http://vk.com/svtvofficial\n\nЕсли вам нравится что я делаю, помогите каналу криптовалютой!\n\nBTC 154H8UAG9EgBPHNFuW8u6h56JdqpSsAYmS\nLTC LgAYmdCfta3csv7Ahi6pN1Rz4za48fViw6\nBCH 16VEgMz15eza5sjLyBZBLZuX5rBYX6zueJ\nDASH Xut9jPe5jbv1wbr394N6xfJNDoA2QEN7BG\nETH 0x0CbE5dC38a1f453547D67238680c250b8Ce58b40\nEOS. 0x0CbE5dC38a1f453547D67238680c250b8',
         'date': 1525048713,
         'comments': 94,
         'views': 22285,
         'local_views': 22285,
         'photo_130': 'https://sun1-84.userapi.com/c834102/v834102746/12a32d/YU4Nr613Cko.jpg',
         'photo_320': 'https://sun1-19.userapi.com/c834102/v834102746/12a32f/PPGGUKr4FRg.jpg',
         'photo_640': 'https://sun1-19.userapi.com/c834102/v834102746/12a330/B8cRHnhkI9I.jpg',
         'photo_800': 'https://sun1-19.userapi.com/c834102/v834102746/12a330/B8cRHnhkI9I.jpg',
         'access_key': '234bba7361822a6d77',
         'platform': 'YouTube',
         'can_add': 1,
         'track_code': 'video_689fe32fzTBElTrHHobm3dZMkRXMgLgUVo5fipajkNOU1OOy'}}],
      'post_source': {'type': 'vk'},
      'comments': {'count': 2716, 'can_post': 1, 'groups_can_post': True},
      'likes': {'count': 11101, 'user_likes': 0, 'can_like': 1, 'can_publish': 1},
      'reposts': {'count': 291, 'user_reposted': 0},
      'views': {'count': 1625040}},
     {'id': 2401719,
      'from_id': 1,
      'owner_id': 1,
      'date': 1525012261,
      'post_type': 'post',
      'text': 'Видеозапись, присланная сторонниками акции #sundaypaperplane.',
      'attachments': [{'type': 'video',
        'video': {'id': 456239025,
         'owner_id': 1,
         'title': '#sundaypaperplane',
         'duration': 59,
         'description': 'Видео, присланное сторонниками акции #sundaypaperplane',
         'date': 1525009959,
         'comments': 338,
         'views': 3758435,
         'width': 1280,
         'height': 720,
         'photo_130': 'https://sun9-68.userapi.com/c834302/v834302714/127274/cAAnK4yYfDk.jpg',
         'photo_320': 'https://sun9-43.userapi.com/c834302/v834302714/127272/fehorJva6Ek.jpg',
         'photo_800': 'https://sun9-11.userapi.com/c834302/v834302714/127271/aUePw7nN1Lg.jpg',
         'first_frame_320': 'https://sun1-21.userapi.com/c845018/v845018714/3dc9d/JOxOnDEXDYA.jpg',
         'first_frame_160': 'https://sun1-88.userapi.com/c845018/v845018714/3dc9e/SBl3ws19v_U.jpg',
         'first_frame_130': 'https://sun1-28.userapi.com/c845018/v845018714/3dc9f/m_iwRKEwSGo.jpg',
         'first_frame_800': 'https://sun1-16.userapi.com/c845018/v845018714/3dc9c/yPygF5p1t2M.jpg',
         'access_key': '58a4fdf3bd91ac7ebb',
         'can_add': 1,
         'track_code': 'video_039f48f2KB9C8G6_0H7qmKAH1iZAcgimfd-clOcMD6mmBUzZ'}}],
      'post_source': {'type': 'vk'},
      'comments': {'count': 3603, 'can_post': 1, 'groups_can_post': True},
      'likes': {'count': 19940, 'user_likes': 0, 'can_like': 1, 'can_publish': 1},
      'reposts': {'count': 459, 'user_reposted': 0},
      'views': {'count': 7870430}},
     {'id': 2401089,
      'from_id': 1,
      'owner_id': 1,
      'date': 1525009304,
      'post_type': 'post',
      'text': 'Завтра (30 апреля) в 14:00 в Москве на проспекте Сахарова состоится согласованный митинг за свободу интернета. Это исторический шанс для москвичей выразить общую позицию. Послезавтра может быть уже поздно.\n\nПоследние 2 недели мы вели неравный бой с интернет-цензором. Мы делали это ради вас – наших российских пользователей. Однако будущее российского интернета находится, в конечном счете, в ваших руках. \n\nКто-то скажет, что митинг ничего не изменит. Это не так. Россия находится на перепутье – полномасштабная цензура еще не была введена. Если бездействовать, Россия потеряет Telegram и другие популярные сервисы. Ваше активное участие может поменять ход истории.',
      'copy_history': [{'id': 8,
        'owner_id': -165675366,
        'from_id': -165675366,
        'date': 1524755130,
        'post_type': 'post',
        'text': 'Митинг против блокировки Telegram. Проспект Сахарова, 30 апреля, 14:00 — 16:00 \n \nБлокировка Telegram – это национальный позор: ни одно государство, претендующее на лидерство в XXI веке, не должно препятствовать развитию собственных технологий и цифровому прогрессу. \n \nРоскомнадзор нарушает нормы Конституции РФ и фундаментальные права и свободы человека. Блокировки, цензура и уголовные преследования за лайки и репосты недопустимы. Единственными реальными результатами «блокировки» будут только рост угрозы национальной безопасности, долгосрочный ущерб экономике и изоляция России от прогресса. \n \nМетоды, которыми власть «развивает интернет» и новые законы о соцсетях не оставляют надежд, что ситуация разрешится сама собой. \n \nЕсли вы используете Telegram, поддерживаете свободу слова, вас достали блокировки, вы за свободный интернет и цифровой прогресс — приходите на митинг. \n \n30 апреля, 14:00. проспект академика Сахарова. Сбор с 13:00 по адресу: ул. Маши Порываевой, 38). Не забудьте пару бумажных самолетиков! \n \nМитинг организовывается Либертарианской партией России. Согласовано с мэрией Москвы. \n \n• Поддержать нас рублем: http://digitalresistance.moscow \n• Наши ивенты в VK и в FB \n• По вопросам участия в организации и для обратной связи пишите на info@libertarian-party.ru или в бота обратной связи: @digitalresistance_moscow',
        'attachments': [{'type': 'link',
          'link': {'url': 'https://vk.com/app5575136_-165675366',
           'title': 'Митинг за свободу интернета #DigitalResistance',
           'caption': 'Application',
           'description': 'Вся информация: digitalresistance.moscow',
           'photo': {'id': 456242045,
            'album_id': -2,
            'owner_id': 100,
            'sizes': [{'type': 'm',
              'url': 'https://sun1-30.userapi.com/c840334/v840334770/7b6e9/pi8vUUo_Atw.jpg',
              'width': 130,
              'height': 58},
             {'type': 'o',
              'url': 'https://sun1-25.userapi.com/c840334/v840334770/7b6ed/ivETWN2O51g.jpg',
              'width': 130,
              'height': 87},
             {'type': 'p',
              'url': 'https://sun1-87.userapi.com/c840334/v840334770/7b6ee/35N6X4AgvfQ.jpg',
              'width': 200,
              'height': 133},
             {'type': 'q',
              'url': 'https://sun1-23.userapi.com/c840334/v840334770/7b6ef/ZPjm2XSfdm4.jpg',
              'width': 320,
              'height': 213},
             {'type': 'r',
              'url': 'https://sun1-23.userapi.com/c840334/v840334770/7b6f0/FLnQB4mgddA.jpg',
              'width': 510,
              'height': 340},
             {'type': 's',
              'url': 'https://sun1-18.userapi.com/c840334/v840334770/7b6e8/PYpIpkn41pQ.jpg',
              'width': 75,
              'height': 33},
             {'type': 'x',
              'url': 'https://sun1-87.userapi.com/c840334/v840334770/7b6ea/vbFs7yBS3Ck.jpg',
              'width': 604,
              'height': 270},
             {'type': 'y',
              'url': 'https://sun1-84.userapi.com/c840334/v840334770/7b6eb/CrCbFu7DoeM.jpg',
              'width': 807,
              'height': 361},
             {'type': 'z',
              'url': 'https://sun1-84.userapi.com/c840334/v840334770/7b6ec/cuTc-FyX2CA.jpg',
              'width': 1280,
              'height': 573}],
            'text': '',
            'date': 1524755117},
           'button': {'title': 'Open',
            'action': {'type': 'open_url',
             'url': 'https://vk.com/app5575136_-165675366'}}}}],
        'post_source': {'type': 'vk'}}],
      'post_source': {'type': 'vk'},
      'comments': {'count': 2184, 'can_post': 1, 'groups_can_post': True},
      'likes': {'count': 21127, 'user_likes': 0, 'can_like': 1, 'can_publish': 1},
      'reposts': {'count': 956, 'user_reposted': 0},
      'views': {'count': 1966002}},
     {'id': 2389655,
      'from_id': 1,
      'owner_id': 1,
      'date': 1524838659,
      'post_type': 'post',
      'text': 'https://www.youtube.com/watch?v=FCbPGhUxDiQ\n(при просмотре нужно включить русские субтитры)',
      'attachments': [{'type': 'video',
        'video': {'id': 456239024,
         'owner_id': 1,
         'title': 'Совещание в РКН',
         'duration': 240,
         'description': 'Включите русские субтитры!',
         'date': 1524838659,
         'comments': 587,
         'views': 187027,
         'local_views': 187027,
         'photo_130': 'https://sun9-43.userapi.com/c844521/v844521881/3be8f/CAs8vZb_b8I.jpg',
         'photo_320': 'https://sun9-63.userapi.com/c844521/v844521881/3be91/XEPyjlFQ_Y4.jpg',
         'photo_640': 'https://sun9-48.userapi.com/c844521/v844521881/3be92/AxXaeifW8_w.jpg',
         'photo_800': 'https://sun9-48.userapi.com/c844521/v844521881/3be92/AxXaeifW8_w.jpg',
         'access_key': 'd41f154fa71177c8fb',
         'platform': 'YouTube',
         'can_add': 1,
         'track_code': 'video_66f482123pNE5mWaKQ9QCcPuOAaiO6iEZJO9Gpujb-RlYWJE'}}],
      'post_source': {'type': 'vk'},
      'comments': {'count': 9350, 'can_post': 1, 'groups_can_post': True},
      'likes': {'count': 47499, 'user_likes': 0, 'can_like': 1, 'can_publish': 1},
      'reposts': {'count': 3031, 'user_reposted': 0},
      'views': {'count': 2941269}},
     {'id': 2382822,
      'from_id': 1,
      'owner_id': 1,
      'date': 1524761880,
      'post_type': 'post',
      'text': '11-й день продолжаются попытки блокировать Telegram на территории России. Многие спрашивают, возможен ли был некий компромисс. Думаю, что едва ли.\n\nКлючи для расшифровки переписки всех своих пользователей ни Telegram, ни другие мессенджеры, не могли бы выдать при всем желании. Это обусловлено техническими особенностями шифрования в 2018 году.\n\nДаже если бы запрос ФСБ ограничивался помощью в поимке 6 террористов, участвовавших в теракте в Петербурге, мы вряд ли могли быть полезны: часть интересующих ФСБ мобильных номеров никогда не имели аккаунта в Telegram, другая их часть была автоматически удалена за неактивностью еще в прошлом году. \n\nВпрочем, согласно материалам дела, ставшим доступными Republic.ru в октябре, для координации теракта в большей степени использовался не Telegram, а WhatsApp.',
      'post_source': {'type': 'vk'},
      'comments': {'count': 6958, 'can_post': 1, 'groups_can_post': True},
      'likes': {'count': 37351, 'user_likes': 0, 'can_like': 1, 'can_publish': 1},
      'reposts': {'count': 1066, 'user_reposted': 0},
      'views': {'count': 4470793}},
     {'id': 2358781,
      'from_id': 1,
      'owner_id': 1,
      'date': 1524440871,
      'post_type': 'post',
      'text': 'Эту неделю мы боролись не с Роскомнадзором или ФСБ. Мы боролись за цифровое будущее России. Свободный интернет и оконечное шифрование – неотъемлемые части этого будущего. \n\nНи одна развитая страна не блокирует мессенджеры за отказ выдать спецслужбам ключи шифрования. Отмена права на конфиденциальность – лекарство, которое опаснее самой болезни. \n\nКак только некая служба получает возможность бесконтрольно мониторить личную переписку граждан, очень скоро этот доступ оказывается в руках у третьих сторон – взяткодателей, хакеров, агентов других государств. В результате требование предоставить универсальные пути обхода шифрования через выдачу “ключей” снижает информационную безопасность как элит, так и общества в целом.\n\nP. S. Если у Вас есть инсайды о причинах, планах и методах блокировки, сообщайте нам по адресу arequest2@gmail.com.',
      'post_source': {'type': 'vk'},
      'comments': {'count': 15148, 'can_post': 1, 'groups_can_post': True},
      'likes': {'count': 47828, 'user_likes': 0, 'can_like': 1, 'can_publish': 1},
      'reposts': {'count': 1671, 'user_reposted': 0},
      'views': {'count': 4567685}},
     {'id': 2358485,
      'from_id': 1,
      'owner_id': 1,
      'date': 1524439551,
      'post_type': 'post',
      'text': 'Огромное спасибо жителям десятков городов России за поддержку свободного интернета. \n\nВидеоролики с прошедшей акции предлагаю выкладывать под хэштегом #sundaypaperplane во всех соцсетях.\n\nСледующий раз? Воскресенье, 29 апреля в 19:00 по местному времени.',
      'attachments': [{'type': 'video',
        'video': {'id': 456239442,
         'owner_id': -6726778,
         'title': '«Смотри, как летит!» Как прошла акция в поддержку Telegram',
         'duration': 59,
         'description': 'Сегодня Telegram разослал уведомления: «Если вы поддерживаете свободный интернет, запустите из окна бумажный самолетик сегодня ровно в 7 вечера». Вот, что из этого вышло',
         'date': 1524423074,
         'comments': 0,
         'views': 6955341,
         'width': 1920,
         'height': 1080,
         'photo_130': 'https://sun1-14.userapi.com/c844320/v844320005/3501b/l0ZyprH86uA.jpg',
         'photo_320': 'https://sun1-23.userapi.com/c844320/v844320005/35019/vZwfgZWMf5Q.jpg',
         'photo_800': 'https://sun1-90.userapi.com/c844320/v844320005/35018/kcpAsbrL250.jpg',
         'first_frame_320': 'https://sun1-24.userapi.com/c847020/v847020484/2e434/zwfKl2_dY4k.jpg',
         'first_frame_160': 'https://sun1-86.userapi.com/c847020/v847020484/2e435/ibEkU5wC1NY.jpg',
         'first_frame_130': 'https://sun1-24.userapi.com/c847020/v847020484/2e436/DS96-esVSxU.jpg',
         'first_frame_800': 'https://sun1-83.userapi.com/c847020/v847020484/2e433/7c-xI13cYeQ.jpg',
         'access_key': '44088de20a1d3dd9b7',
         'can_add': 1,
         'track_code': 'video_0e4a06d9DjbA_uLL9O2Zqq9AeCp9H8I4STqzQ0TZR1JTLIZtUY8MJO3I1Q'}}],
      'post_source': {'type': 'vk'},
      'comments': {'count': 5852, 'can_post': 1, 'groups_can_post': True},
      'likes': {'count': 38329, 'user_likes': 0, 'can_like': 1, 'can_publish': 1},
      'reposts': {'count': 1067, 'user_reposted': 0},
      'views': {'count': 7447993}},
     {'id': 2348522,
      'from_id': 1,
      'owner_id': 1,
      'date': 1524402346,
      'post_type': 'post',
      'text': 'Мы продержались 7 дней под самым масштабным актом интернет-цензуры за историю России.\n\nВсех, кто поддерживает свободный интернет, призываем запустить из окна бумажный самолетик сегодня ровно в 7 вечера по местному времени.\n\nЧерез час после акции имеет смысл устроить небольшой субботник – собрать те самолетики, которые Вы найдете у Вашего дома. \n\nСпасибо за поддержку. Эта неделя останется в истории.',
      'attachments': [{'type': 'photo',
        'photo': {'id': 456311287,
         'album_id': -7,
         'owner_id': 1,
         'sizes': [{'type': 'm',
           'url': 'https://sun1-16.userapi.com/c840331/v840331315/7980a/elqYxlBXDt4.jpg',
           'width': 109,
           'height': 130},
          {'type': 'o',
           'url': 'https://sun1-14.userapi.com/c840331/v840331315/7980f/mi_6yzkjOgk.jpg',
           'width': 130,
           'height': 155},
          {'type': 'p',
           'url': 'https://sun1-27.userapi.com/c840331/v840331315/79810/gZWd0AydnT0.jpg',
           'width': 200,
           'height': 238},
          {'type': 'q',
           'url': 'https://sun1-21.userapi.com/c840331/v840331315/79811/GMuDaXj73zc.jpg',
           'width': 320,
           'height': 381},
          {'type': 'r',
           'url': 'https://sun1-25.userapi.com/c840331/v840331315/79812/L3RbhPkNcTA.jpg',
           'width': 510,
           'height': 607},
          {'type': 's',
           'url': 'https://sun1-87.userapi.com/c840331/v840331315/79809/wemzIrvo93Q.jpg',
           'width': 63,
           'height': 75},
          {'type': 'w',
           'url': 'https://sun1-91.userapi.com/c840331/v840331315/7980e/kp8MdNLCQIk.jpg',
           'width': 1816,
           'height': 2160},
          {'type': 'x',
           'url': 'https://sun1-27.userapi.com/c840331/v840331315/7980b/wEMNpAbN5Ac.jpg',
           'width': 507,
           'height': 604},
          {'type': 'y',
           'url': 'https://sun1-29.userapi.com/c840331/v840331315/7980c/dEI_cC4qgZY.jpg',
           'width': 678,
           'height': 807},
          {'type': 'z',
           'url': 'https://sun1-30.userapi.com/c840331/v840331315/7980d/Ph9yi54v5FI.jpg',
           'width': 908,
           'height': 1080}],
         'text': '',
         'date': 1524406529,
         'access_key': 'e8d2843ab80866361c'}},
       {'type': 'photo',
        'photo': {'id': 456311217,
         'album_id': -7,
         'owner_id': 1,
         'sizes': [{'type': 'm',
           'url': 'https://sun1-17.userapi.com/c845216/v845216315/33ec9/l_0acnvR2Lw.jpg',
           'width': 130,
           'height': 130},
          {'type': 'o',
           'url': 'https://sun1-91.userapi.com/c845216/v845216315/33ece/ZaHA5l-UQ9s.jpg',
           'width': 130,
           'height': 130},
          {'type': 'p',
           'url': 'https://sun1-20.userapi.com/c845216/v845216315/33ecf/lVgexBBK4iA.jpg',
           'width': 200,
           'height': 200},
          {'type': 'q',
           'url': 'https://sun1-19.userapi.com/c845216/v845216315/33ed0/ovUJ9nyzqc4.jpg',
           'width': 320,
           'height': 320},
          {'type': 'r',
           'url': 'https://sun1-18.userapi.com/c845216/v845216315/33ed1/-6cnhavwq6Q.jpg',
           'width': 510,
           'height': 510},
          {'type': 's',
           'url': 'https://sun1-27.userapi.com/c845216/v845216315/33ec8/nMXu21wxVL8.jpg',
           'width': 75,
           'height': 75},
          {'type': 'w',
           'url': 'https://sun1-85.userapi.com/c845216/v845216315/33ecd/8y5bkHbPrO4.jpg',
           'width': 1276,
           'height': 1276},
          {'type': 'x',
           'url': 'https://sun1-87.userapi.com/c845216/v845216315/33eca/f1QfPVeYCfg.jpg',
           'width': 604,
           'height': 604},
          {'type': 'y',
           'url': 'https://sun1-84.userapi.com/c845216/v845216315/33ecb/ccP98flufCc.jpg',
           'width': 807,
           'height': 807},
          {'type': 'z',
           'url': 'https://sun1-16.userapi.com/c845216/v845216315/33ecc/zJ6-nZvpO8A.jpg',
           'width': 1080,
           'height': 1080}],
         'text': '',
         'date': 1524405864,
         'access_key': '16c7801b5c9f97c4a5'}}],
      'post_source': {'type': 'vk'},
      'comments': {'count': 9016, 'can_post': 1, 'groups_can_post': True},
      'likes': {'count': 89539, 'user_likes': 0, 'can_like': 1, 'can_publish': 1},
      'reposts': {'count': 2670, 'user_reposted': 0},
      'views': {'count': 4457644}},
     {'id': 2331162,
      'from_id': 1,
      'owner_id': 1,
      'date': 1524147382,
      'post_type': 'post',
      'text': 'Telegram продолжает оставаться доступным российским пользователям, несмотря на блокировку властями РФ более 18 миллионов IP-адресов за последние 4 дня. \n\nСпасибо всем, кто участвует в Цифровом Сопротивлении. Все больше IT-предпринимателей, программистов, системных администраторов делом помогают обеспечивать гарантированные Конституцией права россиян.',
      'post_source': {'type': 'vk'},
      'comments': {'count': 13244, 'can_post': 1, 'groups_can_post': True},
      'likes': {'count': 88176, 'user_likes': 0, 'can_like': 1, 'can_publish': 1},
      'reposts': {'count': 1906, 'user_reposted': 0},
      'views': {'count': 5225736}},
     {'id': 2307813,
      'from_id': 1,
      'owner_id': 1,
      'date': 1523971038,
      'post_type': 'post',
      'text': 'Спасибо за поддержку и преданность Telegram – вместе нам удалось пережить первые 24 часа блокировки.\n\nКак показали последние сутки, в своей войне с прогрессом надзорные органы России готовы блокировать миллионы IP-адресов облачных хостингов, не считаясь с потерями посторонних проектов. \n\nПомимо этого, власти России борются и с независимыми сервисами proxy/VPN, многие из которых перестают работать (если это произошло, отключите прокси в настройках Telegram и попробуйте найти другой).\n\nХотя российский рынок не составляет существенной доли пользовательской базы Telegram, он важен нам по личным соображениям. \n\nВ рамках Цифрового Сопротивления – децентрализованного движения в защиту цифровых свобод и прогресса – я начал выплачивать биткоин-гранты администраторам proxy и vpn. В течение этого года буду рад пожертвовать миллионы долларов личных средств на эти цели. Призываю всех присоединяться и участвовать – настройкой прокси/vpn серверов или их финансированием.',
      'post_source': {'type': 'vk'},
      'comments': {'count': 19469, 'can_post': 1, 'groups_can_post': True},
      'likes': {'count': 173108, 'user_likes': 0, 'can_like': 1, 'can_publish': 1},
      'reposts': {'count': 4693, 'user_reposted': 0},
      'views': {'count': 7057457}},
     {'id': 2296940,
      'from_id': 1,
      'owner_id': 1,
      'date': 1523881233,
      'post_type': 'post',
      'text': 'Сегодня утром власти России начали блокировать Telegram, поэтому на некоторых операторах связи сервис может работать нестабильно. Последствия блокировки: \n\n1. Качество жизни 15 миллионов россиян ухудшится, так как Telegram без VPN может быть временами недоступен. \n\n2. Террористическая угроза в России останется на прежнем уровне, так как экстремисты продолжат пользоваться шифрованными каналами связи – в других мессенджерах, либо через VPN.\n\n3. Национальная безопасность России снизится, так как часть личных данных россиян перейдет из нейтральной к РФ площадки в контролируемые из США WhatsApp/Facebook. \n\nМы считаем решение о блокировке антиконституционным и продолжим отстаивать право на тайну переписки россиян. ✊🏼',
      'post_source': {'type': 'vk'},
      'comments': {'count': 12333, 'can_post': 1, 'groups_can_post': True},
      'likes': {'count': 160402, 'user_likes': 0, 'can_like': 1, 'can_publish': 1},
      'reposts': {'count': 4625, 'user_reposted': 0},
      'views': {'count': 6582578}},
     {'id': 2285269,
      'from_id': 1,
      'owner_id': 1,
      'date': 1523619298,
      'post_type': 'post',
      'text': 'Таганский суд Москвы вынес решение о блокировке Telegram на территории РФ. Что стоит иметь в виду пользователям:\n\n1. Telegram будет использовать встроенные методы обхода блокировок, которые не требуют действий от пользователей, однако 100%-ая доступность сервиса без VPN не гарантирована.\n2. В первые часы блокировки сторонние VPN/Proxy-сервисы могут быть перегружены и с большой вероятностью будут работать медленно.\n3. Независимо от наличия блокировки, Telegram сохранит возможность централизованно рассылать уведомления всем российским пользователям, информируя о развитии ситуации. \n\nВажно: не удаляйте и не переустанавливайте Telegram при возникновении проблем со связью. Старайтесь своевременно скачивать обновления Telegram в AppStore или Google Play.\n\n💪',
      'post_source': {'type': 'vk'},
      'comments': {'count': 11751, 'can_post': 1, 'groups_can_post': True},
      'likes': {'count': 106713, 'user_likes': 0, 'can_like': 1, 'can_publish': 1},
      'reposts': {'count': 5229, 'user_reposted': 0},
      'views': {'count': 6607646}},
     {'id': 2236210,
      'from_id': 1,
      'owner_id': 1,
      'date': 1519549711,
      'post_type': 'post',
      'text': '',
      'copy_history': [{'id': 30344,
        'owner_id': -35769930,
        'from_id': -35769930,
        'date': 1519520066,
        'post_type': 'post',
        'text': 'Сегодня ВКонтакте запустил набор «Election girl», полностью срисовав стикеры с моих. Получилось, правда, не очень, но не отчаивайся, дорогой автор! Пару лет срисовки моих стикеров и ты станешь даже вполне себе ничего - у меня их очень много. 😌\n\nХочешь по-взрослому? Работай сам, а не сиди на чужой шее, как пиявка. По иронии судьбы этот набор посвящен выборам и призывает повзрослеть. \n\nОригинальный набор тут: t.me/addstickers/pinup_girl\n💕',
        'attachments': [{'type': 'photo',
          'photo': {'id': 456239215,
           'album_id': -7,
           'owner_id': -35769930,
           'user_id': 100,
           'sizes': [{'type': 'm',
             'url': 'https://sun1-22.userapi.com/c824503/v824503538/cfa91/lkMea8ehuJA.jpg',
             'width': 130,
             'height': 92},
            {'type': 'o',
             'url': 'https://sun1-25.userapi.com/c824503/v824503538/cfa93/0ek4PTEofLw.jpg',
             'width': 130,
             'height': 92},
            {'type': 'p',
             'url': 'https://sun1-30.userapi.com/c824503/v824503538/cfa94/NjaGxeohRBk.jpg',
             'width': 200,
             'height': 141},
            {'type': 'q',
             'url': 'https://sun1-93.userapi.com/c824503/v824503538/cfa95/i1UwI5nop2s.jpg',
             'width': 320,
             'height': 226},
            {'type': 'r',
             'url': 'https://sun1-14.userapi.com/c824503/v824503538/cfa96/AQlm-6NOxyM.jpg',
             'width': 510,
             'height': 360},
            {'type': 's',
             'url': 'https://sun1-25.userapi.com/c824503/v824503538/cfa90/EreWNC9mgj4.jpg',
             'width': 75,
             'height': 53},
            {'type': 'x',
             'url': 'https://sun1-26.userapi.com/c824503/v824503538/cfa92/zCbJn0iygCE.jpg',
             'width': 524,
             'height': 370}],
           'text': '',
           'date': 1519520066,
           'access_key': 'a48f44fbbab4802f8c'}},
         {'type': 'photo',
          'photo': {'id': 456239216,
           'album_id': -7,
           'owner_id': -35769930,
           'user_id': 100,
           'sizes': [{'type': 'm',
             'url': 'https://sun1-94.userapi.com/c824503/v824503538/cfa8a/vltV2SSpc7E.jpg',
             'width': 130,
             'height': 92},
            {'type': 'o',
             'url': 'https://sun1-86.userapi.com/c824503/v824503538/cfa8c/UXtsy0gRq0c.jpg',
             'width': 130,
             'height': 92},
            {'type': 'p',
             'url': 'https://sun1-90.userapi.com/c824503/v824503538/cfa8d/a3RTr4JKGMs.jpg',
             'width': 200,
             'height': 141},
            {'type': 'q',
             'url': 'https://sun1-16.userapi.com/c824503/v824503538/cfa8e/v74fHOaKrhs.jpg',
             'width': 320,
             'height': 226},
            {'type': 'r',
             'url': 'https://sun1-17.userapi.com/c824503/v824503538/cfa8f/YjvF6eslIzk.jpg',
             'width': 510,
             'height': 360},
            {'type': 's',
             'url': 'https://sun1-14.userapi.com/c824503/v824503538/cfa89/p71fhfZ8-Mo.jpg',
             'width': 75,
             'height': 53},
            {'type': 'x',
             'url': 'https://sun1-29.userapi.com/c824503/v824503538/cfa8b/oBN7hoNR1xQ.jpg',
             'width': 524,
             'height': 370}],
           'text': '',
           'date': 1519520066,
           'access_key': '17d876b8a46e3223fc'}},
         {'type': 'photo',
          'photo': {'id': 456239217,
           'album_id': -7,
           'owner_id': -35769930,
           'user_id': 100,
           'sizes': [{'type': 'm',
             'url': 'https://sun1-18.userapi.com/c824503/v824503538/cfa98/Dx2fJmedw5U.jpg',
             'width': 130,
             'height': 92},
            {'type': 'o',
             'url': 'https://sun1-94.userapi.com/c824503/v824503538/cfa9a/W1epMq1GSC0.jpg',
             'width': 130,
             'height': 92},
            {'type': 'p',
             'url': 'https://sun1-16.userapi.com/c824503/v824503538/cfa9b/Z8OwHC2TJnU.jpg',
             'width': 200,
             'height': 141},
            {'type': 'q',
             'url': 'https://sun1-93.userapi.com/c824503/v824503538/cfa9c/jY2jzQrvdZk.jpg',
             'width': 320,
             'height': 226},
            {'type': 'r',
             'url': 'https://sun1-83.userapi.com/c824503/v824503538/cfa9d/2nMv6Ehaqn4.jpg',
             'width': 510,
             'height': 360},
            {'type': 's',
             'url': 'https://sun1-90.userapi.com/c824503/v824503538/cfa97/9MBiG28Ht1c.jpg',
             'width': 75,
             'height': 53},
            {'type': 'x',
             'url': 'https://sun1-85.userapi.com/c824503/v824503538/cfa99/OKrx6uAzo7Y.jpg',
             'width': 524,
             'height': 370}],
           'text': '',
           'date': 1519520066,
           'access_key': '7a16532dfd9dd87ab2'}},
         {'type': 'photo',
          'photo': {'id': 456239218,
           'album_id': -7,
           'owner_id': -35769930,
           'user_id': 100,
           'sizes': [{'type': 'm',
             'url': 'https://sun1-16.userapi.com/c824503/v824503538/cfa83/p-699MHN-JA.jpg',
             'width': 130,
             'height': 92},
            {'type': 'o',
             'url': 'https://sun1-91.userapi.com/c824503/v824503538/cfa85/2dk7AuAFfYU.jpg',
             'width': 130,
             'height': 92},
            {'type': 'p',
             'url': 'https://sun1-29.userapi.com/c824503/v824503538/cfa86/62JtBBTJYHY.jpg',
             'width': 200,
             'height': 141},
            {'type': 'q',
             'url': 'https://sun1-94.userapi.com/c824503/v824503538/cfa87/SlmnZNj1Pks.jpg',
             'width': 320,
             'height': 226},
            {'type': 'r',
             'url': 'https://sun1-86.userapi.com/c824503/v824503538/cfa88/xVIMW5MqVBE.jpg',
             'width': 510,
             'height': 360},
            {'type': 's',
             'url': 'https://sun1-90.userapi.com/c824503/v824503538/cfa82/OFw5ND5l6z4.jpg',
             'width': 75,
             'height': 53},
            {'type': 'x',
             'url': 'https://sun1-23.userapi.com/c824503/v824503538/cfa84/RhWbp9eFklk.jpg',
             'width': 524,
             'height': 370}],
           'text': '',
           'date': 1519520066,
           'access_key': '25a4b39360c9c23530'}},
         {'type': 'photo',
          'photo': {'id': 456239220,
           'album_id': -7,
           'owner_id': -35769930,
           'user_id': 100,
           'sizes': [{'type': 'm',
             'url': 'https://sun1-28.userapi.com/c830408/v830408556/8cf8c/xFEGH7SnXgg.jpg',
             'width': 130,
             'height': 92},
            {'type': 'o',
             'url': 'https://sun1-14.userapi.com/c830408/v830408556/8cf8e/FjA6lwXFvSU.jpg',
             'width': 130,
             'height': 92},
            {'type': 'p',
             'url': 'https://sun1-30.userapi.com/c830408/v830408556/8cf8f/RwP-lhZ8XRA.jpg',
             'width': 200,
             'height': 141},
            {'type': 'q',
             'url': 'https://sun1-88.userapi.com/c830408/v830408556/8cf90/piZdy0NRn10.jpg',
             'width': 320,
             'height': 226},
            {'type': 'r',
             'url': 'https://sun1-86.userapi.com/c830408/v830408556/8cf91/BJq-Xy74Jn0.jpg',
             'width': 510,
             'height': 360},
            {'type': 's',
             'url': 'https://sun1-91.userapi.com/c830408/v830408556/8cf8b/gWHRp1EYhpo.jpg',
             'width': 75,
             'height': 53},
            {'type': 'x',
             'url': 'https://sun1-88.userapi.com/c830408/v830408556/8cf8d/Qk4tzgPb3tA.jpg',
             'width': 524,
             'height': 370}],
           'text': '',
           'date': 1519523929,
           'access_key': '0894b321edf007b026'}},
         {'type': 'link',
          'link': {'url': 'http://t.me',
           'title': 'Telegram – a new era of messaging',
           'description': '',
           'target': 'internal',
           'photo': {'id': 456239123,
            'album_id': -2,
            'owner_id': 100,
            'sizes': [{'type': 'm',
              'url': 'https://sun1-28.userapi.com/c840629/v840629865/58b0e/Bpzq42bY9Lg.jpg',
              'width': 130,
              'height': 130},
             {'type': 's',
              'url': 'https://sun1-23.userapi.com/c840629/v840629865/58b0d/YHJSk3TlX6s.jpg',
              'width': 75,
              'height': 75},
             {'type': 'x',
              'url': 'https://sun1-91.userapi.com/c840629/v840629865/58b0f/dReJxmEWgf4.jpg',
              'width': 150,
              'height': 150}],
            'text': '',
            'date': 1519196573}}}],
        'post_source': {'type': 'vk'}}],
      'post_source': {'type': 'vk'},
      'comments': {'count': 36617, 'can_post': 1, 'groups_can_post': True},
      'likes': {'count': 15867, 'user_likes': 0, 'can_like': 1, 'can_publish': 1},
      'reposts': {'count': 233, 'user_reposted': 0},
      'views': {'count': 2313714}},
     {'id': 2083400,
      'from_id': 1,
      'owner_id': 1,
      'date': 1509059043,
      'post_type': 'post',
      'text': 'Советник Президента России по вопросам развития интернета заявил о том, что Telegram якобы игнорирует запросы от российских государственных органов, но сотрудничает с властями других стран, например, Индонезии.\n\nЭто не так: уровень сотрудничества Telegram с властями не зависит от юрисдикции и везде строится на одних и тех же принципах. В отличие от своих российских коллег, индонезийские государственные службы не требовали от нас доступа к личной переписке. \n \nВо всем мире, включая Россию, Telegram обрабатывает запросы на удаление публично доступного противоправного контента, содержащего пропаганду терроризма, детскую порнографию и т. д. Вместе с тем, ни в одной стране мы не выдаем личные данные пользователей государственным органам. \n\nХотя весомая доля аудитории Telegram приходится на более консервативные страны, чем Россия, только в России Telegram был оштрафован за непредоставление ключей шифрования сообщений. Это единственный подобный прецедент за 4 года работы Telegram на глобальном рынке.',
      'post_source': {'type': 'vk'},
      'comments': {'count': 106007, 'can_post': 1, 'groups_can_post': True},
      'likes': {'count': 41552, 'user_likes': 0, 'can_like': 1, 'can_publish': 1},
      'reposts': {'count': 1075, 'user_reposted': 0},
      'views': {'count': 4765575}}]



* Now let's extract the text from the first post:


```python
data['response']['items'][0]['text']
```




    'Иногда говорят, что Telegram был заблокирован в России, так как “закон есть закон”. Однако Telegram заблокирован в России как раз вопреки главному закону страны – Конституции. Решения судов и законы, противоречащие Конституции, не имеют силы. А это значит, что и сама блокировка Telegram незаконна. \n\nЕсли бы ФСБ ограничилась запросом информации о нескольких террористах, то ее требование вписывалось бы в рамки Конституции. Однако речь идет о передаче универсальных ключей шифрования с целью последующего бесконтрольного доступа к переписке неограниченного круга лиц. A это – прямое нарушение 23-й статьи Конституции о праве каждого на тайну переписки.\n\nПо этой причине юристы из “Агоры” сегодня обжаловали решение Верховного суда России о законности приказа ФСБ. Надеюсь, власти России откажутся от языка неисполнимых ультиматумов, на котором сегодня ведется диалог с технологическими компаниями.\n\nНезависимо от этого, мы продолжим борьбу за Telegram в России. История наших предков учит биться до победного конца. \n\nС Днем Победы!'



* Now, how do we extract the original text from a repost?


```python
data['response']['items'][18]['copy_history'][0]['text']

```




    'Сегодня ВКонтакте запустил набор «Election girl», полностью срисовав стикеры с моих. Получилось, правда, не очень, но не отчаивайся, дорогой автор! Пару лет срисовки моих стикеров и ты станешь даже вполне себе ничего - у меня их очень много. 😌\n\nХочешь по-взрослому? Работай сам, а не сиди на чужой шее, как пиявка. По иронии судьбы этот набор посвящен выборам и призывает повзрослеть. \n\nОригинальный набор тут: t.me/addstickers/pinup_girl\n💕'



* Sometimes we would want to extract the time of the post:


```python
from datetime import datetime

unixtime = data['response']['items'][1]['date'] # extracting the time info
utc = datetime.fromtimestamp(unixtime) # converting unixtime into utc
print(utc)
```

    2018-05-03 16:05:53
    

* Let's draw a wordcloud based on the text of the second post:


```python
from PIL import Image
import numpy as np
import matplotlib.pyplot as plt
from wordcloud import WordCloud, STOPWORDS

text = data['response']['items'][1]['text']

comment_mask = np.array(Image.open("C:\!!_info_!!\Desktop\Free_Blue_Star.jpg"))

stopwords = set(STOPWORDS)
stopwords.add("Светов")
stopwords.add("Михаил")

cloud = WordCloud(background_color="white", max_words=2000, mask=comment_mask, stopwords=stopwords, contour_width=5, contour_color='steelblue')

cloud.generate(text)

plt.imshow(cloud, interpolation='bilinear')
plt.axis("off")
plt.show()

cloud.to_file("post_cloud.png")
# the real size of the picture
#Image.open("post_cloud.png")
```


![png](output_17_0.png)





    <wordcloud.wordcloud.WordCloud at 0x8573f98>



* Can we download the comments? Yes, here is the method -- https://vk.com/dev/wall.getComments
* To get the post_id, click on the date of the post, you will see something like https://vk.com/id1?w=wall1_2442097 -- copy the final number from the link, in this case, 2442097


```python
import urllib.request  
req = urllib.request.Request('https://api.vk.com/method/wall.getComments?owner_id=1&post_id=2442097&count=2&need_likes=1&v=5.92&access_token=8423c2448423c2448423c244d08441f2a1884238423c244dee1644d9e90529494134bf8') 
response = urllib.request.urlopen(req) 
comments = response.read().decode('utf-8')
```


```python
print(comments)
```

    {"response":{"count":388173,"items":[{"id":2442098,"parents_stack":[],"date":1525805968,"thread":{"count":170,"items":[],"can_post":true,"show_reply_button":true,"groups_can_post":true},"deleted":true},{"id":2442100,"from_id":243752050,"post_id":2442097,"owner_id":1,"parents_stack":[],"date":1525805970,"text":"Ну чо пасаны,цифровое сопротивление\nUPD:Го 1К лайков? :D\nUPDD:Чувак сверху спиздил с сохраненки.крыса!!!","likes":{"count":3838,"user_likes":0,"can_like":1},"attachments":[{"type":"photo","photo":{"id":456244482,"album_id":-5,"owner_id":243752050,"sizes":[{"type":"m","url":"https:\/\/sun9-47.userapi.com\/c850632\/v850632550\/9685d\/LbqEM027b5A.jpg","width":119,"height":130},{"type":"o","url":"https:\/\/sun9-51.userapi.com\/c850632\/v850632550\/96861\/wapqg-NHEdE.jpg","width":130,"height":142},{"type":"p","url":"https:\/\/sun9-55.userapi.com\/c850632\/v850632550\/96862\/VnAlnZcwMgc.jpg","width":200,"height":219},{"type":"q","url":"https:\/\/sun9-34.userapi.com\/c850632\/v850632550\/96863\/SjrgzKy52HU.jpg","width":320,"height":350},{"type":"r","url":"https:\/\/sun9-56.userapi.com\/c850632\/v850632550\/96864\/HPIeAFCMaz4.jpg","width":510,"height":558},{"type":"s","url":"https:\/\/sun9-60.userapi.com\/c850632\/v850632550\/9685c\/1NTxUqK7lnA.jpg","width":69,"height":75},{"type":"x","url":"https:\/\/sun9-53.userapi.com\/c850632\/v850632550\/9685e\/kBEOX4AOOIo.jpg","width":552,"height":604},{"type":"y","url":"https:\/\/sun9-63.userapi.com\/c850632\/v850632550\/9685f\/gQwFzGyZ3nw.jpg","width":737,"height":807},{"type":"z","url":"https:\/\/sun9-48.userapi.com\/c850632\/v850632550\/96860\/Ezov7Jtfc2E.jpg","width":750,"height":821}],"text":"","date":1525806506,"access_key":"e13021f278115f48a8"}}],"thread":{"count":97,"items":[],"can_post":true,"show_reply_button":true,"groups_can_post":true}}],"current_level_count":344927,"can_post":true,"show_reply_button":true,"groups_can_post":true}}
    
