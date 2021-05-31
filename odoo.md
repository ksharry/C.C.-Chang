#### 全域紀錄 
1. vm tool 安裝 用虛擬光碟下載到目錄後,使用sudo perl vmware-indatll.pl進行安裝

#### github使用方式(win10)
1. 參考https://progressbar.tw/posts/3
2. https://git-scm.com/downloads
3. 打開Git Bash
4. ssh-keygen -t rsa -C 'Your email address'
5. ssh-add ~/.ssh/id_rsa  or   ssh-agent bash
6. 到github的設定，新增SSH的金鑰。
7. 上傳程式碼，先前要先去新增repositories。
  > 
    echo "# googlesheets" >> README.md
    git init
    git add README.md
    git commit -m "first commit"
    git branch -M main
    git remote add origin git@github.com:ksharry/googlesheets.git
    git push -u origin main
7. 如果要隱藏，就增加.gitignore，如有檔案操作如下
  > 
    git rm --cached xxxx(檔名)
    git clean -fX
    重新push
    
#### github使用方式(ubuntu)
1. sudo apt-get install git
2. 產生金鑰ssh-keygen -t rsa -b 4096 -C "your_email@example.com" ;  確認指令:eval "$(ssh-agent -s)"
3. 新增金鑰ssh-add ~/.ssh/id_rsa
4. 複製金鑰，vi ~/.ssh/id_rsa.pub
5. 到github的設定，新增SSH的金鑰。
6. linux設定  git config --global user.name “ksharry”  ;  git config --global user.email w461059@hotmail.com
7. 連線到  ssh -T git@github.com   成功訊息:Hi github! You've successfully authenticated
8. 上傳程式碼，先前要先去新增repositories。
  > 
    git pull #獲取新版本
    git status #獲取需要上傳的檔案 
    git add . # .表示全新增， git add README.md 表示只新增說明檔案
    git commit -m "add new files" # a commit
    git push
    git remote add origin git@github.com:ksharry/odoo14-cookbook    #新增遠端數據庫
    git push -u origin master     #參數 -u 等同於 --set-upstream，設定 upstream 可以使分支開始追蹤指定的遠端分支      
    
    git branch newbranch      #新增分支
    git checkout newbranch    #切換工作分支
    git merge newbranch       #合併
    git branch -D newbranch   #刪除

<table>
    <tr>
        <td>元植課程</td>
    </tr>
</table>

#### 紀錄 
1. python3.7.9 使用管理著，自定選python37路徑。1.勾選第一個，最後DISABLE
2. postgresql  使用10以上版本。
3. ODOO GITHUB下載


#### 開發紀錄 (多注意點和底線)
1. bbb新增承租紀錄:
    + 增加py的one2many
    + 新增py,xml,menuitem,security,的程式
    + 新增manafest,init
2. bbb新增客戶:
    + 新增py繼承，menuitem，xml對應尋找位置
    + 新增manafest,init
    
    
    
    
<table>
    <tr>
        <td>odoo14安裝</td>
    </tr>
</table>

#### 紀錄 
1. 環境vmware 
2. 啟動指令 https://www.candidroot.com/blog/our-candidroot-blog-1/post/how-to-install-odoo-14-on-ubuntu-20-04-lts-67
  > 
    sudo su - odoo -s /bin/bash
    cd /odoo/odoo-server
    ./odoo-bin -c /etc/odoo-server.conf

  >
    wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
    sudo apt install -y -f ./google-chrome-stable_current_amd64.deb

<table>
    <tr>
        <td>ubuntu啟動指令</td>
    </tr>
</table>

#### 紀錄 
1. Postgresql使用 
  + systemctl status postgresql.service ,查看 PostgreSQL 服務狀態
  + sudo -i -u postgres   ,  pql  登入
  + https://www.itread01.com/content/1546698734.html

2. 列舉資料庫：\l
3. 選擇資料庫：\c 資料庫名
4. 檢視該某個庫中的所有表：\dt
5. 切換資料庫：\c interface
6. 檢視某個庫中的某個表結構：\d 表名
7. 檢視某個庫中某個表的記錄：select * from apps limit 1;
7. 顯示字符集：\encoding
8. 退出psgl：\q
  
#### 紀錄 
0. 工具安裝
    + sudo apt install vim
    + pgadmin4
       
       > sudo vim /etc/apt/sources.list.d/pgdg.list
       
       > deb http://apt.postgresql.org/pub/repos/apt/ bionic-pgdg main
       
       > sudo wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
       
       > sudo apt update
       
       > sudo apt install pgadmin4

    +copyq
     
      > sudo apt install software-properties-common
         sudo add-apt-repository ppa:hluk/copyq
         sudo apt update
         sudo apt install copyq
         
    + x11vnc
    
       >apt-get install x11vnc
        sudo x11vnc -storepasswd [your_password] /etc/x11vnc.pass
        x11vnc

1. docker 安裝https://docs.docker.com/install/linux/docker-ce/ubuntu/

2. postgresql安裝  
    > 進入docke postgresql   :  docker ps ; docker exec -it 49054d415576 bash   :   volum路徑:/var/lib/docker/vloume/xxxxxxx or odooxxxx
    
    > 遠端pgadmin 安裝後設定,odoo/postgresql/odoo/odoo  ip設定即可。
    
    > 勿用--調整使用docker-compose (docker run -d -e POSTGRES_USER=odoo -e POSTGRES_PASSWORD=odoo --name db postgres:10.0)

2.wkhtmltopdf安裝
    
    > wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.xenial_amd64.deb
    
    > sudo apt --fix-broken install,sudo dpkg -i libpng12-0_1.2.54-1ubuntu1_amd64.deb
    
    > sudo dpkg -i dpkg -i wkhtmltox_0.12.5-1.xenial_amd64.deb
    
3. odoo安裝
    >git clone https://github.com/odoo/odoo.git
    
    >sudo apt-get install python3-venv ; python3 -m venv odoo13
    
    

   > pip3 install wheel
   
   > sudo apt-get install python3 python-dev python3-dev \
     build-essential libssl-dev libffi-dev \
     libxml2-dev libxslt1-dev zlib1g-dev \
     python-pip
     
   > sudo apt-get install libsasl2-dev python-dev libldap2-dev libssl-dev
   
   > pip3 install -r requirements.txt
   
 4.設定odoo環境
    
    >odoo.conf
       [options]
       addons_path = /home/twtrubiks/work/odoo13/addons
       data_dir = /home/twtrubiks/Downloads/odoo-git/odoo-data
       db_host = localhost

5. 路徑 要有odoo-bin:/home/dsc/odoo
    > source odoo13/bin/activate 
    
    > cd odoo
    
    > docker-compose up -d
    
    > python3 odoo-bin -w odoo -r odoo -c /home/dsc/odoo/config/odoo.conf

6 登入網址：
   > http://0.0.0.0:8069/
   
7.database網址：
  >  http://0.0.0.0:8069/web/database/manager

8. 複製語法python odoo-bin scaffold aa_sale1 addons

9. 語法：卡8069 netstat -lp --inet  , kill -9 pid

10.ssh連線開放
  >  sudo apt-get install ssh
   
  >  sudo nano /etc/ssh/sshd_config  開放Port 22  , AllowUsers dsc
  
  >  sudo /etc/init.d/ssh  restart
  
  >  sudo gedit /etc/hosts.allow   ALL: 192.168.3.*
  
  >  ssh –X dsx@192.168.x.x
   
11. XSHELL 上傳:sudo apt-get install lrzsz 

12. 直接在linux安裝指令 :python3 odoo-bin -i demo_expense_tutorial_v1 -d odoo -c /home/dsc/odoo/config/odoo.conf

13. 

14. jupyter 64位元出現sqlite3問題，https://www.sqlite.org/download.html ，下載Precompiled Binaries for Windows對應的位元數放入DLLs檔案即可。

15. 永續成本，公司編輯視圖 
  > 
    <group string="Cost Accounting" groups="account.group_account_user"> 
     <field name="anglo_saxon_accounting"/> 
    </group>
    
16. odoo14調整連線pgadmin /etc/postgres/12/main 
  + 調整pg_hba.conf 0.0.0.0/0  # IPv4 local connections:   host    all             all             0.0.0.0/0            md5
  + 調整pg_hba.conf 0.0.0.0/0  # replication privilege.    host    replication     all             0.0.0.0/0            md5
  + 開放postgresql.conf    listen_addresses = '*'
  + 重啟  /etc/init.d/postgresql restart
  > 
    ps aux  | grep 'postgres *-D'
    service postgresql status
    port sudo ufw status verbose
    sudo -u postgres psql 
    ALTER USER postgres WITH PASSWORD 'postgres';
    sudo -i -u postgres

16. odoo14調整port
  + sudo ufw enable  啟用
  + sudo apt-get install ufw     安裝
  + sudo ufw default allow/deny   開啟
  + sudo ufw status numbered    查看狀態
  + sudo ufw status verbose     查看狀態
  + sudo ufw allow 80/tcp / sudo ufw allow 443/tcp


