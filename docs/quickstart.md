---
title: Quickstart
---

# Quickstart

## PHP

```bash
git clone https://github.com/siesta-php/siesta-php.git
cd siesta-php
composer install
php tools/siesta-cli/bin/siesta discover
php tools/siesta-cli/bin/siesta validate
```

Embed in your app:

```php
use Siesta\Runtime\SiestaKernel;

$siesta = SiestaKernel::discover(__DIR__);
$result = $siesta->handle('siesta.create', [
    'library' => 'siesta-carbon',
    'factory' => 'now',
    'args' => [],
]);
```

## TypeScript

```bash
git clone https://github.com/siesta-php/siesta-ts.git
cd siesta-ts
npm install && npm run build
npm run discover
```

No standalone server — applications discover manifest files and handle protocol calls in-process.
