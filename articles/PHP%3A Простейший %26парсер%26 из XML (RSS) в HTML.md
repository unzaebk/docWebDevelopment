
 Элементарнейший парсер - который обрабатывает xml-документ и выводит информацию ввиде html, т.е. к примеру, вы можете брать Rss любого сайта и, используя данный скрипт, выводить его содержимое на своем сайте.   
 
 ![](/images/802f24751e94388c97fff42291715e3b.png) 
 
 Пример, указанный ниже, предназначен для rss с сайта bash.org.ru. На данном примере можно построить свой "парсер" из rss(xml). Используется расширение для PHP - SIMPLEXML. Для тех,кто знаком с расширением SIMPLEXML, этот пример вообще не должен вызывать вопросы.
 
```php
<?php 
$xml = simplexml_load_file('http://bash.org.ru/rss/'); 
foreach ($xml->xpath('//item') as $item) 
{ 
	echo "<b><a href='$item->guid'>$item->title<br/></a></b>$item->description<hr/>"  ; 
} 
?>
```

**********
[PHP](/tags/PHP.md)
[RSS](/tags/RSS.md)
[SimpleXML](/tags/SimpleXML.md)
[XML](/tags/XML.md)
