# jData
JSON Database
>This Class works on PHP 8 or above.
## Functions
* [Construct](#construct)
* [Select](#select)
* [Insert](#insert)
* [Update](#update)
* [Delete](#delete)
## Construct
1. File - path to file (create new file, if file not exists)
2. (optional) Structure - array of colums
```php
require "jData.php";
$jd = new jData("db.json",["key","value"]);
$jd->insert(["keyName","0"]);
/*
 +----+-----------+------------+
 | id | key       | value      |
 +----+-----------+------------+
 | 0  | keyName   | 0 (string) |
 +----+-----------+------------+
*/
```
>Returns false if structures (from db and script) doesn't equal.
## Select
1. Colum|ID - name of colum for search or direct select by id (returns whole table if null).
2. Value - string/bool/int for searching (if first argument was colum name).
Returns object (if single result) or array (if multiple results).
```php
$sel = $jd->select(); // select whole table
$sel = $jd->select(0); // select data where id = 0
$sel = $jd->select("key","keyName"); // select data where key = keyName
```
>Saves id of last result (ONLY with single result)
>Returns false if colum with that name doesn't exists or search value null (if first argument was colum name).
## Insert
1. Values - array of values for inserting
```php
$jd->insert(["keyName","0"]);
```
Returns ID of this data.
>Returns false if size of colums and values doesn't equal.
## Update
1. ID - id of data or Values (if id was saved after [select](#select)).
2. Values - array of values for inserting
```php
$sel = $jd->select(0);
$sel->key = "otherName";
$jd->update($sel); // using selected id
$jd->update(0,$sel);
```
Returns ID of this data.
>Returns false if size of colums and values doesn't equal or ID not found.
## Delete
1. (optional) ID - id of data.
```php
$jd->select(0);
$jd->delete(); // using selected id
$jd->delete(0);
```
Return boolean result of searching by ID.
