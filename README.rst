Introduction
============

The default Plone theme use a grid css framework named deco. Mixin two grid
system can be a bad idea, but we love 960 css.

This example add-on show how to integrate and use 960 css grid framework in
Plone to make a diazo theme. It fixes many issues details here and show you
the power and common tricks to use.

Issues
======

One, two or three columns ?
---------------------------

The default plone theme use a controller to know if there are portlets to 
display on left and on right columns. You want to react on this in your theme.

Solution: We are loading values as theme parameters: ::

    [theme:parameters]
    have_left_portlets = python:context.restrictedTraverse('@@plone').have_portlets('plone.leftcolumn',context)
    have_right_portlets = python:context.restrictedTraverse('@@plone').have_portlets('plone.rightcolumn',context)
    have_both_portlets = python:context.restrictedTraverse('@@plone').have_portlets('plone.leftcolumn',context) and context.restrictedTraverse('@@plone').have_portlets('plone.rightcolumn',context)

TinyMCE overlays has scroll bars ?
----------------------------------

This issues comes from the way we are loading css insinde TinyMCE. Because
every overlays are simple iframe they have a body and 960css fix the body width
to 960px.

Solution: We are making a small fix on 960 to remove the fixed width of the
body outside of plone page: ::

    -body {
    +body.plonesite {
        min-width: 960px;
     }

And make sure every theme templates are using 'plonesite' css class.

Overlays are broken
-------------------

Be sure your theme has a #content. Plone's overlays are query serverside and
just the #content is displayed, so no #content means a javascript error;

Tricks
======

You will find many css tricks with google by using 960 in your search terms.

How to use this add-on ?
------------------------

Just copy paste the theme folder in your new plonetheme add-on, and update
your profile / zcml.


CSS fixes in this add-on
------------------------

In this add-on there is few fixes (yes the default Plone theme rocks)

* fix z-index of some drop down menu with the livesearch
* fix globalnav margin because it overrides the 960 grid's margin

How do I use 960 Grid System with borders?
------------------------------------------

source: http://doctype.com/use-960-grid-system-borders

solution: ::

    #mybox{
      border:1px solid #333;
      margin-left:9px; /* border + margin = 10px */
      margin-right:9px; /* border + margin = 10px */
    }

