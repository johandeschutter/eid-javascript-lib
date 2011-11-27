Library of JavaScript objects designed to retrieve data out of eID- and SIS cards using the applet from the eID middleware.

The interface and implementation (identity data) of EIDCard and SISCard are designed to be eID middleware independent.
The interface and implementation of EIDCardBuilder35 and SISCardBuilder35 are designed for eID middleware 3.5. 
The interface of CardReader is designed to be middleware independent.
The implementation of CardReader uses EIDCardBuilder35- and SISCardBuilder35 objects and so it is designed for eID middleware 3.5.

If a new EID middleware is released, only new EIDCardBuilder- and SISCardBuilder objects should be created and 
only small changes will need to be applied to the implementation of the CardReader.

The interface of CardReader, EIDCard and SISCard will not change.
Therefore code that uses the CardReader-, EIDCard- and SISCard-objects will not have to be changed if a new eID middleware is released.

The library is supposed to work on Windows in Internet Explorer 5.5 and higher, in Mozilla Firefox 2 and higher, and in Opera 9 and higher.
Other browsers and other platforms were not tested.

SIS cards can only be read when using a SIS card plugin. A SIS card plugin for the ACS ACR38U reader is available in the eID Quick Install.
More information about SIS card plugins in the eID V3 middleware can be found at: http://eid.belgium.be/nl/binaries/eid3_siscardplugins_tcm147-22479.pdf

@version 1.8 14/05/2011
@author Johan De Schutter (eidjavascriptlib AT gmail DOT com), http://code.google.com/p/eid-javascript-lib/


How to run the examples on your computer
----------------------------------------

1) Download the archive eidjavascriptlib.zip from http://code.google.com/p/eid-javascript-lib/   
   The archive contains the following subdirectories: examples, jsdoc and src.
   Unzip the archive in a directory, for example c:\eid-javascript-lib

2) Install eID software with the eID Quick install. Instructions can be found at
   http://eid.belgium.be/nl/Hoe_installeer_je_de_eID/Quick_Install/
   http://eid.belgium.be/fr/Comment_installer_l_eID/Quick_Install/

3) Download Belgium Identity Card Developer's Kit (eID SDK 3.5) from 
   http://eid.belgium.be/nl/Achtergrondinfo/De_eID_technisch/index.jsp
   http://eid.belgium.be/fr/Informations_legales_et_techniques/L_eID_d_un_point_de_vue_technique/index.jsp

    - Unzip the archive
    - Run the installer from the archive
    - Select the Common and JAVA feature to be installed.
    - Go to the installation directory of the eID SDK (probably C:\Documents and Settings\<user>\My Documents\Belgium Identity Card SDK)
    - Go to the subdirectory \beidlib\Java\bin of the installation directory.
    - Copy the following files to the examples subdirectory of the eid-javascript-lib:
        - Applet-Launcher License.rtf
        - applet-launcher.jar
        - beid35JavaWrapper-linux.jar
        - beid35JavaWrapper-mac.jar
        - beid35JavaWrapper-win.jar
        - beid35libJava.jar
        - BEID_Applet.jar

4) Go to the examples subdirectory and open beid.jnlp in notepad or any other text editor.
   The codebase directory should be changed to the examples subdirectory of the eid-javascript-lib:

   If your examples subdirectory is C:\eid-javascript-lib\examples\

   change 
   <jnlp codebase="http://127.0.0.1/" href="beid.jnlp"> 
   into 
   <jnlp codebase="file:///C:/eid-javascript-lib/examples/" href="beid.jnlp">

   This is also explained in readme.txt and copy_binaries.bat in the Samples\misc\Applet\Basic\java subdirectory of the eID SDK.

5) Open beid_java_plugin.jnlp in notepad or any other text editor.
   The codebase directory should be changed to the examples subdirectory of the eid-javascript-lib:

   If your examples subdirectory is C:\eid-javascript-lib\examples\

   change 
   <jnlp codebase="http://127.0.0.1/" href="beid_java_plugin.jnlp"> 
   into 
   <jnlp codebase="file:///C:/eid-javascript-lib/examples/" href="beid_java_plugin.jnlp">

6) Open the examples in a browser.

How to deploy the examples on a webserver
-----------------------------------------
1) I presume you have a webserver located at http://hostname.domainname.be

2) Create a directory (or webcontext) named examples on your webserver.
   Make sure the directory is accessible at http://hostname.domainname.be/examples (surf with a browser to this url)

3) Copy the following files to the examples directory
    - Applet-Launcher License.rtf (from eID SDK)
    - applet-launcher.jar (from eID SDK)
    - beid35JavaWrapper-linux.jar (from eID SDK)
    - beid35JavaWrapper-mac.jar (from eID SDK)
    - beid35JavaWrapper-win.jar (from eID SDK)
    - beid35libJava.jar (from eID SDK)
    - BEID_Applet.jar (from eID SDK)
    - beid.jnlp (from eid-javascript-lib)
    - beid_java_plugin.jnlp (from eid-javascript-lib)
    - example.html (from eid-javascript-lib)
    - if needed, other examples files from eid-javascript-lib

4) Create a subdirectory named src in directory examples.
    - Copy be_belgium_eid.js (from eid-javascript-lib) to the examples\src directory
    - If needed, copy base64.js (from http://hellerim.net/base64_src.php) to the examples\src directory
    - Make sure the directory is accessible at http://hostname.domainname.be/examples/src (surf with a browser to this url)
    - If you want to put be_belgium_eid.js and base64.js in the examples directory, you need to change the following in example.html
        change
        <script type="text/javascript" src="..\src\be_belgium_eid.js"></script>
        into
        <script type="text/javascript" src="be_belgium_eid.js"></script>

5) Go to the examples directory and open beid.jnlp in notepad or any other text editor.
   The codebase parameter should be changed to http://hostname.domainname.be/examples/
   More info about the codebase parameter: http://download.oracle.com/javase/6/docs/technotes/guides/jweb/applet/codebase_determination.html

   change 
   <jnlp codebase="http://127.0.0.1/" href="beid.jnlp"> 
   into 
   <jnlp codebase="http://hostname.domainname.be/examples/" href="beid.jnlp">

   Open beid_java_plugin.jnlp in notepad or any other text editor.
   The codebase parameter should also be changed to http://hostname.domainname.be/examples/

   change 
   <jnlp codebase="http://127.0.0.1/" href="beid_java_plugin.jnlp"> 
   into 
   <jnlp codebase="http://hostname.domainname.be/examples/" href="beid_java_plugin.jnlp">

6) Add jnlp to the configuration of your webserver
   Make sure that the webserver, for example Internet Information Services (IIS), does NOT block files with extension jnlp (or files with MIME type application/x-java-jnlp-file).
   The default configuration of some webservers does not allow files with extension jnlp. Therefore you need to add the extension jnlp to the default configuration.

   How to change configuration of Internet Information Services (IIS)
   - http://technet.microsoft.com/en-us/library/cc725608(WS.10).aspx
   - http://nirlevy.blogspot.com/2010/01/iis-jnlp-404-problem.html

   How can I add JNLP MIME-types to my ISP's Apache Web Server? http://lopica.sourceforge.net/faq.html#apachemime

   Web Start returns a Bad MIME Type error. What's wrong? http://lopica.sourceforge.net/faq.html#badmimetype

   Unofficial Java Web Start/JNLP FAQ http://lopica.sourceforge.net/faq.html

7) Test your configuration
   Enter http://hostname.domainname.be/examples/beid_java_plugin.jnlp or http://hostname.domainname.be/examples/beid.jnlp in the address bar (url bar) of a browser.
   Normally, a Java Web Start icon or Java Web Start popup is shown, or a popup with a question if you want to download this file is shown.
   If a "404 Not Found" is shown, something is wrong. Check your configuration of your webserver. http://nirlevy.blogspot.com/2010/01/iis-jnlp-404-problem.html

8) Open http://hostname.domainname.be/examples/example.html in a browser.

Remark
------
1) The Base64 encoding only works in Internet Explorer, if JRE 6 Update 10 (Java Runtime Environment 1.6.0_10) or higher is installed
   and if the Next-Generation Java Plug-in is enabled (this is the default setting) in the Java Control Panel.
   The code for base64.js can be downloaded at http://hellerim.net/base64_src.php
   More details about base64 encoding are explained in the examples example_picture.html and example_upload_picture.html

2) If you are using Internet Explorer 7 or 8 on Vista, it could be that the examples doesn't work.
   Normally if you open the examples in Internet Explorer, a warning "To help protect your security, Internet Explorer has restricted
   this webpage from running scripts or ActiveX controls that could access to your computer. Click here for options ..." should be displayed.
   If this warning is not displayed, Java applets in that webpage are blocked.

   The problem is caused by Protected Mode for IE7 and IE8 in Windows Vista.
   More info at: http://blogs.msdn.com/ie/archive/2007/04/04/protected-mode-for-ie7-in-windows-vista-is-it-on-or-off.aspx

   You can solve this problem using the following solution: 
        - Open the html-file.
        - Add a whitespace.
        - Delete the whitespace.
        - Save the html-file using a different filename.

3) A foreigner eID card and a kids eID contains the same data as an eID card for Belgian citizens.
   The only difference is the card number. A foreign eID card number starts with B. And a kids eID card number starts with 610.