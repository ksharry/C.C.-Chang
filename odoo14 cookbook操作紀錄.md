<table>
    <tr>
        <td>odoo14 cookbook</td>
    </tr>
</table>

## 大綱
#### 因操作過程中有些修改自己的CODE，中間紀錄一下使用方式，本書資料來源:https://alanhou.org/odoo-14-creating-odoo-add-on-modules/

## 第一章 安裝Odoo開發環境
  1. 安裝主要的依賴：
  
    sudo apt-get update 
    sudo apt install git python3-pip build-essential wget python3-dev python3-venv python3-wheel libxslt-dev libzip-dev libldap2-dev libsasl2-dev python3-setuptools -y 
    
  2. 下載並安装wkhtmltopdf：
  
    wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.bionic_amd64.deb
    sudo dpkg -i wkhtmltox_0.12.5-1.bionic_amd64.deb
    
  3. 如果以上命令出現了錯誤，請使用以下命令可強制安裝依賴：
  
    sudo apt-get install -f
    
  4. 安裝PostgreSQL資料庫
  
    sudo apt install postgresql -y
    
  5. 配置PostgreSQL
  
    sudo -u postgres createuser --superuser $(whoami)
    
  6. 配置git（以下內容須自行修改）：
  
    git config --global user.name "Your Name"
    git config --global user.email youremail@example.com
    
  7. Clone Odoo 基礎程式碼：
  
    mkdir ~/odoo-dev
    cd ~/odoo-dev
    git clone -b 14.0 --single-branch --depth 1 https://github.com/odoo/odoo.git
    
  8. 新建odoo-14.0虛擬環境並啟用：
  
    python3 -m venv ~/venv-odoo-14.0
    source ~/venv-odoo-14.0/bin/activate
    
  9. 在venv中安装Odoo的Python依赖：
  
    cd ~/odoo-dev/odoo/
    pip3 install -r requirements.txt
    
  10. 新建並啟動第一個ODOO：
    
    createdb odoo-test
    python3 odoo-bin -d odoo-test -i base --addons-path=addons --db-filter=odoo-test$
    
  11. 在http://localhost:8069 ，使用帳密admin/admin登陸，如需RTL（文字右向左）的支持，请使用如下命令安装node 和 rtlcss ：
  
    sudo apt-get install nodejs npm -y
    sudo npm install -g rtlcss
    
  12. 建立新的資料庫指令
  
    createdb -T odoo-test odoo-test2
    cd ~/.local/share/Odoo/filestore # 如果你修改了data_dir请调整此处
    cp -r odoo-test odoo-test2
    cd -
    
  13. 建立新的資料庫指令
  
    dropdb dbname
    rm -rf ~/.local/share/Odoo/filestore/dbname

  14. 建立備份
  
    pg_dump -Fc -fodoo-test2.dump odoo-test2
    tar cjf odoo-test2.tgz odoo-test2.dump ~/.local/share/Odoo/filestore/dbname
  
   15. 還原備份
  
    tar xf odoo-test2.tgz
    pg_restore -C -d odoo-test2 odoo-test2.dump
    
   16. 配置服務
  
    ./odoo-bin --save --config myodoo.cfg --stop-after-init
    ./odoo-bin --help | less    可查詢指令
    ./odoo-bin -c myodoo.cfg    開始指令
    
## 第二章 管理Odoo服務端實例
   1. 配置插件位置  addons_path = ~/odoo-dev/odoo/addons,~/odoo-dev/local-addons
   2. save選項保存路徑到配置文件中
   
    mkdir -p ~/odoo-dev/local-addons/dummy
    touch ~/odoo-dev/local-addons/dummy/__init__.py
    echo '{"name": "dummy", "installable": False}' > ~/odoo-dev/local-addons/dummy/__manifest__.py
    odoo/odoo-bin -d mydatabase --addons-path="odoo/odoo/addons,odoo/addons,~/odoo-dev/local-addons" --save -c ~/odoo-dev/my-instance.cfg --stop-after-init

   3. 標準化目錄布局
     + 每個環境創立一個目錄：
     
       mkdir ~/odoo-dev/projectname
       cd ~/odoo-dev/projectname

   b. 在env/的子目錄中創建一個Python虛擬環境對象：
    
    python3 -m venv env

   c. 創建一些子目錄，如下：
   
    mkdir src local bin filestore logs
    
    這些子目錄的功能如下：
    src/：包含Odoo本身的一個拷貝，以及一些第三方插件項目（我們在下一步中添加了Odoo源碼）
    local/：用於保存你針對具體實例的插件
    bin/：包含各類幫助可執行shell腳本
    filestore/：用於文件存儲
    logs/（可選）：用於存儲服務日誌文件
    
   d. 克隆Odoo並安裝所需依賴包：
   
    git clone -b 14.0 --single-branch --depth 1 https://github.com/odoo/odoo.git src/odoo
    env/bin/pip3 install -r src/odoo/requirements.txt

   e. 以bin/odoo保存如下shell腳本：
   
    #!/bin/sh
    ROOT=$(dirname $0)/..
    PYTHON=$ROOT/env/bin/python3
    ODOO=$ROOT/src/odoo/odoo-bin
    $PYTHON $ODOO -c $ROOT/projectname.cfg "$@"
    exit $?

   f. 讓該腳本可執行：
   
    chmod +x bin/odoo

   g. 創建一個空的本地模塊dummy：
   
    mkdir -p local/dummy
    touch local/dummy/__init__.py
    echo '{"name": "dummy", "installable": False}' > local/dummy/__manifest__.py

   h. 為你的實例生成配置文件：
   
    bin/odoo --stop-after-init --save --addons-path ,/home/wkc/odoo-dev/projectname/src/,/home/wkc/odoo-dev/projectname/local --data-dir /home/wkc/.local/share/Odoo

   i 添加一個.gitignore文件，用於告訴GitHub排除這些給定目錄，這樣Git在提交代碼時就會忽略掉這些目錄，例如 filestore/, env/, logs/和src/：
   
    # dotfiles, with exceptions:
    .*
    !.gitignore
    # python compiled files
    *.py[co]
    # emacs backup files
    *~
    # not tracked subdirectories
    /env/
    /src/
    /filestore/
    /logs/

   j. 為這個實例創建一個Git倉庫並將已添加的文件添加到Git中：
   
    git init
    git add .
    git commit -m "initial version of projectname"

   4. 手動激活虛擬環境：

    source env/bin/activate
    cd src/odoo
    ./odoo-bin --addons-path=addons,../../local -d test-14 -i account,sale,purchase --log-level=debug

   5. 安裝插件：
   
    cd ~/odoo-dev/my-odoo/src
    git clone --branch 14.0 https://github.com/OCA/partner-contact.git src/partner-contact
    
    projectname.cfg中的addons_path一行應該是這樣的：
    addons_path = /home/wkc/odoo-dev/projectname/src/odoo/odoo/addons,/home/wkc/odoo-dev/projectname/src/odoo/addons,/home/wkc/odoo-dev/projectname/src/,/home/wkc/odoo-dev/projectname/local

## 第一章 創建ODOO的addons
  1. 操作方式
