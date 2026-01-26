---
cases:
  - C1278889
team: stream video

tags:
  - video
name: Мок для параметров appversion
---

# description
1. Добавляет параметр для отправки QoS событий по одному на SmartTV
2. Добавляет параметр, выставляющий таймаут на запуск файла в 10 секунд на SmartTV  (дефолтное значение 30с)
3. Добавляет параметр, выставляющий таймаут на буфферизацию файла в 5 секунд на SmartTV  (дефолтное значение 10с)
4. Добавляет параметр для управления стартовым качеством при воспроизведении ABR на SmartTV – примерные значения указаны в задаче VISION-13051 - [Player] Добавить настройку стартового битрейта для адаптивного качества VOD плеера Закрыто
5. Изменяет параметр, отвечающий за отправку groot событий по https. Позволяет видеть groot на SmartTV
6. Добавляет параметр для изменения времени жизни ссылок на медиафайлы – для тестирования выхода из спящего режима
7. Изменяет значение параметра default_video_content_quality на невалидное
8. Изменяет значение параметра default_video_trailer_quality на невалидное
9. Добавляет объект flow_config для flow_stb
10. Позволяет изменить ограничение по битрейту для режима экономии трафика
11. Добавляет объект flow_config для flow_mobile
12. Добавляет объект vert_config — https://confluence.ivi.ru/pages/viewpage.action?pageId=444570281#id-ВертикальныесериалыakaКарликовыесериалыakaСтыдныесериалы-Конфигурированиеплеера
13.	Добавляет свойство оптимизации для легкого плеера при быстрой смене контента
14.	Добавляет список url ivi proxy для android config
15.	Добавляет свойство timeout_for_svpk_in_player
16.	Добавляет свойство ttl_for_svpk_informer_in_player
----

```charles
<?xml version='1.0' encoding='UTF-8' ?>
<?charles serialisation-version='2.0' ?>
<rewriteSet-array>
  <rewriteSet>
    <active>true</active>
    <name>appversioninfo_parameters_v11</name>
    <hosts>
      <locationPatterns>
        <locationMatch>
          <location>
            <path>mobileapi/appversioninfo/v5/</path>
          </location>
          <enabled>true</enabled>
        </locationMatch>
      </locationPatterns>
    </hosts>
    <rules>
      <rewriteRule>
        <active>true</active>
        <ruleType>7</ruleType>
        <matchValue>(Отправка qos по 1 — SmartTV)&quot;parameters&quot;:\s?\{</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;parameters&quot;:{&quot;qos_pack_disabled&quot;: true,</newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>false</active>
        <ruleType>7</ruleType>
        <matchValue>(Таймаут на запуск файла — SmartTV)?&quot;parameters&quot;:\s?\{</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;parameters&quot;:{&quot;video_hangup_timeout_ms&quot;:5000,</newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>false</active>
        <ruleType>7</ruleType>
        <matchValue>(Таймаут на stall — SmartTV)?&quot;parameters&quot;:\s?\{</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;parameters&quot;:{&quot;video_buffering_timeout_ms&quot;:5000,</newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>false</active>
        <ruleType>7</ruleType>
        <matchValue>(Auto — SmartTV)?&quot;parameters&quot;:\s?\{</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;parameters&quot;:{&quot;abr_default_bandwidth&quot;:2668000,</newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>false</active>
        <ruleType>7</ruleType>
        <matchValue>(Грут по http — SmartTV)?&quot;groot_https&quot;:\s?.*?,</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;groot_https&quot;: false,</newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>false</active>
        <ruleType>7</ruleType>
        <matchValue>(Время жизни ссылок — SmartTV)&quot;parameters&quot;:\s?\{</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;parameters&quot;:{&quot;descriptor_living_interval_ms&quot;:420000,</newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>false</active>
        <ruleType>7</ruleType>
        <matchValue>(Дефолт качество контента — SmartTV)?&quot;default_video_content_quality&quot;:\s*?&quot;.*?&quot;</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;default_video_content_quality&quot;:&quot;undefined&quot;</newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>false</active>
        <ruleType>7</ruleType>
        <matchValue>(Дефолт качество трейлера — SmartTV)?&quot;default_video_trailer_quality&quot;:\s*?&quot;.*?&quot;</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;default_video_trailer_quality&quot;:&quot;undefined&quot;</newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>false</active>
        <ruleType>7</ruleType>
        <matchValue>(Добавление flow_config — SmartTV)&quot;parameters&quot;:\s?\{</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;parameters&quot;:{&quot;flow_config&quot;:{&quot;flow_type&quot;:&quot;flow_stb&quot;,&quot;item_count_to_cache&quot;:5,&quot;timeout_for_full_reload_sec&quot;:25200,&quot;timeout_for_one_element_sec&quot;:30},</newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>false</active>
        <ruleType>7</ruleType>
        <matchValue>(Экономия трафика)?&quot;preferred_peak_bitrate_for_economy_mode_bps&quot;:\s*\d+</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;preferred_peak_bitrate_for_economy_mode_bps&quot;:38000000</newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>false</active>
        <ruleType>7</ruleType>
        <matchValue>(Добавление flow_config — Mobile)?&quot;parameters&quot;:\s?\{</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;parameters&quot;:{&quot;flow_config&quot;: {&quot;flow_type&quot;: &quot;flow_mobile&quot;,&quot;item_count_to_cache&quot;: 4,&quot;item_count_to_cache_back&quot;: 1,&quot;segment_to_show_flow_on_start&quot;: &quot;show_flow_on_start&quot;,&quot;timeout_for_full_reload_sec&quot;: 1800,&quot;timeout_for_one_element_sec&quot;: 10},</newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>false</active>
        <ruleType>7</ruleType>
        <matchValue>(Добавление vert_config)?&quot;parameters&quot;:\s?\{</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;parameters&quot;:{&quot;vert_config&quot;:{&quot;item_count_to_cache&quot;:5,&quot;item_count_to_cache_back&quot;:1,&quot;timeout_for_one_element_sec&quot;:10},</newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>false</active>
        <ruleType>7</ruleType>
        <matchValue>(Оптимизация при смене контента - android)?&quot;parameters&quot;:\s?\{</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;parameters&quot;:{&quot;embedded_dynamic_content_optimizations&quot;: true,</newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>false</active>
        <ruleType>7</ruleType>
        <matchValue>(url_ivi_proxy - android)?&quot;android_player_config&quot;:\s?\{</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;android_player_config&quot;: {&quot;widevine_proxy_list&quot;: [&quot;http://217.16.20.211:9950&quot;, &quot;http://217.16.20.211&quot;, &quot;http://217.16.20.211/widevine/license&quot;, &quot;http://217.16.20.211:9950/widevine/license&quot;],</newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>false</active>
        <ruleType>7</ruleType>
        <matchValue>(Добавление timeout_for_svpk_in_player)?&quot;parameters&quot;:\s?\{</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;parameters&quot;:{&quot;timeout_for_svpk_in_player&quot;:30,</newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>true</active>
        <ruleType>7</ruleType>
        <matchValue>(Добавление ttl_for_svpk_informer_in_player)?&quot;parameters&quot;:\s?\{</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;parameters&quot;:{&quot;ttl_for_svpk_informer_in_player&quot;:10,</newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
    </rules>
  </rewriteSet>
  <null/>
</rewriteSet-array>
```