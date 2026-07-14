# How to run PHP and MariaDB in Linux Mint.
Without downloading any app (_probably_). Just terminal and apt install.
___
# Ingredients:
- Device with Linux Mint
- Browser
- Internet Connection
- Database Viewer (phpmyadmin, dbeaver, heidisql, etc)
- Terminal
___
# 1. INSTALLING
### 1. We need to install the PHP and MariaDB  *(Similar as MySQL)*
`sudo apt update && sudo apt install php-cli php-mysql mariadb-server -y`
<br>\- `-y` to say yes to download it btw.
### 2. Open terminal and run this code:
`sudo nano /etc/mysql/my.cnf`
<br>\- Wait until the text opened.
### 3. At the VERY bottom of the my.cnf, add these lines:
`[mysqld]
bind-address = 0.0.0.0`
<br>\- **Save and close it.** The purpose of editing the script is to allow LAN access.
#### 3.1 SINCE WE USE MARIADB, we need to execute these:
`sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf`
<br>\- **Once the text opened,** find and change `bind-address = 127.0.0.1` to `bind-address = 0.0.0.0`

### 4. Return to terminal to run this code:
`sudo systemctl restart mysql`

### 5. Create a user to access it
`sudo mysql
CREATE USER 'Username'@'%' IDENTIFIED BY 'MyPassword';
GRANT ALL PRIVILEGES ON *.* TO 'Username'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
EXIT;`
<br>\- We **need** this to login into the Database through **phpmyadmin** or **HeidiSQL**, etc.
<br>\- Replace **Username** and **MyPassword** as what you wish. `root` is not recommended.

# 2. DAILY DEV COMMANDS
### Starting PHP (Running a PHP file):
1. Enter your PHP project folder with **Files** and right click the empty space to and click "Open in terminal" **or access directly via Terminal**
<br>\*It is recommended that your folder has index.php so that it will shows up your page immediately when executed.
2. **Open terminal** and run this code.
<br>`php -S 0.0.0.0:8000`
<br>**Don't close the terminal** unless you want to stop the PHP service.

### Start Database, run this code in terminal:
`sudo systemctl start mysql`
<br>There's no output but if it is working, it will ask for next input.
### Stop Database, run this code in terminal:
`sudo systemctl stop mysql`
<br>There's no output but if it is working, it will ask for next input.
### Ger your device IP, run this code in terminal:
`hostname -I | awk '{print $1}'` or `hostname -I`
or
`ip a | grep "inet"` (select the second _inet_, **not** inet6) or `ip a` (at _inet_ in _wlo1_)

Have fun coding. Source command: Gemini and general forums.
This is a personal note, but feel free to use it.
