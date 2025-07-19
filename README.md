# WordPress Remove Version Query Strings

This code snippet helps you **remove version query strings (like `?ver=X.X.X`) from your WordPress script and stylesheet URLs**. By default, WordPress appends a version number to CSS and JavaScript files. While this is useful for cache busting (ensuring users get the latest file versions), some developers prefer to remove these strings for aesthetic reasons, specific caching strategies, or to slightly obscure the WordPress version (though this is a minor security measure).

## Why remove version query strings?

* **Cleaner URLs:** Makes your script and style URLs look cleaner and simpler.
* **Alternative Caching Strategies:** If you use other methods for cache invalidation (e.g., file renaming, CDN settings), these query strings might be redundant.
* **Minor Obscurity:** Slightly reduces information leakage about the exact WordPress or plugin/theme versions in use, though this is a very minor security benefit and not a substitute for proper security practices.

## Installation

There are two primary methods to implement this code:

### Method 1: As a Standalone Plugin (Recommended)

Creating a small, dedicated plugin is the most robust way to add this customization. It ensures your modification remains active regardless of theme changes.

1.  Create a new folder named `wp-no-ver-query` inside your WordPress site's `wp-content/plugins/` directory.
2.  Inside this new folder, create a file named `wp-no-ver-query.php`.
3.  Copy and paste the following code into `wp-no-ver-query.php`:

    ```php
    <?php
    /**
     * Plugin Name: WordPress Remove Version Query Strings
     * Description: Removes version query strings from WordPress script and stylesheet URLs.
     * Version: 1.0
     * Author: Your Name (Optional)
     * License: MIT
     */

    // Remove Version Query Strings from Scripts/Styles
    function _remove_script_version( $src ){
        $parts = explode( '?ver', $src );
        return $parts[0];
    }
    add_filter( 'script_loader_src', '_remove_script_version', 15, 1 );
    add_filter( 'style_loader_src', '_remove_script_version', 15, 1 );
    ?>
    ```

4.  Go to your WordPress admin dashboard, navigate to **"Plugins"**, and **activate** the "WordPress Remove Version Query Strings" plugin.

### Method 2: Adding to your Theme's functions.php File

You can add this code directly to your active theme's `functions.php` file. **Before doing so, it's highly recommended to back up your `functions.php` file.**

1.  Navigate to `wp-content/themes/YourThemeName/` (replace `YourThemeName` with the actual name of your active theme).
2.  Open the `functions.php` file.
3.  Add the following code to the end of the file (before the closing `?>` tag, if one exists):

    ```php
    // Remove Version Query Strings from Scripts/Styles
    function _remove_script_version( $src ){
        $parts = explode( '?ver', $src );
        return $parts[0];
    }
    add_filter( 'script_loader_src', '_remove_script_version', 15, 1 );
    add_filter( 'style_loader_src', '_remove_script_version', 15, 1 );
    ```

## Important Considerations

* **Caching:** Removing version query strings might impact how browsers and caching plugins handle your static files. Ensure your caching strategy is still effective after implementing this. Without version strings, changes to CSS/JS files might not immediately reflect for users with cached versions.
* **Troubleshooting:** If you experience issues with styles or scripts not loading correctly after implementing this, it might be related to caching or how your server/CDN handles files without query strings.

## Contributing

Contributions are welcome! If you have suggestions or improvements for this code, feel free to open a "Pull Request" or report an "Issue."

## License

This project is licensed under the MIT License. For more details, see the `LICENSE` file.

# حذف رشته‌های پرس‌وجوی نسخه از وردپرس

این قطعه کد به شما کمک می‌کند تا **رشته‌های پرس‌وجوی نسخه (مانند `?ver=X.X.X`) را از آدرس‌های اسکریپت‌ها و برگه‌های استایل (CSS) وردپرس حذف کنید**. به طور پیش‌فرض، وردپرس یک شماره نسخه به فایل‌های CSS و جاوااسکریپت اضافه می‌کند. اگرچه این کار برای باطل کردن کش (cache busting) مفید است (اطمینان از دریافت آخرین نسخه‌های فایل توسط کاربران)، برخی از توسعه‌دهندگان ترجیح می‌دهند این رشته‌ها را به دلایل زیبایی‌شناختی، استراتژی‌های کش خاص، یا برای پنهان کردن جزئی نسخه وردپرس حذف کنند (اگرچه این یک اقدام امنیتی جزئی است).

## چرا رشته‌های پرس‌وجوی نسخه را حذف کنیم؟

* **آدرس‌های تمیزتر:** آدرس‌های اسکریپت و استایل شما را تمیزتر و ساده‌تر نشان می‌دهد.
* **استراتژی‌های جایگزین کش:** اگر از روش‌های دیگری برای باطل کردن کش (مانند تغییر نام فایل، تنظیمات CDN) استفاده می‌کنید، این رشته‌های پرس‌وجو ممکن است اضافی باشند.
* **پنهان‌کاری جزئی:** اطلاعات افشاشده در مورد نسخه‌های دقیق وردپرس یا افزونه/قالب‌های در حال استفاده را کمی کاهش می‌دهد، اگرچه این یک مزیت امنیتی بسیار جزئی است و جایگزینی برای رویه‌های امنیتی صحیح نیست.

## نصب

برای پیاده‌سازی این کد دو روش اصلی وجود دارد:

### روش ۱: به عنوان یک افزونه مستقل (توصیه شده)

ایجاد یک افزونه کوچک و اختصاصی، قوی‌ترین راه برای افزودن این سفارشی‌سازی است. این تضمین می‌کند که تغییر شما صرف‌نظر از تغییر قالب، فعال باقی بماند.

1.  یک پوشه جدید با نام `wp-no-ver-query` در مسیر `wp-content/plugins/` سایت وردپرسی خود ایجاد کنید.
2.  در داخل این پوشه جدید، یک فایل با نام `wp-no-ver-query.php` ایجاد کنید.
3.  کد زیر را در `wp-no-ver-query.php` کپی و جایگذاری کنید:

    ```php
    <?php
    /**
     * Plugin Name: WordPress Remove Version Query Strings
     * Description: Removes version query strings from WordPress script and stylesheet URLs.
     * Version: 1.0
     * Author: Your Name (Optional)
     * License: MIT
     */

    // Remove Version Query Strings from Scripts/Styles
    function _remove_script_version( $src ){
        $parts = explode( '?ver', $src );
        return $parts[0];
    }
    add_filter( 'script_loader_src', '_remove_script_version', 15, 1 );
    add_filter( 'style_loader_src', '_remove_script_version', 15, 1 );
    ?>
    ```

4.  وارد پنل مدیریت وردپرس خود شوید، به بخش **"افزونه‌ها"** بروید و افزونه **"WordPress Remove Version Query Strings"** را **فعال کنید**.

### روش ۲: اضافه کردن به فایل functions.php قالب شما

می‌توانید این کد را مستقیماً به فایل `functions.php` قالب فعال خود اضافه کنید. **پیشنهاد اکید می‌شود قبل از انجام این کار، از فایل `functions.php` خود یک پشتیبان (backup) تهیه کنید.**

1.  به مسیر `wp-content/themes/YourThemeName/` بروید (به جای `YourThemeName` نام واقعی قالب فعال خود را قرار دهید).
2.  فایل `functions.php` را باز کنید.
3.  کد زیر را به انتهای فایل (قبل از تگ بستن `?>`، در صورت وجود) اضافه کنید:

    ```php
    // Remove Version Query Strings from Scripts/Styles
    function _remove_script_version( $src ){
        $parts = explode( '?ver', $src );
        return $parts[0];
    }
    add_filter( 'script_loader_src', '_remove_script_version', 15, 1 );
    add_filter( 'style_loader_src', '_remove_script_version', 15, 1 );
    ```

## ملاحظات مهم

* **کش (Caching):** حذف رشته‌های پرس‌وجوی نسخه ممکن است بر نحوه مدیریت فایل‌های استاتیک شما توسط مرورگرها و افزونه‌های کش تأثیر بگذارد. اطمینان حاصل کنید که استراتژی کش شما پس از پیاده‌سازی این کد همچنان موثر است. بدون رشته‌های نسخه، تغییرات در فایل‌های CSS/JS ممکن است بلافاصله برای کاربرانی که نسخه‌های کش‌شده دارند، منعکس نشود.
* **عیب‌یابی:** اگر پس از پیاده‌سازی این کد، با مشکلاتی در بارگذاری صحیح استایل‌ها یا اسکریپت‌ها مواجه شدید، ممکن است مربوط به کش یا نحوه مدیریت فایل‌ها بدون رشته‌های پرس‌وجو توسط سرور/CDN شما باشد.

## مشارکت (Contributing)

مشارکت شما خوشایند است! اگر پیشنهاد یا بهبودهایی برای این کد دارید، می‌توانید یک "Pull Request" ایجاد کنید یا "Issue" جدیدی را گزارش دهید.

## مجوز (License)

این پروژه تحت مجوز MIT منتشر شده است. برای جزئیات بیشتر به فایل `LICENSE` مراجعه کنید.
