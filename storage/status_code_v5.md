---
cases:
  - C1278889. 6703596, 6703597
team: stream video
tags:
  - video
---

# description
Набор подмен позволяет менять код состояния для **указанных ниже** запросов:
+ /mobileapi/video/get/            &mdash; Дескриптор контента
+ /mobileapi/tvchannel/get/        &mdash; Дескриптор тв-канала
+ /mobileapi/additional/video/get/ &mdash; Дескриптор дополнительного материала
+ /mobileapi/broadcast/get/        &mdash; Дескриптор трансляции
+ fairplay*ivi.ru                  &mdash; Запрос лицензии в случае DRM FairPlay
+ widevine*ivi.ru                  &mdash; Запрос лицензии в случае DRM Widevine (Вариант для k8s)
+ w.ivi.ru                         &mdash; Запрос лицензии в случае DRM Widevine (Вариант для production)
+ player.mediavitrina.ru/*sdk.json &mdash; Запрос конфига плеера Витрина ТВ
+ /pivi/flow.FlowService/Get       &mdash; Запрос элемента/ов ленты Потока
+ /mobileapi/broadcasts/*?compilation_group=true &mdash; Запрос трансляций других сериалов для блока на КТТ
+ /mobileapi/broadcast/status/* &mdash; Запрос статуса трансляции
+ /mobileapi/compilation/favourite/v5/check* &mdash; Запрос проверки наличия контента в очереди

Подмены
1.	Заменяет код состояния на 500
2.	Заменяет код состояния на 403
3.	Заменяет общий статус запроса на Failed
----

```charles
<?xml version='1.0' encoding='UTF-8' ?>
<?charles serialisation-version='2.0' ?>
<rewriteSet-array>
  <rewriteSet>
    <active>true</active>
    <name>status_code_v5</name>
    <hosts>
      <locationPatterns>
        <locationMatch>
          <enabled>false</enabled>
          <location>
            <path>/mobileapi/video/get/*</path>
            <query>*</query>
          </location>
        </locationMatch>
        <locationMatch>
          <enabled>false</enabled>
          <location>
            <path>/mobileapi/tvchannel/get/*</path>
            <query>*</query>
          </location>
        </locationMatch>
        <locationMatch>
          <enabled>false</enabled>
          <location>
            <path>/mobileapi/additional/video/get/*</path>
            <query>*</query>
          </location>
        </locationMatch>
        <locationMatch>
          <enabled>false</enabled>
          <location>
            <path>/mobileapi/broadcast/get/*</path>
            <query>*</query>
          </location>
        </locationMatch>
        <locationMatch>
          <enabled>false</enabled>
          <location>
            <host>fairplay*ivi.ru</host>
          </location>
        </locationMatch>
        <locationMatch>
          <enabled>false</enabled>
          <location>
            <host>widevine*ivi.ru</host>
          </location>
        </locationMatch>
        <locationMatch>
          <enabled>false</enabled>
          <location>
            <host>w.ivi.ru</host>
          </location>
        </locationMatch>
        <locationMatch>
          <enabled>false</enabled>
          <location>
            <host>player.mediavitrina.ru</host>
            <path>*sdk.json</path>
          </location>
        </locationMatch>
        <locationMatch>
          <enabled>false</enabled>
          <location>
            <path>/pivi/flow.FlowService/Get</path>
          </location>
        </locationMatch>
        <locationMatch>
          <enabled>false</enabled>
          <location>
            <protocol></protocol>
            <host>a-bomba.tivision.ru</host>
            <path>asset/video/vast_video.mp4</path>
            <query>*chain_number=2</query>
          </location>
        </locationMatch>
        <locationMatch>
          <enabled>false</enabled>
          <location>
            <path>*html</path>
            <query>*chain_number=2</query>
          </location>
        </locationMatch>
        <locationMatch>
          <enabled>false</enabled>
          <location>
            <path>/pivi/flow.FlowService/Get</path>
          </location>
        </locationMatch>
        <locationMatch>
          <enabled>false</enabled>
          <location>
            <path>/mobileapi/broadcasts/*</path>
            <query>compilation_group=true</query>
          </location>
        </locationMatch>
        <locationMatch>
          <enabled>false</enabled>
          <location>
            <path>/mobileapi/broadcast/status/*</path>
          </location>
        </locationMatch>
        <locationMatch>
          <location>
            <path>mobileapi/compilation/favourite/v5/check*</path>
          </location>
        </locationMatch>
      </locationPatterns>
    </hosts>
    <rules>
      <rewriteRule>
        <active>true</active>
        <ruleType>11</ruleType>
        <matchValue></matchValue>
        <matchResponse>true</matchResponse>
        <newValue>500 Internal Server Error</newValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <ruleType>11</ruleType>
        <matchValue></matchValue>
        <matchResponse>true</matchResponse>
        <newValue>403 Forbidden</newValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>true</active>
        <ruleType>11</ruleType>
        <matchValue></matchValue>
        <matchResponse>true</matchResponse>
        <newValue>Failed</newValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <ruleType>11</ruleType>
        <matchValue></matchValue>
        <matchResponse>true</matchResponse>
        <newValue>400 Bad Request</newValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
    </rules>
  </rewriteSet>
</rewriteSet-array>
```