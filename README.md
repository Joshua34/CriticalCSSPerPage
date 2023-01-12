# CriticalCSSPerPage
>> Tested Successfully: Adobe Commerce 2.4

>> This repo allows the override of the single critical.css contents with unique contents from a corresponding static block.

This code is easily added to your existing theme.
No need for a custom module.

Adds template logic to check for any pageType data passed in from the page layout instructions and if present, renders a unique static block with corresponding ID
If no unique static block exists or no specific layout instruction is passed to template, then only standard criticalCss is rendered
Includes data-page attribute to display page handles in html, so specific layout instructions can be easily referenced and created

>> Example

Add this repo to your existing Adobe Commerce theme and browse to your homepage,
Inspect the page source code, and you will see:
   <style type="text/css" data-page="cms_index_index cms_page_view cms_index_index_id_home" data-type="criticalCss">body {background-color: blueviolet !important;}</style>

In order to provide additional criticalCss rules unique to this page, you would create a layout instruction referencing one of the page handles.
In this example it would be cms_index_index.xml:

<?xml version="1.0"?>
<page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
    <body>
        <referenceBlock name="critical_css_block">
            <arguments>
                <argument name="pageType" xsi:type="string">home</argument>
            </arguments>
        </referenceBlock>
    </body>
</page>

By passing in an arbitrary pageType string, we can then use the string to reference a unique static block, which we can create with the corresponding ID.
In this example, we would create a static block with the Identifier, home-criticalCss
The contents of this block should be raw CSS, as such, you may need to disable page builder in order to save raw CSS code.

Please leave comments or feedback or a PR if you have any improvements, thanks!
