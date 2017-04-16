---
layout: post
title: "Eliminating duplicate rows from text file in PHP"
---

Below is a simple way to do this.

```
<?
if (isset($_FILES['upload'])) {

$data = file_get_contents($_FILES['upload']['tmp_name']);

$lines = explode("\r\n", $data);
foreach ($lines as $line) {
if (in_array($line, $newlines)) continue;
$newlines[] = $line;
}

header('Content-Type: application/force-download');
header('Content-Disposition: filename=new.csv');
echo implode("\r\n", $newlines);
exit;
}
?>
```
