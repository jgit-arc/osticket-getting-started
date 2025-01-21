<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Getting Started</h1>
osTicket is an open source ticketing system used to easily manage customer support tickets. While osTicket is easy to use overall, some setup required to get started. osTicket runs in the web browser. A web server and database must be installed and configured. This walkthrough will cover installation and setting up of the required dependencies. I am using a Windows virtual machine hosted on Microsoft Azure. It is a basic, pay-as-you-go VM named osticket-vm running Windows 10 Pro (2 vpus, 8 GB). This walkthrough will not cover Azure in-depth or setting up virtual machines. Because the purpose of this walkthrough is osTicket, this will work on any version of Windows 10; virtual machine or not.<br />

<h2>List of Prerequisites</h2>

- Windows 10 or greater
- (OPTIONAL) An Azure virtual machine
- osTicket
- HeidiSQL
- mySQl
- PHP 7 (or higher)
- PHP Manager for IIS
- Rewrite Module 2
- VC_Redist

<h2>Installation Steps</h2>



<p>
<img src="https://i.ibb.co/QdsBZgW/1.png" alt="Disk Sanitization Steps"/>
<img src="https://i.ibb.co/p3b1jcJ/2.png" alt="Disk Sanitization Steps"/>
<img src="https://i.ibb.co/QFpHwRf/3.png" alt="Disk Sanitization Steps"/>
</p>
<p>
Enable Internet Information Services (IIS) in Windows with CGI. This is the web server that osTicket will use. Click Start. Enter and click Turn Windows Features On or Off. Select the Internet Information Services checkbox. Expand the box and verify that Web Management Tools and World Wide Web Services are checked. Expand World Wide Web Services. Expand Application Development Features. Check CGI and click OK. This will install the CGI dependency that is required and may take a few minutes. Once complete, you can test the server by opening any web browser and going to 127.0.0.1. This should bring up the blue Internet Information Services page (shown above).
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Install PHP Manager for IIS. The specifics of what this does is out of the scope for this walkthrough. Just know, this is another required dependency because osTicket runs on PHP. Download it <a href="https://www.iis.net/downloads/community/2018/05/php-manager-150-for-iis-10">here</a>. It is a standard Windows installer. Follow the instructions until the installation is complete. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Install the Rewrite Module. To reiterate, knowing the specifics of what this (and the following dependencies) does is not required for the goal of getting osTicket up and running. Download it <a href="https://www.iis.net/downloads/microsoft/url-rewrite">here</a>. It is a standard Windows installer. Follow the instructions until the installation is complete. 
</p>
<br />


<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create a directory called PHP. The C drive ("C:\PHP") is recommended for compatibility sake. Download the PHP binaries <a href="https://windows.php.net/download/">here</a>. This walkthrough uses version 7 (using a later versions will likely be okay). Save the zipped folder somewhere easily accessible and unzip its contents to the recently created PHP folder.  
</p>
<br />


<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Install the VC_redist from <a href="https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170">here</a>. It is a standard Windows installer. Follow the instructions until the installation is complete.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Install MySQL from <a href="https://downloads.mysql.com/archives/community/?version=5.5.41">here</a>. This is the database that osTicket will use to store all of its data. This walkthrough uses version 5 (using a later version will likely be okay). It is a standard Windows installer. Follow the instructions until the installation is complete. When prompted, launch MySQL Instance Configuration Wizard. When prompted, select standard configuration and click Next. When asked for a password, enter "root" for simplicity sake (this would not be done in a production environment). Keep all other settings default, click Next and click Execute when prompted to finish.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click Start and enter Internet Information Services (IIS) Manager. Right click and run as administrator. The web server must be connected to PHP. Click PHP Manager. Click Register new PHP version. Browse to where you saved the PHP folder and select the php-cgi executable. Click OK. IIS must be restarted. Click Restart on the right-pane. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Install osTicket from <a href="https://osticket.com/download/">here</a>. Save the zipped folder somewhere easily accessible. Extract the osTicket folder. We need to replace an existing folder in Windows with the upload folder we just extracted from osTicket. Open a new file explorer and go to "C:\inetpub\wwwroot". Copy the Upload folder into the wwwroot folder. Rename the upload folder to osTicket. Important: the name must be exact! No spaces, no typos. Simply - osTicket. Restart IIS again.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
From IIS, expand Sites on the left-pane. Expand Default Web Site. Click osTicket. Click Browse*:80(http) on the right-pane. A new web tab with the osTicket installer will open. Under prerequisites, PHP and MySQL should be green checked. Below are other recommended extensions. Not all of these are required, so we'll only enable the ones that are needed. In IIS, under Default Web Site and osTicket, open PHP Manager. Under PHP Extension, click Enable or Disable an Extension. Find the following extensions:
  - php_imap.dll
  - php_intl.dll
  - php_opcache.dll

Right click each extension and select Enable. Refresh the web browser for the changes to take effect. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Open a new file explorer and go to "C:\inetpub\wwwroot" (if it's not already open). Open the osTicket folder. Open the Include folder. Find the file titled ost-sampleconfig.php. Rename it to ost-config.php. Verify the spelling and spacing is exactly ost-config.php. Permissions will be assigned to allow this file to make changes on the backend for osTicket. Right click ost-config.php. Select properties. Click the Security tab. Click Advanced. Click Disable Inheritance and select Remove All Inherited Permissions From this Object. Click Add. Click Select a Principle. Enter "everyone" (note - you would never do this in a production environment, this is merely for testing purposes), click Check Names, and click OK. Check Full Control and click OK. Click Apply and OK. Go back to osTicket tab in the browser and click Continue.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On the basic installation screen, you will enter the information you would like to use for your osTicket's configuration. To complete the database settings, we'll need to create a new database specifically for osTicket and enter those credentials into the form. Install HeidiSQL from <a href="https://www.heidisql.com/download.php">here</a>. It is a standard Windows installer. Follow the instructions until the installation is complete. When prompted, launch HeidiSQL. Clikc the green New button. Enter "root" as the user and password. Click Open. Right-click Unnamed in the left-pane, highlight Create New and click Database. Name the database osTicket. Important: the name must be exact! No spaces, no typos. Simply - osTicket.  Click OK. If you click on osticket under Unnamed, you'll see that the database is empty. This is where the data from osTicket will be stored. Return to the osTicket browser page. Enter osTicket as the MySQL Database. Enter root as the MySQL username. Enter root as the MySQL password. Click Install Now. Optional - If you return to Heidi and refresh the osticket instance, the database will now contain default tables from osTicket.
</p>
<br />

