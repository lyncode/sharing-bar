What is?
==========
Sharing and Export Bar is an addon re-developed by Lyncode for the SARI service (RCAAP project) a National project (from Portugal) currently maintained by FCCN. It aims to make easy sharing DSpace items (on social networks) and export them (to bibliographic formats).

> **Is it tested?**
> Yes. Currently there are 25 DSpace respositories using it with positive feedback.

How it works?
==========
There are two major functionalities, (1) the sharing functionality and (2) the export functionality. 

*Sharing*: It looks at the configuration file (config/modules/sharingbar.cfg) and parse all defined social networks (each network has a specific url that must be triggered in order to share the content)
*Export*: It uses XOAI core and XSL transformers to export.

> **Works on XMLUI?**
> No. Only on JSPUI.

Which DSpace version?
==========

DSpace 3.1 (need support for another version? Please, contact [general@lyncode.com](mailto:general@lyncode.com))

Installation
==========

Download this package, and using the patch tool apply it to the DSpace 3.1 source.

    cd [dspace source directory]
    patch -p1 < [unzipped content]/install.diff

---

How to add a new Social Network?
==========
Open the config/modules/sharingbar.cfg file. Establish a new id (unique) for the new social network. For example, "facebook":

    facebook.url = http://www.facebook.com/sharer.php?s=100&p[url]=[$url]&p[title]=[$title]&p[summary]=[$description]

there are three possible variables that might be added to the url:

* [$url] - DSpace Item back url
* [$title] - DSpace item title
* [$summary] = Dspace item abstract

finally, you must add the (unique) id to the list of possible social networks

    list = facebook, twitter, ...

**NOTE**: To add the icon image, just add an image at the following path - [jspui-webapp]/image/sharing/facebook.png

How to add a new export format?
==========
For example, let's add the "endnote" provider.

Create a new XSL similar to config/crosswalks/export/bibtex.xsl to transform the XOAI input into the desired format and add it to config/crosswalks/export directory.
Open the config/modules/export.cfg and define a new export provider:

    endnote.xslt = config/crosswalks/export/endnote.xsl
    endnote.mimeType = application/x-Research-Info-Systems
    endnote.extension = ris

Add the (unique) id to the list of available export formats

    list = bibtex, endnote

**NOTE**: To add the icon image, just add an image at the following path - [jspui-webapp]/image/sharing/endnote.png 

- - - 
![Developed by Lyncode](http://www.lyncode.com/images/lyncode/DevelopedBy.png) in partnership with ![RCAAP Project](http://pesquisa.biblioteca.iscte.pt/_img/logos/logo_rcaap.png)
