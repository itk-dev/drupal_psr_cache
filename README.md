# PSR cache implementations for Drupal 10+

Contains two modules, `drupal_psr6_cache` and `drupal_psr16_cache`, implementing PSR-6 and PSR-16 cache, respectively.

## Installation

``` shell
composer require itk-dev/drupal_psr_cache
vendor/bin/drush pm:install drupal_psr6_cache
# and/or
vendor/bin/drush pm:install drupal_psr16_cache
```

or add a composer dependency on `itk-dev/drupal_psr_cache` (see below for details).

## Usage

Add a dependency on the `drupal_psr_cache` module to a module:

``` json
# composer.json
{
    "name": "drupal/my_module",
    …
    "require": {
        "itk-dev/drupal_psr_cache": "^1.0"
    }
}
```

``` yaml
# my_module.info.yml
…
dependencies:
  - drupal:drupal_psr6_cache
  # and/or
  - drupal:drupal_psr16_cache
```

Inject the cache pool into a service:

``` yaml
# my_module.services.yml
Drupal/my_module/SomeService:
  arguments:
    $cacheItemPool: '@drupal_psr6_cache.cache_item_pool'
```

Use the cache pool:

```php
// src/SomeService.php
namespace Drupal/my_module;

use Psr\Cache\CacheItemPoolInterface;

class SomeService {
  __construct(CacheItemPoolInterface $cacheItemPool) {
    …
  }
}
```

## Development

### Tests

@todo

### Coding standards

The code must follow the [Drupal coding standards](https://www.drupal.org/docs/develop/standards).

Check coding standards (run `composer install` to install the required tools):

``` shell
composer install
composer coding-standards-apply
composer coding-standards-check
```

``` shell
docker run --rm --volume "$PWD:/md" peterdavehello/markdownlint markdownlint '**.md' --fix
docker run --rm --volume "$PWD:/md" peterdavehello/markdownlint markdownlint '**.md'
```

### Code analysis

``` shell
composer install
composer code-analysis


## References and inspiration

<https://git.drupalcode.org/project/drupal_psr_cache>
