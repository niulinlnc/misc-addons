.. image:: https://img.shields.io/badge/license-LGPL--3-blue.png
   :target: https://www.gnu.org/licenses/lgpl
   :alt: License: LGPL-3

====================
 Backend debranding
====================

Removes references to odoo.com:

1. *(feature is not required in 12.0+ versions)*
2. Replaces "Odoo" in page title
3. Replaces "Odoo" in help message for empty list. 

   Some list views has word Odoo when search return empty result. E.g. search random string at menu ``[[ Settings ]] >> Users & Companies >> Companies`` that return empty result -- it has Odoo word

    Create and manage the companies that will be managed by **Odoo** from here. Shops or subsidiaries can be created and maintained from here.

4. *(feature is not required in 9.0+ versions)*
5. Deletes *Documentation*, *Support*, *My Odoo.com account*; adds *Developer mode*, *Developer mode (with assets)* links to the top right-hand User Menu.
6. *(feature is not required in 11.0+ versions)*
7. Replaces "Odoo" in Dialog Box

   E.g. try to remove Administrator via menu ``[[ Settings ]] >> Users & Companies >> Users``. It will show warning

    You can not remove the admin user as it is used internally for resources created by **Odoo** (updates, module installation, ...)

8. Replaces "Odoo" in strings marked for translation.

   This provides a big part of debranding. You can find examples at menu ``[[ Settings ]] >> General Settings``:

    Use external pads in **Odoo** Notes

    Extract and analyze **Odoo** data from Google Spreadsheet
   
   Full list of debranded phrases can be found at menu ``[[ Settings ]] >> Translations >> Application Terms`` (You may need to click ``Generate Missing Terms`` first).

9. Replaces default favicon to a custom one
10. **Hides Apps menu**. By default, only superuser can see Apps menu. You can change it via setting *Apps access* in a user form.
11. Disables server requests to odoo.com (publisher_warranty_url) - optional. Works only for non-enterprise versions of odoo, check `note <#enterprise-users-notice>`__ below.
12. *(feature is a part of p.5)*
13. Deletes Share block and branded parts of other blocks at ``[[ Settings ]] >> Dashboard``
14. *(feature is not required in 12.0+ versions)*
15. *(feature is not required in 12.0+ versions)*
16. Deletes "Odoo" in a request message for permission desktop notifications (yellow block at ``Discuss`` page). Replaces "Odoo" and icon in desktop notifications
17. [ENTERPRISE] Deletes odoo logo in application switcher
18. Hides Enterprise features in Settings
19. Replaces "Odoo" in all backend qweb templates

    This provides a big part of debranding. You can find examples in any tree view if you click ``[Import]`` button (e.g. at menu ``[[ Settings ]] >> Users & Companies >> Users``), then paste next code in browser javascript console:
    ``$('.oe_import_with_file').removeClass('d-none').siblings('.o_view_nocontent').hide().parent().find('.oe_import_noheaders.text-muted').show()``

     If the file contains the column names, **Odoo** can try auto-detecting the field corresponding to the column. This makes imports simpler especially when the file has many columns.


20. Replaces "odoo.com" in hints, examples, etc.

    For example, when you create new company it shows placeholder for field *Website*

     e.g. www.odoo.com

21. Renames "OdooBot" to "Bot". Use company's logo as bot avatar

    To receive a message from the Bot open menu ``[[ Discuss ]] >> CHANNELS >> #general`` and send ``/help`` to the chat.

22. [ENTERPRISE] Replaces icons for mobile devices with custom url
23. Replaces links to `documentation <https://www.odoo.com/documentation>`__ (e.g. "Help" in Import tool, "How-to" in paypal, etc.) to custom website
24. *(feature is not required in 12.0+ versions)*
25. *(feature is not required in 12.0+ versions)*

Configuration
=============

By default the module replaces "Odoo" to "Software". To configure
module openf ``[[ Settings ]] >> Technical >> Parameters >> System Parameters`` and modify

* ``web_debranding.new_title`` (put space in value if you don't need Brand in Title)
* ``web_debranding.new_name`` (your Brand)
* ``web_debranding.new_website`` (your website)
* ``web_debranding.new_documentation_website`` (website with documentation instead of official one)
* ``web_debranding.favicon_url``
* ``web_debranding.send_publisher_warranty_url`` - set 0 to disable server requests to odoo.com and 1 otherwise (useful for enterprise contractors). Works only for non-enterprise versions of odoo, check `note <#enterprise-users-notice>`__ below.
* ``web_debranding.icon_url`` - icon for mobile devices. recommended size :192x192
* ``web_debranding.apple_touch_icon_url`` - icon for IOS Safari. recommended size :152x152


Note. More user friendly way to configure the module is available in `Brand Kit <https://apps.odoo.com/apps/modules/11.0/theme_kit/>`__.

Further debranding
==================

* open addons/mail/data/mail_data.xml and edit Template "Notification Email" -- delete "using Odoo"
* open addons/website_livechat/data/website_livechat_data.xml and edit in "im_livechat_channel_data_website" record YourWebsiteWithOdoo.com string
* install **website_debranding** module if module "Website Builder" is installed in your system
* install **pos_debranding** module if module "POS" is installed in your system
* delete "Odoo.com Accounts" record at Settings\\Users & Companies\\OAuth Providers if module "OAuth2 Authentication" is installed in your system
* to debrand **/web/database/manager**:

  * edit addons/web/views/database_manager.html file:

    * delete or modify <title> tag
    * delete or modify favicon
    * delete or modify <img> tag with logo2.png
    * delete or modify warning <div class="alert alert-warning">Warning, your Odoo database ...</div>
    * delete or modify <small class="text-muted">To enhance your experience, some data may be sent to Odoo online services. See our <a href="https://www.odoo.com/privacy">Privacy Policy</a>.</small>
    * delete or modify <p class="form-text">In order to avoid conflicts between databases, Odoo needs ...</p>

Auto-debrand new databases
==========================
To automatically install this module for every new databases set **'auto_install': True** in __openerp__.py files of following modules:

* web_debranding
* ir_rule_protected
* access_restricted
* access_apps
* access_settings_menu
* mail (built-in)
* base_setup (built-in)
* bus (built-in)

Tested on Odoo 12.0 e774b2cb1c29fdd407aedc1f5c959d9725d2b514

Enterprise users notice
=======================

* `Terms of Odoo Enterprise Subscription Agreement <https://www.odoo.com/documentation/user/12.0/legal/terms/enterprise.html#customer-obligations>`_ don't allow to disable server requests to odoo.com. For this reason feature #11 doesn't work in Enterprise version.

Note
====

* You can also use our new extended `Brand Kit module <https://www.odoo.com/apps/modules/11.0/theme_kit>`_ to brand your odoo instance and create your theme in few clicks.

Need our service?
=================

Contact us by `email <mailto:apps@it-projects.info>`__ or fill out `request form <https://www.it-projects.info/page/website.contactus>`__:

* Email: apps@it-projects.info
* Form: https://www.it-projects.info/page/website.contactus
* Facebook: https://m.me/itprojectsllc
* Skype: skype@it-projects.info
