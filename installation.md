# ZijlstraTech SyliusOnePageCheckoutPlugin

## Installation


1. 

```bash
$ composer require zijlstratech/sylius-one-page-checkout-plugin
```

2. Add plugin dependencies to your `config/bundles.php` file:
```php
// config/bundles.php

return [
    ...

    ZijlstaTech\SyliusOnePageCheckoutPlugin\ZijlstraTechSyliusOnePageCheckoutPlugin::class => ['all' => true],
];
```

3. Import required config in your `config/packages/_sylius.yaml` file:
```yaml
# config/packages/_sylius.yaml

imports:
    ...

    - { resource: "@ZijlstraTechSyliusOnePageCheckoutPlugin/Resources/config/config.yml" }
```

4. Import routing in your `config/routes.yaml` file:

```yaml
# config/routes.yaml

zijlstratech_one_page_checkout_plugin:
    resource: "@ZijlstraTechSyliusOnePageCheckoutPlugin/Resources/config/routing.yml"
```

5. Clear application cache by using command:

```bash
$ bin/console cache:clear
```
