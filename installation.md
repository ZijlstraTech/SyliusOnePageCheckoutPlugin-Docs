# Sylius One Page Checkout Plugin Installation Guide

Follow the steps below to install and configure the Sylius One Page Checkout Plugin.

## Step 1: Update `composer.json`

Add the repository to your `composer.json` file:

```json
{
    "repositories": [
        {
            "type": "vcs",
            "url": "git@github.com:ZijlstraTech/SyliusOnePageCheckoutPlugin.git"
        }
    ]
}
```

## Step 2: Require the Plugin

Run the following command to require the plugin:

```bash
composer require zijlstratech/sylius-one-page-checkout-plugin
```

## Step 3: Register the Plugin

Add the plugin dependencies to your `config/bundles.php` file:

```php
return [
    // ...
    ZijlstraTech\SyliusOnePageCheckoutPlugin\ZijlstraTechSyliusOnePageCheckoutPlugin::class => ['all' => true],
];
```

## Step 4: Import Required Configuration

Import the required configuration in your `config/packages/_sylius.yaml` file:

```yaml
# config/packages/_sylius.yaml

imports:
    # ...
    - { resource: "@ZijlstraTechSyliusOnePageCheckoutPlugin/Resources/config/config.yml" }
```

## Step 5: Update Shop Routing Configuration

Add the following to the top of your `sylius_shop.yaml` file:

```yaml
Zijlstratech_sylius_onepagecheckout_shop:
    resource: "@ZijlstraTechSyliusOnePageCheckoutPlugin/Resources/config/shop_routing.yml"
    prefix: /{_locale}
    requirements:
        _locale: ^[a-z]{2}(?:_[A-Z]{2})?$
```

## Step 6: Import Plugin's Webpack Configuration

Import the plugin's `webpack.config.js` file in your project's `webpack.config.js`:

```javascript
// webpack.config.js

const [ zijlstratechOnePageCheckoutShop, zijlstratechOnePageCheckoutAdmin ] = require('./vendor/zijlstratech/sylius-one-page-checkout-plugin/webpack.config.js');

// ...
module.exports = [
    // ...
    zijlstratechOnePageCheckoutShop, 
    zijlstratechOnePageCheckoutAdmin
];
```

## Step 7: Install and Build Assets

Finally, run the following commands to install and build the assets:

```bash
yarn install
yarn build
```

Your Sylius One Page Checkout Plugin should now be installed and configured correctly!

