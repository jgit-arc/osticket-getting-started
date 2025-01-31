<p align="center">
<img src="https://i.imgur.com/0KdiDRX.png" />
</p>

<h1>osTicket - Getting Started</h1>
osTicket is an open-source ticketing system used to easily manage customer support tickets. While osTicket is generally user-friendly, some setup is required to get started. osTicket runs in a web browser, so a web server and database must be installed and configured. This walkthrough covers the installation and setup of the required dependencies.  

I am using a Windows virtual machine hosted on Microsoft Azure. The VM is named `osticket-vm` and runs Windows 10 Pro (2 vCPUs, 8 GB RAM). This guide does not delve into Azure specifics or virtual machine setup. However, these steps will work on any version of Windows 10, whether running on a VM or not.

---

<h2>Prerequisites</h2>

- Windows 10 or later
- (Optional) An Azure virtual machine
- osTicket
- HeidiSQL
- MySQL
- PHP 7 (or higher)
- PHP Manager for IIS
- Rewrite Module 2
- VC_Redist

---

<h2>Installation Steps</h2>

### 1. Enable Internet Information Services (IIS)
<p>
<img src="https://i.imgur.com/ieZVePk.png" />
<img src="https://i.imgur.com/mDo6q3u.png" />
<img src="https://i.imgur.com/cMx6b0p.png" />
</p>

1. Open **Start**, then search for **Turn Windows Features On or Off**.
2. Select the checkbox for **Internet Information Services (IIS)**.
3. Expand **Web Management Tools** and **World Wide Web Services**, then ensure these are checked:
   - Application Development Features > **CGI**
4. Click **OK** to install. This may take a few minutes.
5. Test the setup by opening a web browser and navigating to `127.0.0.1`. You should see the default blue IIS page.

---

### 2. Install PHP Manager for IIS
<p>
<img src="https://i.imgur.com/JcmlAEb.png" />
</p>

- Download PHP Manager for IIS from [this link](https://www.iis.net/downloads/community/2018/05/php-manager-150-for-iis-10).  
- Follow the installer instructions to complete the setup.

---

### 3. Install the Rewrite Module
- Download the Rewrite Module from [here](https://www.iis.net/downloads/microsoft/url-rewrite).  
- Follow the installation instructions.

---

### 4. Install PHP
1. Create a directory called `C:\PHP`.
2. Download PHP binaries from [this link](https://windows.php.net/download/). This guide uses PHP 7, though later versions may work.  
3. Extract the downloaded ZIP file to `C:\PHP`.

---

### 5. Install VC_Redist
- Download the Visual C++ Redistributable from [this link](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170).  
- Follow the installer instructions to complete the setup.

---

### 6. Install MySQL
<p>
<img src="https://i.imgur.com/AKPavfx.png" />
<img src="https://i.imgur.com/smERVgp.png" />
</p>

- Download MySQL from [this link](https://downloads.mysql.com/archives/community/?version=5.5.41).  
- Follow the installer instructions. During setup:
  - Launch the **MySQL Instance Configuration Wizard**.
  - Select **Standard Configuration** and click **Next**.
  - For simplicity, set the password to `root` (not recommended for production).
  - Finish the setup.

---

### 7. Configure PHP in IIS
1. Open **IIS Manager** (Run as Administrator).
2. Click **PHP Manager**.
3. Click **Register New PHP Version**, then browse to `C:\PHP` and select `php-cgi.exe`.
4. Restart IIS.

---

### 8. Install osTicket
<p>
<img src="https://i.imgur.com/cwRnabP.png" />
</p>

1. Download osTicket from [here](https://osticket.com/download/). Extract the ZIP file.  
2. Copy the `upload` folder to `C:\inetpub\wwwroot` and rename it to `osTicket`.  
3. Restart IIS.

---

### 9. Configure PHP Extensions
<p>
<img src="https://i.imgur.com/y32WygR.png" />
</p>

1. Open IIS and navigate to **Default Web Site > osTicket**.
2. In **PHP Manager**, enable the following extensions:
   - `php_imap.dll`
   - `php_intl.dll`
   - `php_opcache.dll`
3. Refresh the osTicket installer in your browser.

---

### 10. Configure Permissions
<p>
<img src="https://i.imgur.com/4PhysEq.png" />
</p>

1. Go to `C:\inetpub\wwwroot\osTicket\include`.
2. Rename `ost-sampleconfig.php` to `ost-config.php`.
3. Right-click `ost-config.php` > **Properties** > **Security** > **Advanced**.
4. Disable inheritance and grant **Full Control** to `Everyone` (testing only).

---

### 11. Set Up the Database
<p>
<img src="https://i.imgur.com/x7tIwFM.png" />
<img src="https://i.imgur.com/ECtnC7Q.png" />
</p>

1. Install HeidiSQL from [here](https://www.heidisql.com/download.php).  
2. Launch HeidiSQL and create a new session using:
   - Username: `root`
   - Password: `root`
3. Create a new database named `osTicket`.
4. Return to the osTicket installer and complete the setup using:
   - MySQL Database: `osTicket`
   - MySQL Username: `root`
   - MySQL Password: `root`
5. Click **Install Now**.

