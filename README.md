# TYPO3 :cookie: Extension: we_cookie_consent
Cookie Consent Panel (Optin) with DSGVO/GDPR compliant use of cookies. Preconfigured modules for Google Analytics, Facebook and other frequently used services. Arbitrary expandability with tracking scripts that generate cookies on your website. Support of Google Tag Manager and easy export of Google Tag Manager. Third-party cookies and scripts are only loaded when active consent is given. Website visitors can edit their privacy settings at any time. Automatic update of cookie information when new cookies/scripts are inserted with secure consent procedure. Cookies can be automatically added to the privacy policy via a plugin. Multilingual and full support for desktop, tablet and mobile. Four standard modes for displaying the content solution. Based on [Klaro!](https://github.com/kiprotect/klaro).

## Links
Demo: [https://consent.websedit.de/](https://consent.websedit.de/)\
Documentation: [https://consent.websedit.de/dokumentation](https://consent.websedit.de/dokumentation)\
TYPO3 Extension Repository: [https://extensions.typo3.org/extension/we_cookie_consent/](https://extensions.typo3.org/extension/we_cookie_consent/)\
Packagist: [https://packagist.org/packages/websedit/we-cookie-consent](https://packagist.org/packages/websedit/we-cookie-consent)\

## Note on v2.0.0
Due to the update of the klaro library to version 0.7.x there have been some changes. Klaro has revised the generation of the HTML DOM and some CSS classes. We have implemented a fallback function that makes an update from the old 1.3 to the new 2.0 as smooth as possible. Please note that we cannot guarantee that everything will look exactly the same as before, especially with existing customisations to the output in CSS. Therefore, please check the output after an update. 

## Support
If you need private or personal support, contact us via our contact form on [https://consent.websedit.de/](https://consent.websedit.de/).

## Setup Extension

Edit constants.typoscript to configure Extension

````typo3_typoscript
plugin {
    tx_wecookieconsent_pi1 {
        view {
            partialRootPath = EXT:prj_template/Resources/Private/Extensions/WeCookieConsent/Partials/
            templateRootPath = EXT:prj_template/Resources/Private/Extensions/WeCookieConsent/Templates/
        }
        persistence.storagePid = ###COOKIE-STORAGE-UID###
        settings {
            styleCss >
            klaro {
                privacyPolicy = ###PRIVACY-PAGE-UID###
                testing = 0
                poweredBy = konverto.eu
            }
        }
    }
}
````

- Create Cookie Consent folder
- Scan site with ex. https://www.cookieyes.com/cookie-scanner/ and add Services and cookies to folder
- If scripts are needed for special cookies, select "other" in Service and give unique name. 
Create new partial under ``Partials/Service`` with same name and add script in ``Header`` or ``Footer`` section:

````html
<f:section name="Header">
    <script type="text/javascript">
        ...
    </script>
</f:section>

<f:section name="Footer">
    <script type="text/javascript">
        ...
    </script>
</f:section>
````

### Custom language files

Under ``ext_localconf.php``:
````php
        // Override language for WeCookieConsent extension
        $GLOBALS['TYPO3_CONF_VARS']['SYS']['locallangXMLOverride']
        ['EXT:we_cookie_consent/Resources/Private/Language/locallang.xlf'][] =
            'EXT:prj_template/Resources/Private/Ext/WeCookieConsent/Language/locallang.xlf';
        $GLOBALS['TYPO3_CONF_VARS']['SYS']['locallangXMLOverride']['de']
        ['EXT:we_cookie_consent/Resources/Private/Language/de.locallang.xlf'][] =
            'EXT:prj_template/Resources/Private/Ext/WeCookieConsent/Language/de.locallang.xlf';
        $GLOBALS['TYPO3_CONF_VARS']['SYS']['locallangXMLOverride']['it']
        ['EXT:we_cookie_consent/Resources/Private/Language/it.locallang.xlf'][] =
            'EXT:prj_template/Resources/Private/Ext/WeCookieConsent/Language/it.locallang.xlf';
````

## TODO
- CSS refactoring + only need to modify variables to style cookiebanner
- Implementation of optional REGEX to cover multiple cookies
- Optional partials for scripts that are called before/after klaro is set up
