=======================
Maintenance Plone 3.3.x
=======================

Maintenance problems and solution for them.



PlacelessTranslationService You have a stale entry for
======================================================


In the log message appears like this::

    2009-09-14 15:45:44 INFO PlacelessTranslationService You have a stale entry for 'Products.ZWiki' in your ZMI Products section.You should consider removing it. 


The product name 'Products.ZWiki' can change depend of your configuration. 
The solution is:


Control_Panel/Products is the list of products that is or was known to the Zope instance.  
It is updated when you restart Zope.  It may contain stale entries like you encountered here. 
Or it may contain entries for products that are still available but not in the place that Zope expects this.  
This can happen for example when you copy a Data.fs from one computer to another; 
Zope may still expect to find a product somewhere in /home/serveruser which does not exist on the other machine.  
Delete all products then, restart Zope and this list should be fine again, without stale entries. 

The list in portal_quickinstaller is the list of products that are
currently installed or that are available for installation.  If a
product is installed but is not known to Zope anymore it is still
listed here.  This can happen when you install a product in Plone and
remove it from the file system without properly uninstalling it first
in Plone.  This may have happened with Poi.

The version numbers that portal_quickinstaller shows as 'Product
version' are (at least mostly) taken from Control_Panel/Products.  I
think portal_quickinstaller asks the control panel for the version
number of the product.  The control panel takes the file system path
that it has remembered of the product and looks for a version.txt file
there.

So:

- If you move a Data.fs around, it can help to remove all products
  from the Control_Panel/Products and restart Zope to update the list.

- If you no longer want to use a product that is already installed in
  Plone, first uninstall it and only then remove it from the file
  system. 



Cannot register transform lynx_dump error log entries in Plone
==============================================================


In the instance.log is (mgirated from 3.3) gets messages like::

    2012-07-09 17:40:38 ERROR PortalTransforms Cannot register transform lynx_dump, using BrokenTransform: Error Unable to find binary "lynx" in /Users/moo/tools/bin:/Users/moo/.zsh/bin:/opt/local/libexec/gnubin:/opt/local/bin:/opt/local/sbin:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin:/usr/X11/bin
    

It is not a real problem, unless you use the lynx_dump transform (nothing in stock Plone uses it, and other transforms provide text/html to text/plain too).

The solutin to deal with it:

1. Remove the lynx_dump transform. Go to the ZMI, find the portal_transforms tool, check the box by the lynx_dump entry, and hit the [Delete] button at the bottom of the form. This is harmless if you don't use the transform.    
2. In the portal_transforms click on the tab Reload transforms 



    
ERROR Zope.ZCatalog reindexIndex could not resolve an object from the uid
=========================================================================

When trying to insert a new page I get an error complaining about some lost uid::

    ERROR Zope.ZCatalog reindexIndex could not resolve an object from the uid '/path/to/the/object'
    

Proposed solution:

When you want to recover from the error (without understanding where the problem comes from), 
you could use the "Update catalog" from the "Advanced" tab. 
It will uncatalog any object that cannot be resolved.


