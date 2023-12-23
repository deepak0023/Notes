## Notes

### Vagrant :
- virtualbox is a tool to run a virtual machine in the system
- vagrant is automation of virtualbox

#### Commands
```bash
vagrant init "<box-name>"
vagrant up
vagrant reload
vagrant halt
vagrant box list
vagrant status
vagrant destroy
vagrant global --status
vagrant global --status -- prune
```

### Redis :
- Provides key:value pair in memmory storage
- Data persistence by backing up the data to hard disk
- Json support
- Search feature
- Redis OM (object mapping)

### Redis main datatypes
- string ['abc', '20']
- set {'abc', 'efg'}
- hashes {title: 'abc', author: 'efg'}
- lists {'abc', 'efg'}
- sorted set {'abc':1, 'efg':2} (value is score)

#### String commands
```bash
set <key> <value>
keys *
get <key> <value>
del <key>
set <key1> <value1> <key2> <value2>
getrange <key> <initial-index> <final-index> (eg : getrange <key> 0 3, getrange <key> -1 -2)
setrange <key> <index> <value> (setname name 2 abc -> naabc )
incr <age>
incrby <key> <value>
decrby <key> <value>
set <key> <value> ex <seconds> (remove/expire the key after few seconds)
set <key> <value> get (set new value and get old value of the key)
```

#### Set commands [allows only unique values]
```bash
sadd <key> <value>
sadd <key> <value1> <value2>
smembers <key>
srem <key> <value>
sunion <key1> <key2> (array_merge())
sismember <key> <value> (in_array())
scard <key> (to get number i=of items in set)
```

#### List commands [allows duplicate values] (linked list)
```bash
sadd <key> <value>
sadd <key> <value1> <value2>
smembers <key>
srem <key> <value>
sunion <key1> <key2> (array_merge())
sismember <key> <value> (in_array())
scard <key> (to get number i=of items in set)
```

#### Hashmap [can only have string as value] (for other types serialise)
```bash
hset books:1 <key> <value>
hget <key> <value>
hgetall <key>
hexist <key> <hash-key>
hkeys <key>
hdel <key> <hash-key>
del <key>
hvals <key>
hmset <keys> <val> <key> <val>
```

#### Json
```bash
JSON.SET authors:1 $ '{
	"name": "sample name",
	"age": "12",
	"books" [
		"name": "name_1",
		"value" : "value_1
	]}' 

JSON.GET authors:1 $name.books[0].name
JSON.SET authors:1 $name.books[0].value value2
```

### Laravel Lifecyclle :
- (apache/nginx) public/index.php 
- composer autoload 
- create application instance from bootstrap/app.php (service container) 
- http kernal or console kernal 
- app/http/kernal.php ()
- parent class Illuminate\Foundation\Http\Kernel (error handling, configure logging,  detect the application environment) [internal laravel configuration]
- http kernal to middleware (handles reading and wrting http sessions, maintanenece mode check, verify csrf token)
- service providers [database, queues, validation, routing components]
- create instance of service providers and then movr to register method
- boot method on all providers
- route service provider has registered router object thamove throug route, middleware, and controller action (authentication code in middleware)
- post middleware action also possible after each request after $next()
- response -> kernal handle() -> piblic index.php send() -> browser 

### Laravel env :

```bash
if (App::environment('local')) {
    // The environment is local
}

if (App::environment(['local', 'staging'])) {
    // The environment is either local OR staging...
}

.env key encrytion [default : AES-256-CBC]
LARAVEL_ENV_ENCRYPTION_KEY
php artisan env:encrypt
php artisan env:decrypt
php artisan env:decrypt --key=qUWuNRdfuImXcKxZ --cipher=AES-128-CBC
php artisan env:decrypt --env=staging [env.staging]
```

### Laravel maintenance mode :
```bash
php artisan down [laravel maintanence mode]
php artisan down --redirect=/
```

### Laravel queue commands
```bash
php artisan queue:work --tries=3 [if exception is thrown inside job then it will try endlessly]
php artisan queue:failed  [running this again after failed attemps will not run the queue with (php artisan queue:work) need to go with (php artisan queue:retry)]
php artisan queue:retry <uuid> [uuid of the job]
php artisan queue:retry all [retry all failed jobs]
php artisan queue:work --queue="high,default"
php artisan queue:work --once [only perform the very next queue not others]
```

#### Laravel horizon [Monitoring queues on redis]
```bash
composer require laravel/horizon
php artisan horizon:install
php artisan horizon
```

#### Laravel telescope [Monitoring request and cache in laravel]
```bash
composer require laravel/telescope
php artisan telescope:install
php artisan telescope:purne
```


### Phpunit
```bash
vendor/bin/phpunit 
vendor/bin/phpunit --filter test_add_numbers
php artisan test
php artisan test --log-events-verbose-text test.log
vendor/bin/phpunit --list-tests
```

### Pint [build on cs-code-fixer]
```bash
vendor/bin/pint --test                 [give the list of files over which changes will be done]
./vendor/bin/pint --dirty              [do changes only on uncommited files]
vendor/bin/pint                        [update changes in the code file]
./vendor/bin/pint app/Models/User.php  [on specific file]
./vendor/bin/pint app/Models           [on specific folder]
```

### Solid Principle
- Single Responsibility Principle [Different class for different functionality]
- Open/Close Principle [Open for extension and and closed for modification]
- Liskov's Principle [Return types must be same for interface subclass implementation]
- Interface Segregation [Seperate interfaces if needed for different implementations on sub classes]
- Dependency inversion [Have intefaces to decouple the calling class from the implementation class]

### Main design patterns
- Singleton pattern [use same object]
- Decorator pattern [nested object implementation , passes through each class functions]
- Adaptor pattern [have the interface class mapping common functions map to implementation functions]
- Template method pattern [main to abstract to implementation function]
- Strategy Pattern [comman main to interface to subclass flow]
- Chain of responsibility pattern [attach one class to another and on execution flow on that chain to execute]
- Observer Pattern [event class connecting to different observer classes through interface]

### OSI Model
- Application Layer [HTTP, FTP, SSH, SMTP]
- Transport Layer [TCP, UDP]
- Network Layer [IP]
- Link [Router, Switches]
- Phisical [Phisical Wires]

### HTTP Codes
- 100 Range [information response]
- 200 Range [success codes]
- 300 Range [codes of redirect]
- 400 Range [user/client error codes]
- 500 Range [server error]
