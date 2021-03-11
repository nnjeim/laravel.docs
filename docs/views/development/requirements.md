<div class="toolbar">
    <h1>Requirements</h1>
    <div class="actions">
        <a class="action-link" href="/laravel.docs">Home</a>
    </div>
</div>

### PHP
The general php requirements are:

* PHP >= 7.2.5
* BCMath PHP Extension
* Ctype PHP Extension
* Fileinfo PHP extension
* JSON PHP Extension
* Mbstring PHP Extension
* OpenSSL PHP Extension
* PDO PHP Extension
* Tokenizer PHP Extension
* XML PHP Extension

```
brew install php@7.4 or php@8.0
```
To validate the installation of the required php extensions run php -i

### Redis
Redis >=v5 is required if the package CrowdFavorite/Perist is to be used for caching.

In addition the extension redis.so should be installed and enabled.
```
git clone https://www.github.com/phpredis/phpredis.git
cd phpredis
phpize && ./configure && make && sudo make install

Add extension=redis.so in your php.ini
```
