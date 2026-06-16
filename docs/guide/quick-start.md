# Quick Start — Up and Running in 5 Minutes

::: tip Who this page is for
You understand Magento architecture and eBay seller workflows. You just need the key variables and sequential roadmap.
:::

## The Big Picture

| Step | Task | Estimated Time | Reference Guide |
| ---- | ---- | -------------- | --------------- |
| 1 | Upload & compile module | 3 min | [Installation](/guide/installation.html) |
| 2 | Register eBay app & get tokens | 5 min | [eBay Credentials](/guide/ebay-credentials.html) |
| 3 | Input settings & authorize | 2 min | [Module Settings](/guide/module-settings.html) |
| 4 | Map categories & import products | 5 min | [Map Category](/guide/map-category.html) · [Import Product](/guide/import-product-from-ebay.html) |
| **Total** | | **~15 min** | |

## Preparation Checklist

- [ ] Magento 2.4.x installation is operational.
- [ ] SSL/HTTPS is provisioned globally.
- [ ] eBay Developer Program account created at [developer.ebay.com](https://developer.ebay.com).
- [ ] eBay seller account (Sandbox for testing, Production for live).
- [ ] `composer require webkul/ebayconnector` dependency available.

---

## Step-by-Step Fast Path

### 1. Install the Module

1. Upload module files to `app/code/Webkul/Ebaymagentoconnect`.
2. Run from Magento root:

```bash
composer require webkul/ebayconnector
php bin/magento setup:upgrade
php bin/magento setup:di:compile
php bin/magento setup:static-content:deploy -f
php bin/magento indexer:reindex
php bin/magento cache:flush
```

3. Confirm **eBay Magento Connect** appears in the admin menu.

See full details: [Installation](/guide/installation.html)

### 2. Register eBay Application & Get Tokens

1. Go to [developer.ebay.com](https://developer.ebay.com) and sign in or create an account.
2. Create a new app and generate a **key set** (Sandbox first for testing).
3. Copy **App ID**, **Cert ID**, **Dev ID**, and generate a **User Token**.
4. Set the OAuth redirect (auth accepted URL):

```
https://your-domain.com/ebaymagentoconnect/index/fetchtoken
```

5. Copy the **RuName** from your eBay application settings.

See full walkthrough: [eBay Credentials](/guide/ebay-credentials.html)

### 3. Connect Magento to eBay

1. Log in to Magento Admin.
2. Go to **Stores → Configuration → Webkul → eBay Magento Connect**.
3. Set **Enable** to `Yes`.
4. Enter **App ID**, **Cert ID**, **Dev ID**, **User ID**, **Auth Token**, and **RuName**.
5. Select **Mode** — `Sandbox` for testing, `Production` for live.
6. Configure **Item Country**, **Item Location**, and **Postal Code**.
7. Click **Save Config**.
8. Complete OAuth authorization via the frontend token callback if prompted.

See all configuration groups: [Module Settings](/guide/module-settings.html)

### 4. Map Categories & Import First Products

1. Go to **eBay Magento Connect → Map Category**.
2. Click **Import eBay Categories** to pull the eBay category tree.
3. Map at least one Magento store category to an eBay leaf category.
4. Go to **eBay Magento Connect → Map Product**.
5. Select **Sync From eBay → Import Product From eBay**.
6. Set date range or SKUs, then click **Import Product From eBay**.
7. Run **eBay Product Profiler** to create catalog entries.
8. Run **eBay Product Image Profiler** to import images.

See detailed guides: [Map Category](/guide/map-category.html) · [Import Product](/guide/import-product-from-ebay.html)

---

## Validation: Check That It Worked

1. Open **eBay Magento Connect → Map Product** — imported products should appear in the grid with eBay Item IDs.
2. Open a synced product on the Magento storefront — name, price, and images should be visible.
3. Run a test **Export to eBay** for one SKU and confirm the listing appears in your eBay seller account.
4. Check **Export Queue Log** if using automatic or background export.

## What To Optimize Next

| Objective | Module Interface |
| --------- | ---------------- |
| Automate nightly product exports | **Automatic Product Export To eBay** config |
| Monitor failed export attempts | **Export Queue Log** grid |
| Export large catalogs in batches | **Bulk Export Tasks** (Feed API) |
| Sync orders in real time | **Real-Time Information Update** config |
| Apply price adjustments on sync | **Price Rules** under eBay Magento Connect |
| Use separate images for eBay listings | Product **eBay image** attributes on export |
