---
cases:
  - C1278889
teams: 
  - stream video
tags:
  - video
---

# description

Подмены для рекламного плейлиста (объект "pele" в дескрипторе). Для проверок, для которых требуется определённая конфигурация рекламного плейлиста, но целью проверки не является собственно рекламный плейлист:

Взаимодействие рекламы с функционалом контентного плеера: построллы и эндскрины, прероллы и автоматическая перемотка в режим марафон

Проверки рекламы внутри блока: проигрывание определённых креативов, набор блока определённой длины

Для всех блоков в подменах:
+ блоки линейные
+ длина блока — 1
+ есть моковые пиксели плейлиста, по 1 на событие для каждого блока
+ нет parameters — блоки совместимы с боевой рекламой
+ break_id с боевыми значениями — блоки совместимы с боевой рекламой

Подмены
1. Пустой плейлист &mdash; Заменяет присланный плейлист на корректный пустой плейлист
2. Преролл &mdash; Заменяет присланный плейлист на плейлист из только преролла
3. Мидролл на 20 секунде &mdash; Заменяет присланный плейлист на плейлист из только мидролла с "time_offset": "00:00:20"
4. Постролл &mdash; Заменяет присланный плейлист на плейлист из только постролла
5. Изменяет время показа мидролла &mdash; Изменяет time_offset всех рекламных блоков
6. Все блоки, мидроллы на 20 и 40 секундах &mdash; Заменяет присланный плейлист на плейлист из:
    + Преролл
    + Мидролл с "time_offset": "00:00:20"
    + Мидролл с "time_offset": "00:00:40"
    + Постролл
7. Все блоки, мидроллы на 40 и 80 секундах &mdash; Для VISION, плеер которого на 30 секунд "отключает" все метки
линейных рекламных блоков после показа рекламы.
Заменяет присланный плейлист на плейлист из:
    + Преролл
    + Мидролл с "time_offset": "00:00:40"
    + Мидролл с "time_offset": "00:01:20"
    + Постролл
8. Все блоки, мидроллы на 5 и 15 минутах
Для сериального контента, длина которого обычно 20-30 минут
Заменяет присланный плейлист на плейлист из:
    + Преролл
    + Мидролл с "time_offset": "00:05:00"
    + Мидролл с "time_offset": "00:15:00"
    + Постролл
9. Все блоки, мидроллы на 30, 60 и 90 минутах
Для единичного контента, длина которого обычно ~2 часа
Заменяет присланный плейлист на плейлист из:
    + Преролл
    + Мидролл с "time_offset": "00:30:00"
    + Мидролл с "time_offset": "01:00:00"
    + Мидролл с "time_offset": "01:30:00"
    + Постролл
10. Изменяет длину блоков &mdash;
Изменяет break_length всех рекламных блоков

----

```charles
<?xml version='1.0' encoding='UTF-8' ?>
<?charles serialisation-version='2.0' ?>
<rewriteSet-array>
  <rewriteSet>
    <active>true</active>
    <name>video-get_ad_playlist_basic_v2</name>
    <hosts>
      <locationPatterns>
        <locationMatch>
          <location>
            <path>mobileapi/video/get*</path>
          </location>
          <enabled>true</enabled>
        </locationMatch>
        <locationMatch>
          <location>
            <path>mobileapi/additional/video/get*</path>
          </location>
          <enabled>true</enabled>
        </locationMatch>
        <locationMatch>
          <location>
            <path>player/proxy/*</path>
          </location>
          <enabled>true</enabled>
        </locationMatch>
      </locationPatterns>
    </hosts>
    <rules>
      <rewriteRule>
        <active>false</active>
        <ruleType>7</ruleType>
        <matchValue>(Пустой плейлист)?&quot;pele&quot;:\s?\{(.*?&quot;playlist&quot;:\s?\[\]\}|.*?\}\]\})(?x)</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;pele&quot;: {     &quot;version&quot;: &quot;1.0&quot;,     &quot;playlist&quot;:[] }</newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>true</active>
        <ruleType>7</ruleType>
        <matchValue>(Преролл)?&quot;pele&quot;:\s?\{(.*?&quot;playlist&quot;:\s?\[\]\}|.*?\}\]\})(?x)</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;pele&quot;: {     &quot;version&quot;: &quot;1.0&quot;,     &quot;playlist&quot;:     [         {             &quot;break_id&quot;: &quot;preroll&quot;,             &quot;break_type&quot;: &quot;linear&quot;,             &quot;time_offset&quot;: &quot;start&quot;,             &quot;break_length&quot;: 1,             &quot;parameters&quot;:             {},             &quot;tracking_events&quot;:             {                 &quot;break_start&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/preroll_break_start.gif&quot;                 ],                 &quot;break_end&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/preroll_break_end.gif&quot;                 ],                 &quot;error&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/preroll_error.gif&quot;                 ]             }         }     ] }</newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>false</active>
        <ruleType>7</ruleType>
        <matchValue>(Мидролл на 20 секунде)?&quot;pele&quot;:\s?\{(.*?&quot;playlist&quot;:\s?\[\]\}|.*?\}\]\})(?x)</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;pele&quot;: {     &quot;version&quot;: &quot;1.0&quot;,     &quot;playlist&quot;:     [         {             &quot;break_id&quot;: &quot;midroll-0&quot;,             &quot;break_type&quot;: &quot;linear&quot;,             &quot;time_offset&quot;: &quot;00:00:20&quot;,             &quot;break_length&quot;: 1,             &quot;parameters&quot;:             {},             &quot;tracking_events&quot;:             {                 &quot;break_start&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-0_break_start.gif&quot;                 ],                 &quot;break_end&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-0_break_end.gif&quot;                 ],                 &quot;error&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-0_error.gif&quot;                 ]             }         }     ] }</newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>false</active>
        <ruleType>7</ruleType>
        <matchValue>(Постролл)?&quot;pele&quot;:\s?\{(.*?&quot;playlist&quot;:\s?\[\]\}|.*?\}\]\})(?x)</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;pele&quot;: {     &quot;version&quot;: &quot;1.0&quot;,     &quot;playlist&quot;:     [         {             &quot;break_id&quot;: &quot;postroll&quot;,             &quot;break_type&quot;: &quot;linear&quot;,             &quot;time_offset&quot;: &quot;end&quot;,             &quot;break_length&quot;: 1,             &quot;parameters&quot;:             {},             &quot;tracking_events&quot;:             {                 &quot;break_start&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/postroll_break_start.gif&quot;                 ],                 &quot;break_end&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/postroll_break_end.gif&quot;                 ],                 &quot;error&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/postroll_error.gif&quot;                 ]             }         }     ] }</newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>false</active>
        <ruleType>7</ruleType>
        <matchValue>Время показа мидролла()?&quot;time_offset&quot;:\s?&quot;[^&quot;]+&quot;(?x)</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;time_offset&quot;: &quot;00:00:40&quot;</newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>false</active>
        <ruleType>7</ruleType>
        <matchValue>(Все блоки, мидроллы на 20 и 40 секундах)?&quot;pele&quot;:\s?\{(.*?&quot;playlist&quot;:\s?\[\]\}|.*?\}\]\})(?x)</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;pele&quot;: {     &quot;version&quot;: &quot;1.0&quot;,     &quot;playlist&quot;:     [         {             &quot;break_id&quot;: &quot;preroll&quot;,             &quot;break_type&quot;: &quot;linear&quot;,             &quot;time_offset&quot;: &quot;start&quot;,             &quot;break_length&quot;: 1,             &quot;parameters&quot;:             {},             &quot;tracking_events&quot;:             {                 &quot;break_start&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/preroll_break_start.gif&quot;                 ],                 &quot;break_end&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/preroll_break_end.gif&quot;                 ],                 &quot;error&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/preroll_error.gif&quot;                 ]             }         },         {             &quot;break_id&quot;: &quot;midroll-0&quot;,             &quot;break_type&quot;: &quot;linear&quot;,             &quot;time_offset&quot;: &quot;00:00:20&quot;,             &quot;break_length&quot;: 1,             &quot;parameters&quot;:             {},             &quot;tracking_events&quot;:             {                 &quot;break_start&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-0_break_start.gif&quot;                 ],                 &quot;break_end&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-0_break_end.gif&quot;                 ],                 &quot;error&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-0_error.gif&quot;                 ]             }         },         {             &quot;break_id&quot;: &quot;midroll-1&quot;,             &quot;break_type&quot;: &quot;linear&quot;,             &quot;time_offset&quot;: &quot;00:00:40&quot;,             &quot;break_length&quot;: 1,             &quot;parameters&quot;:             {},             &quot;tracking_events&quot;:             {                 &quot;break_start&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-1_break_start.gif&quot;                 ],                 &quot;break_end&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-1_break_end.gif&quot;                 ],                 &quot;error&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-1_error.gif&quot;                 ]             }         },         {             &quot;break_id&quot;: &quot;postroll&quot;,             &quot;break_type&quot;: &quot;linear&quot;,             &quot;time_offset&quot;: &quot;end&quot;,             &quot;break_length&quot;: 1,             &quot;parameters&quot;:             {},             &quot;tracking_events&quot;:             {                 &quot;break_start&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/postroll_break_start.gif&quot;                 ],                 &quot;break_end&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/postroll_break_end.gif&quot;                 ],                 &quot;error&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/postroll_error.gif&quot;                 ]             }         }     ] }</newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>false</active>
        <ruleType>7</ruleType>
        <matchValue>(Все блоки, мидроллы на 40 и 80 секундах)?&quot;pele&quot;:\s?\{(.*?&quot;playlist&quot;:\s?\[\]\}|.*?\}\]\})(?x)</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;pele&quot;: {     &quot;version&quot;: &quot;1.0&quot;,     &quot;playlist&quot;:     [         {             &quot;break_id&quot;: &quot;preroll&quot;,             &quot;break_type&quot;: &quot;linear&quot;,             &quot;time_offset&quot;: &quot;start&quot;,             &quot;break_length&quot;: 1,             &quot;parameters&quot;:             {},             &quot;tracking_events&quot;:             {                 &quot;break_start&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/preroll_break_start.gif&quot;                 ],                 &quot;break_end&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/preroll_break_end.gif&quot;                 ],                 &quot;error&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/preroll_error.gif&quot;                 ]             }         },         {             &quot;break_id&quot;: &quot;midroll-0&quot;,             &quot;break_type&quot;: &quot;linear&quot;,             &quot;time_offset&quot;: &quot;00:00:40&quot;,             &quot;break_length&quot;: 1,             &quot;parameters&quot;:             {},             &quot;tracking_events&quot;:             {                 &quot;break_start&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-0_break_start.gif&quot;                 ],                 &quot;break_end&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-0_break_end.gif&quot;                 ],                 &quot;error&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-0_error.gif&quot;                 ]             }         },         {             &quot;break_id&quot;: &quot;midroll-1&quot;,             &quot;break_type&quot;: &quot;linear&quot;,             &quot;time_offset&quot;: &quot;00:01:20&quot;,             &quot;break_length&quot;: 1,             &quot;parameters&quot;:             {},             &quot;tracking_events&quot;:             {                 &quot;break_start&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-1_break_start.gif&quot;                 ],                 &quot;break_end&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-1_break_end.gif&quot;                 ],                 &quot;error&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-1_error.gif&quot;                 ]             }         },         {             &quot;break_id&quot;: &quot;postroll&quot;,             &quot;break_type&quot;: &quot;linear&quot;,             &quot;time_offset&quot;: &quot;end&quot;,             &quot;break_length&quot;: 1,             &quot;parameters&quot;:             {},             &quot;tracking_events&quot;:             {                 &quot;break_start&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/postroll_break_start.gif&quot;                 ],                 &quot;break_end&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/postroll_break_end.gif&quot;                 ],                 &quot;error&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/postroll_error.gif&quot;                 ]             }         }     ] }</newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>false</active>
        <ruleType>7</ruleType>
        <matchValue>(Все блоки, мидроллы на 5 и 15 минутах)?&quot;pele&quot;:\s?\{(.*?&quot;playlist&quot;:\s?\[\]\}|.*?\}\]\})(?x)</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;pele&quot;: {     &quot;version&quot;: &quot;1.0&quot;,     &quot;playlist&quot;:     [         {             &quot;break_id&quot;: &quot;preroll&quot;,             &quot;break_type&quot;: &quot;linear&quot;,             &quot;time_offset&quot;: &quot;start&quot;,             &quot;break_length&quot;: 1,             &quot;parameters&quot;:             {},             &quot;tracking_events&quot;:             {                 &quot;break_start&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/preroll_break_start.gif&quot;                 ],                 &quot;break_end&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/preroll_break_end.gif&quot;                 ],                 &quot;error&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/preroll_error.gif&quot;                 ]             }         },         {             &quot;break_id&quot;: &quot;midroll-0&quot;,             &quot;break_type&quot;: &quot;linear&quot;,             &quot;time_offset&quot;: &quot;00:05:00&quot;,             &quot;break_length&quot;: 1,             &quot;parameters&quot;:             {},             &quot;tracking_events&quot;:             {                 &quot;break_start&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-0_break_start.gif&quot;                 ],                 &quot;break_end&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-0_break_end.gif&quot;                 ],                 &quot;error&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-0_error.gif&quot;                 ]             }         },         {             &quot;break_id&quot;: &quot;midroll-1&quot;,             &quot;break_type&quot;: &quot;linear&quot;,             &quot;time_offset&quot;: &quot;00:15:00&quot;,             &quot;break_length&quot;: 1,             &quot;parameters&quot;:             {},             &quot;tracking_events&quot;:             {                 &quot;break_start&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-1_break_start.gif&quot;                 ],                 &quot;break_end&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-1_break_end.gif&quot;                 ],                 &quot;error&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-1_error.gif&quot;                 ]             }         },         {             &quot;break_id&quot;: &quot;postroll&quot;,             &quot;break_type&quot;: &quot;linear&quot;,             &quot;time_offset&quot;: &quot;end&quot;,             &quot;break_length&quot;: 1,             &quot;parameters&quot;:             {},             &quot;tracking_events&quot;:             {                 &quot;break_start&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/postroll_break_start.gif&quot;                 ],                 &quot;break_end&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/postroll_break_end.gif&quot;                 ],                 &quot;error&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/postroll_error.gif&quot;                 ]             }         }     ] }</newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>false</active>
        <ruleType>7</ruleType>
        <matchValue>(Все блоки, мидроллы на 30, 60 и 90 минутах)?&quot;pele&quot;:\s?\{(.*?&quot;playlist&quot;:\s?\[\]\}|.*?\}\]\})(?x)</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;pele&quot;: {     &quot;version&quot;: &quot;1.0&quot;,     &quot;playlist&quot;:     [         {             &quot;break_id&quot;: &quot;preroll&quot;,             &quot;break_type&quot;: &quot;linear&quot;,             &quot;time_offset&quot;: &quot;start&quot;,             &quot;break_length&quot;: 1,             &quot;parameters&quot;:             {},             &quot;tracking_events&quot;:             {                 &quot;break_start&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/preroll_break_start.gif&quot;                 ],                 &quot;break_end&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/preroll_break_end.gif&quot;                 ],                 &quot;error&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/preroll_error.gif&quot;                 ]             }         },         {             &quot;break_id&quot;: &quot;midroll-0&quot;,             &quot;break_type&quot;: &quot;linear&quot;,             &quot;time_offset&quot;: &quot;00:30:00&quot;,             &quot;break_length&quot;: 1,             &quot;parameters&quot;:             {},             &quot;tracking_events&quot;:             {                 &quot;break_start&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-0_break_start.gif&quot;                 ],                 &quot;break_end&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-0_break_end.gif&quot;                 ],                 &quot;error&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-0_error.gif&quot;                 ]             }         },         {             &quot;break_id&quot;: &quot;midroll-1&quot;,             &quot;break_type&quot;: &quot;linear&quot;,             &quot;time_offset&quot;: &quot;01:00:00&quot;,             &quot;break_length&quot;: 1,             &quot;parameters&quot;:             {},             &quot;tracking_events&quot;:             {                 &quot;break_start&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-1_break_start.gif&quot;                 ],                 &quot;break_end&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-1_break_end.gif&quot;                 ],                 &quot;error&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-1_error.gif&quot;                 ]             }         },                 {             &quot;break_id&quot;: &quot;midroll-2&quot;,             &quot;break_type&quot;: &quot;linear&quot;,             &quot;time_offset&quot;: &quot;01:30:00&quot;,             &quot;break_length&quot;: 1,             &quot;parameters&quot;:             {},             &quot;tracking_events&quot;:             {                 &quot;break_start&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-2_break_start.gif&quot;                 ],                 &quot;break_end&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-2_break_end.gif&quot;                 ],                 &quot;error&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/midroll-2_error.gif&quot;                 ]             }         },         {             &quot;break_id&quot;: &quot;postroll&quot;,             &quot;break_type&quot;: &quot;linear&quot;,             &quot;time_offset&quot;: &quot;end&quot;,             &quot;break_length&quot;: 1,             &quot;parameters&quot;:             {},             &quot;tracking_events&quot;:             {                 &quot;break_start&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/postroll_break_start.gif&quot;                 ],                 &quot;break_end&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/postroll_break_end.gif&quot;                 ],                 &quot;error&quot;:                 [                     &quot;https://a-bomba.tivision.ru/asset/pixel/postroll_error.gif&quot;                 ]             }         }     ] }</newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>true</active>
        <ruleType>7</ruleType>
        <matchValue>(Длина всех блоков)?&quot;break_length&quot;:\s?\d+(?x)</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;break_length&quot;:4</newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
    </rules>
  </rewriteSet>
</rewriteSet-array>
```