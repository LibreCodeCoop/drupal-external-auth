[![Build Status](https://travis-ci.org/lyseontech/drupal-external-auth.svg?branch=master)](https://travis-ci.org/lyseontech/drupal-external-auth)
[![Coverage Status](https://coveralls.io/repos/github/lyseontech/drupal-external-auth/badge.svg?branch=master)](https://coveralls.io/github/lyseontech/drupal-external-auth?branch=master)
[![PHPStan](https://img.shields.io/badge/PHPStan-enabled-brightgreen.svg?style=flat)](https://github.com/phpstan/phpstan)
[![Latest Stable Version](https://poser.pugx.org/lyseontech/drupal-external-auth/v/stable)](https://packagist.org/packages/lyseontech/drupal-external-auth)
[![Minimum PHP Version](https://img.shields.io/badge/php-%3E%3D%207-blue.svg)](https://php.net/)
[![License](https://poser.pugx.org/lyseontech/drupal-external-auth/license)](https://packagist.org/packages/lyseontech/drupal-external-auth)

# Drupal External Auth

Composer package to externally authenticate Drupal users

If the user exists in Drupal, authenticates the user.

If the user does not exist in Drupal, it creates the user and authenticates.

## How to use?

```bash
composer require lyseontech/drupal-external-auth
```

```php
$response = new Response();
$pdo = new PDO(...);

(new \DrupalExternalAuth\Auth($pdo))->auth([
    'name'     => 'username',
    'pass'     => 'PrefixHash$' . 'hashOfPassord',
    'timezone' => 'America/Sao_Paulo',
    'langcode' => 'pt-br',
    'roles' => ['administrator']
]);

foreach ($response->headers->getCookies() as $cookie) {
    header('Set-Cookie: '.$cookie->getName().strstr($cookie, '='));
}
```

In PrefixHash, put the prefix hash to identify the hash password from your
system.

In hashPassord put the hash for user, if don't is necessary the user
authenticate in Drupal by default login page of Drupal, put anything in this
field.

If you dont implement custom validation hash in Drupal, the user can only
access Drupal through your system.