Instructions for setting up XAMPP and DVWA on Linux systems.

### Part 1: Install XAMPP

1. Go to [https://www.apachefriends.org/download.html](https://www.apachefriends.org/download.html) and download the linux installer for XAMPP. Make sure you download the version that uses `PHP 5.6`, otherwise DVWA will not work.
2. In your terminal, `cd` to the directory where you saved the XAMPP installer.
3. Run `chmod +x xampp-linux-x64-5.6.31-0-installer.run`. This tells Linux that you give it permission to run the installer.
    * You need to run `chmod +x` on whatever your installer is called.
    * You may need `sudo` for this.
4. Now run the installer: `sudo ./xampp-linux-x64-5.6.31-0-installer.run`.
    * You need `sudo` for this because it installs XAMPP in `/opt/lampp/`; regular users do not have read/write privileges for `/opt/`.

### Part 2: Install DVWA

#### Option 1: Git Clone

1. Clone DVWA from [https://github.com/ethicalhack3r/DVWA](https://github.com/ethicalhack3r/DVWA): `git clone https://github.com/ethicalhack3r/DVWA.git`
2. Rename the `DVWA-master/` directory to `dvwa/`: `mv DVWA-master/ dvwa/`
3. Move this directory to XAMPP's public folder: `sudo mv dvwa/ /opt/lampp/htdocs/`
4. In your terminal, `cd` to the directory you just placed `dvwa/` into: `cd /opt/lampp/htdocs/`
5. Change the permissions to your `dvwa/` directory so that XAMPP can use it: `sudo chmod 777 dvwa/ -R`
    * The `-R` flag tells `chmod` to apply the `777` permissions recursively.

#### Option 2: Zip File

1. Download DVWA from [https://github.com/ethicalhack3r/DVWA](https://github.com/ethicalhack3r/DVWA).
2. In your terminal, `cd` to the directory where you saved `DVWA-master.zip`.
3. Run `unzip DVWA-master.zip` to extract DVWA.
4. Rename the directory you just extracted to `dvwa/`: `mv DVWA-master/ dvwa/`
5. Move this directory to XAMPP's public folder: `sudo mv dvwa/ /opt/lampp/htdocs/`
6. Change the permissions to your `dvwa/` directory so that XAMPP can use it: `sudo chmod 777 dvwa/ -R`
    * The `-R` flag tells `chmod` to apply the `777` permissions recursively.

### Part 3: Configure DVWA

1. From the directory `/opt/lampp/htdocs/dvwa/`, rename the DVWA config file: `mv /config/config.inc.php.dist /config/config.inc.php`
    * You probably want to use `cp` instead of `mv`. That way you have a backup of `config.inc.php.dist`.
2. Using your favorite command line editor, open the `config.inc.php` file.
    * <b>nano:</b> `sudo nano /config/config.inc.php`
    * <b> vim:</b> `sudo vim /config/config.inc.php`
3. Find the line that looks like `$_DVWA[ 'db_password' ] = 'p@ssw0rd';` and change it to `$_DVWA[ 'db_password' ] = '';`

### Part 4: Configure MySQL

1. Go to the root directory of the XAMPP installation: `cd /opt/lampp/`
2. Start XAMPP: `sudo ./xampp start`

You might get an error about apache already running. If you do, run `sudo ./xampp stop` followed by `sudo service apache2 restart`. Now try `sudo ./xampp start` again.

3. In your browser, navigate to [http://127.0.0.1/phpmyadmin/](http://127.0.0.1/phpmyadmin/).
4. On the left-hand side of the page, click <b>New</b>.
5. In the field called <b>Database name</b>, type 'dvwa'.
6. You don't need to do anything with the <b>collation</b> dropdown. Click the <b>Create</b> button.
7. In your browser, navigate to [http://127.0.0.1/dvwa/setup.php](http://127.0.0.1/dvwa/setup.php).
8. If your page looks like [this](https://thehacktoday.com/wp-content/uploads/2017/07/Create-Pentest-Lab-9.png), then you did it! If not, you did something wrong and you will either have to start over or have fun debugging.
    * Don't worry about the `reCAPTCHA key: Missing` or `PHP function allow_url_include: Disabled` messages. They don't affect us.
9. Finally, navigate to [http://127.0.0.1/dvwa/login.php](http://127.0.0.1/dvwa/login.php) in your browser and login with the username <b>admin</b> and the password <b>password</b>.

### Part 5: IMPORTANT!

When you are not using DVWA, make sure you run `sudo ./xampp stop` from `/opt/lampp/` to shutdown the XAMPP server; if you don't, then you are leaving an intentionally vunerable web application open to the world. If you don't know why that's a bad thing, then you haven't been paying attention in class!


