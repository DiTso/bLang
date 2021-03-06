# MODx EVO Lang Pack By Bumkaka

## Installing
- - -


#### 1)  Add folowing rows in `.htaccess` before: `# For Friendly URLs` 
	RewriteRule ^([a-z]{2})$ $1/ [R=301,L]
	RewriteCond %{REQUEST_FILENAME} !-f
	RewriteCond %{REQUEST_FILENAME} !-d
	RewriteRule ^([a-z]{2})/(.*)$ index.php?q=$2&lang=$1 [L,QSA]


# Use
- - -

### Examples

bLang placeholders
```
[(_root)] - link to homepage on current language
[(_lang)] - current language (ru,en,ua)
[(__someplaceholder)] - you can add different placeholders in bLang Module
```

Language selecting 
```
<select name="countries" id="select_" onchange="window.location.href = $(this).val()">
    <option value='[(_ru_url)]' [!if?is=`[(_lang)]:=:ru` &then=`selected`!]>Русский</option>
    <option value='[(_en_url)]' [!if?is=`[(_lang)]:=:en` &then=`selected`!]>English</option>
</select>
```

```
<ul class="nav inline-nav lang-select">
    <li [!if?is=`[(_lang)]:=:ua` &then=`class="active"`!]><a href="[(_ua_url)]">Укр</a></li>
    <li [!if?is=`[(_lang)]:=:ru` &then=`class="active"`!]><a href="[(_ru_url)]">Рус</a></li>
    <li [!if?is=`[(_lang)]:=:en` &then=`class="active"`!]><a href="[(_en_url)]">Eng</a></li>
</ul>
```


EForm
```
[!eForm? 
&to=`bumkaka@yandex.ru`
&formid=`QaForm` 
&subject=`Вопрос с сайта` 
&tpl=`eQaForm_[(_lang)]` 
&report=`eQaReport` 
&gotoid=`[*id*]` 
&vericode=`0` 
&language=`[[switch?ru=`russian-UTF8` &en=`english`]]`
!] 
```

Wayfinder
```
[[Wayfinder? &startId=`0` &outerClass=`menu` &level=`1` &firstClass=`first` &rowTpl=`MenuRowTpl`]]
```
tpl-`MenuRowTpl`:
```
<li [+wf.classes+] id="id[+wf.docid+]">
	<a href="[(_root)][~[+wf.docid+]~]" title="[[switch?ru=`[+pagetitle_ru+]` &en=`[+pagetitle_en+]` &fr=`[+pagetitle_fr+]`]]">
	[[switch?
		&ru=`[[if?is=`[+menutitle_ru+]:=:` &then=`[+pagetitle_ru+]` &else=`[+menutitle_ru+]`]]` 
		&en=`[[if?is=`[+menutitle_en+]:=:` &then=`[+pagetitle_en+]` &else=`[+menutitle_en+]`]]` 
		&fr=`[[if?is=`[+menutitle_fr+]:=:` &then=`[+pagetitle_fr+]` &else=`[+menutitle_fr+]`]]
	`]]
</a>[+wf.wrapper+]</li>

```

DocLister
```
[[DocLister? 
&tvPrefix=`` 
&tvList=`pagetitle_ua,pagetitle_ru,pagetitle_en` 
&tpl=`@CODE:<li data-value="[(_root)][+url+]">[+pagetitle_[(_lang)]+]</li>`
&orderBy=`menuindex ASC` 
&parents=`17`]]
```





Switch

 ``` [[switch? &name=`pagetitle`]] ``` //if you know the name of the field
 ``` [[switch? &pl=`pagetitle]] ```    //if you know the name of the placeholder



##Automatic translation
  if you need an automatic translation into other languages of the resource you should
  1. Get the key yandex api
  2. Open the plugin settings blang.
  3. Set 1 in field translate
  4. Set yandex key in field
  You can only translate from the main language in the form.
  To translate, simply save the document.
  
  
## module bLang
In addition to the chunk you can save the language settings in the blang module.
It also supports auto translation, but you have to enter the Yandex api key in its setting
If you need other languages other than (ru,en,ua), you must add a new line to the blang table

# Attention 
 To create a table in the database you must tick Check Install / Rewrite Demo Content