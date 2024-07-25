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

If you are using Webpack, import the plugin's `webpack.config.js` file in your project's `webpack.config.js`:

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

## Step 7: Add New Packages

Add new packages in `./config/packages/assets.yaml`:

```yaml
# config/packages/assets.yaml

framework:
    assets:
        packages:
            # ...
            shop:
                json_manifest_path: '%kernel.project_dir%/public/build/shop/manifest.json'
            onepagecheckout_shop:
                json_manifest_path: '%kernel.project_dir%/public/build/zijlstratech/onepagecheckout/shop/manifest.json'
            onepagecheckout_admin:
                json_manifest_path: '%kernel.project_dir%/public/build/zijlstratech/onepagecheckout/admin/manifest.json'
```

## Step 8: Add New Build Paths

Add new build paths in `./config/packages/webpack_encore.yml`:

```yaml
# config/packages/webpack_encore.yml

webpack_encore:
    builds:
        # ...
        onepagecheckout_shop: '%kernel.project_dir%/public/build/zijlstratech/onepagecheckout/shop'
        onepagecheckout_admin: '%kernel.project_dir%/public/build/zijlstratech/onepagecheckout/admin'
```

## Step 9: Add Encore Functions to Your Templates

Add encore functions to your templates:

```twig
{# @SyliusShopBundle/_scripts.html.twig #}
{{ encore_entry_script_tags('zijlstratech-onepagecheckout-shop', null, 'onepagecheckout_shop') }}

{# @SyliusShopBundle/_styles.html.twig #}
{{ encore_entry_link_tags('zijlstratech-onepagecheckout-shop', null, 'onepagecheckout_shop') }}

{# @SyliusAdminBundle/_scripts.html.twig #}
{{ encore_entry_script_tags('zijlstratech-onepagecheckout-admin', null, 'onepagecheckout_admin') }}

{# @SyliusAdminBundle/_styles.html.twig #}
{{ encore_entry_link_tags('zijlstratech-onepagecheckout-admin', null, 'onepagecheckout_admin') }}
```

## Step 10: Install and Build Assets

If you are using Webpack, run the following commands to install and build the assets:

```bash
yarn install
yarn build
```

## Or Without Webpack:

If you are not using Webpack, install plugin assets using:

```bash
bin/console assets:install
```

Add Twig inclusions in your templates:

```twig
{# @SyliusShopBundle/_scripts.html.twig #}
{% include '@SyliusUi/_javascripts.html.twig' with {
    'path': 'bundles/zijlstratechsyliusonepagecheckoutplugin/zijlstratech-onepagecheckout-shop.js'
} %}
```

Your Sylius One Page Checkout Plugin should now be installed and configured correctly!
