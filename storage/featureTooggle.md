---
cases:
  - C1278889, 6703596
team: stream video, stream ux, turk
tags:
  - video, app. feature
name: Мок для параметров appversion
---

# description
1. Добавляет фича тоггл на андроид
2. Добавляет  фича тоггл на айос
3. обавляет  фича тоггл для смарт тв
----

```charles
<?xml version='1.0' encoding='UTF-8' ?>
<?charles serialisation-version='2.0' ?>
<rewriteSet-array>
  <rewriteSet>
    <active>true</active>
    <name>&lt;M&gt; FeatureTooggle</name>
    <hosts>
      <locationPatterns>
        <locationMatch>
          <location>
            <path>/mobileapi/appversioninfo/v5/</path>
          </location>
          <enabled>true</enabled>
        </locationMatch>
      </locationPatterns>
    </hosts>
    <rules>
      <rewriteRule>
        <active>false</active>
        <ruleType>7</ruleType>
        <matchValue>Android</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>false</matchValueRegex>
        <matchRequest>true</matchRequest>
        <matchResponse>false</matchResponse>
        <newValue></newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>true</active>
        <ruleType>7</ruleType>
        <matchValue>&quot;feature_toggles&quot;:\s?\[</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;feature_toggles&quot;: [&quot;NameFeatureToggle&quot;, </newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>false</active>
        <ruleType>7</ruleType>
        <matchValue>iOS</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>false</matchValueRegex>
        <matchRequest>true</matchRequest>
        <matchResponse>false</matchResponse>
        <newValue></newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>true</active>
        <ruleType>7</ruleType>
        <matchValue>(&quot;feature_toggles&quot;\s*:\s*\{)</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>$1&quot;name_feature_toggle&quot;:{&quot;is_enabled&quot;:true},</newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>false</active>
        <ruleType>7</ruleType>
        <matchValue>Smart</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>false</matchValueRegex>
        <matchRequest>true</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue></newValue>
        <newHeaderRegex>false</newHeaderRegex>
        <newValueRegex>false</newValueRegex>
        <matchWholeValue>false</matchWholeValue>
        <caseSensitive>false</caseSensitive>
        <replaceType>2</replaceType>
      </rewriteRule>
      <rewriteRule>
        <active>true</active>
        <ruleType>7</ruleType>
        <matchValue>&quot;feature_toggles&quot;:\s?\[</matchValue>
        <matchHeaderRegex>false</matchHeaderRegex>
        <matchValueRegex>true</matchValueRegex>
        <matchRequest>false</matchRequest>
        <matchResponse>true</matchResponse>
        <newValue>&quot;feature_toggles&quot;:\s?\[</newValue>
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