===========
Maintenance
===========

Maintenance problems and solution for them.



Introduction
============


In the log message sometime apear message like this::

    2009-09-14 15:45:44 INFO PlacelessTranslationService You have a stale entry for 'Products.ZWiki' in your ZMI Products section.You should consider removing it. 


The product name 'Products.ZWiki' can change depend of your configuration. 
The solution is:


Control_Panel/Products is the list of products that is or was known to the Zope instance.  
It is updated when you restart Zope.  It may contain stale entries like you encountered here. 
Or it may contain entries for products that are still available but not in the place that Zope expects this.  
This can happen for example when you copy a Data.fs from one computer to another; 
Zope may still expect to find a product somewhere in /home/serveruser which does not exist on the other machine.  
Delete all products then, restart Zope and this list should be fine again, without stale entries. 

