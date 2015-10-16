# Notes on Symfony #

## How to map Doctrine Entity to a custome location  ##

``` 
File: app/confi/config.yml

doctrine:
    dbal:
        driver:   pdo_mysql
        host:     "%database_host%"
        port:     "%database_port%"
        dbname:   "%database_name%"
        user:     "%database_user%"
        password: "%database_password%"
        charset:  UTF8
    orm:
        auto_generate_proxy_classes: "%kernel.debug%"
        naming_strategy: doctrine.orm.naming_strategy.underscore
        auto_mapping: false
        mappings:
            UserEntity:
                type: yml
                dir: %kernel.root_dir%/../src/AppBundle/Users/config  # Location of the Entity Schema file UserEntity.orm.yml
                prefix: AppBundle\Users  # Parent Folder
                alias: UserEntity  # Entity name
                is_bundle: false
```
### Support full Unicode in MySQL databases ###

To save a Unicode Characters like this ( ❤ ☀ ☆ ☂ ☻ ♞ ☯ ☭ ☢ € → ) into your database :

1. Set your database Collation as:   
 ``` utf8mb4_unicode_ci ```    
2. Set Doctrine charset as:  
``` UTF8MB4 ```

```
File: app/confi/config.yml

doctrine:
    dbal:
        driver:   pdo_mysql
        host:     "%database_host%"
        port:     "%database_port%"
        dbname:   "%database_name%"
        user:     "%database_user%"
        password: "%database_password%"
        charset:  UTF8MB4 # Unicode Support
    
