<table>
    <tr>
        <td>odoo14 cookbook</td>
    </tr>
</table>

## 大綱
#### 本書資料來源:https://alanhou.org/odoo-14-creating-odoo-add-on-modules/，因操作過程中有點不連貫，中間紀錄一下使用方式。

#### 第一章 安裝Odoo開發環境
  1. 運行如下命令来安装主要依赖：
    '
     sudo apt-get update
    
     sudo apt install git python3-pip build-essential wget python3-dev python3-venv python3-wheel libxslt-dev libzip-dev libldap2-dev libsasl2-dev python3-setuptools -y
    
     sudo apt-get update
    
     sudo apt install git python3-pip build-essential wget python3-dev python3-venv python3-wheel libxslt-dev libzip-dev libldap2-dev libsasl2-dev python3-setuptools -y
    
    '
    
  2. 下載並安装wkhtmltopdf：
  
    + wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.bionic_amd64.deb
    
    + sudo dpkg -i wkhtmltox_0.12.5-1.bionic_amd64.deb
    
    + wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.bionic_amd64.deb
    
    + sudo dpkg -i wkhtmltox_0.12.5-1.bionic_amd64.deb
    
  3. 如果以上命令出現了錯誤，請使用以下命令可強制安裝依賴：
  
    + sudo apt-get install -f
    
  4. 安裝PostgreSQL資料庫
  
    + sudo apt install postgresql -y
    
    + sudo apt install postgresql -y
    
  5. 配置PostgreSQL
  
    + sudo -u postgres createuser --superuser $(whoami)
    
    + sudo -u postgres createuser --superuser $(whoami)
    
  6. 配置git（以下內容須自行修改）：
  
    + git config --global user.name "Your Name"
    
    + git config --global user.email youremail@example.com
    
    + git config --global user.name "Your Name"
    
    + git config --global user.email youremail@example.com
    
  7. Clone Odoo 基礎程式碼：
    + mkdir ~/odoo-dev
    + cd ~/odoo-dev
    + git clone -b 14.0 --single-branch --depth 1 https://github.com/odoo/odoo.git
  8. 新建odoo-14.0虛擬環境並啟用：
    + python3 -m venv ~/venv-odoo-14.0
    + source ~/venv-odoo-14.0/bin/activate
    +  python3 -m venv ~/venv-odoo-14.0
    + source ~/venv-odoo-14.0/bin/activate
  9. 在venv中安装Odoo的Python依赖：
    + cd ~/odoo-dev/odoo/
    + pip3 install -r requirements.txt
    + cd ~/odoo-dev/odoo/
    + pip3 install -r requirements.txt
  10. 新建並啟動第一個ODOO：
    + createdb odoo-test
    + python3 odoo-bin -d odoo-test -i base --addons-path=addons --db-filter=odoo-test$
    + createdb odoo-test
    + python3 odoo-bin -d odoo-test -i base --addons-path=addons --db-filter=odoo-test$
  11. 在http://localhost:8069 ，使用帳密admin/admin登陸，如需RTL（文字右向左）的支持，请使用如下命令安装node 和 rtlcss ：
    + sudo apt-get install nodejs npm -y
    + sudo npm install -g rtlcss
    + sudo apt-get install nodejs npm -y
    + sudo npm install -g rtlcss
