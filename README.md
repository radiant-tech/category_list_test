Category List Test Plugin for Joomla 3.x
========================================

Here is the test procedure

NOTE: Use the latest version of Joomla 3.x or the github "master" for these tests.

Setup
-----
* Use one of the default templates such as protostar
* Create or find a category.
* Add a category description to that category (if it does not already have one).
* Set up "Category List" menu item for the category.
* Enable Show Title and Show Description for this menu item.
* Display the category list page on front end and make sure you can see the
  category description.  (If not, fix this first since plugin you are testing
  will not be invoked unless the category description is displayed.)


Install the test plugin
-----------------------
* Download and install the plugin zip file from this page: category_list_test.zip

   * Note: when you click on the zip file, github takes you to another screen,
     click on the [RAW] button to download the zip file.  Save it on you local
     computer and then use the "Upload and install option" to install the
     plugin

* In the plugin manager enable the 'Content - Category list test' plugin


The test - BEFORE Applying the patch to Joomla
----------------------------------------------
* Show the front page.  Notice that the plugin adds

    [CATEGORY DESCRIPTION?]

  to both the category title and description (since it cannot tell them
  apart).

  This illustrates the problem that the patch to Joomla 3.x is trying to
  address.

Patch Joomla 3.x
----------------

* Edit this file: <site>/layouts/joomla/content/category_default.php
* Around line 35, add '.title' to the context (last argument) so it reads
  like this:

      <?php echo JHtml::_('content.prepare', $displayData->get('category')->title, '', $extension.'.category.title'); ?>

Test the fix
------------

* Display the category list page again.  
  Now you should see:

    [CATEGORY TITLE] 

  appended to the category title, and:

    [CATEGORY DESCRIPTION?] 

  appended after the category description.

This indicates the plugin can now distinguish between the category title
and description and that the test was successful!

If the test does not work for you, please contact me (see below) so I can
figure out why and fix the test.

If the test works, please post the results on the github page:

   https://github.com/joomla/joomla-cms/pull/2842

Thanks!

 -Jonathan Cameron
  ( jmcameron@jmcameron.net )
