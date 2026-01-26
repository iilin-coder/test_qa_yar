---
cases:
  - C1278889
team: stream video
tags:
  - video, app. feature
name: Дескрипшн есть тег, но нет текста
---

# description
----

```charles
<?xml version='1.0' encoding='UTF-8' ?>
<?charles serialisation-version='2.0' ?>
<rewriteSet-array>
  <rewriteSet>
    <active>true</active>
    <name>FeatureTooggle</name>
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
    </rules>
  </rewriteSet>
</rewriteSet-array>