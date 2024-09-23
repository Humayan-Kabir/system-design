### Bloom-Filter ![ref-alex-xu](https://www.youtube.com/watch?v=V3pzxngeLqw)
> It is a probabilistic data structure which can say following
> - probably yes : key might exists
> - firm no : key is not present
#### Algorithm
1. init a large array with 0
2. choose some good hash function, lets say we have 3 function
3. now for a key we take three hash and mark array position with 1
4. if all of them 1 that means there is a possibility that key is present otherwise it sure that key not present
5. we can't remove key
#### Usages
1. **No-SQL**
	1. when write requests comes it checks first in LMS trees, then if key not present then it needs to check all the SS-TABLE, here we can use bloom-filter to determine if key is present in this table.
2. **Cache Performance**
	1. when something is searched only once we shouldn't add it in the cache. 
3. **SS-TABLE**
	1. checks if key is present or not which helps to skip some table.
4. **CDN - Akamai**
	1. most of the web page is one hit wonders, so using bloom-filter we can determine if this web page is requested before then CDN does caching.
5. **Web Browser**
	1. for malicious web site checking, it checks first in a list of malicious site using bloom-filter. If it gets probably yes then hit remote server to verify
6. **Password Validator** 
	1. to check if password is weak

