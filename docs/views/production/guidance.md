<div class="toolbar">
    <h1>Guidance</h1>
    <div class="actions">
        <a class="action-link" href="/laravel.docs">Home</a>
    </div>
</div>

#### Environment

Some changes should be made to the .env file as
```
APP_ENV=production
APP_DEBUG=false
```

The environment constants cannot be accesses once the Laravel application is optimised for production. As a good practice the env constants should be linked to a config file and called as config('fileName.constantName').


#### Composer
The development dependencies should not be installed on a production server.
```
composer install --no-dev
```

#### Service providers and Facade Aliases
Disable by commenting the non needed service providers and unused Facade aliases.

#### Optimisation
```
composer dump-autoload -o
php artisan optimize
```

#### Server requirements
A digital ocean droplet of 2GB RAM and 1 processor would be a recommended minimum.
