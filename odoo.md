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
   
  >  sudo nano /etc/ssh/sshd_config  開放Port 22  , AllowUsers odoo
  
  >  sudo /etc/init.d/ssh  restart
  
  >  sudo gedit /etc/hosts.allow   ALL: 192.168.x.x
  
  >  ssh –X dsx@192.168.x.x
   
11. XSHELL 上傳:sudo apt-get install lrzsz 

12. 直接在linux安裝指令 :python3 odoo-bin -i demo_expense_tutorial_v1 -d odoo -c /home/dsc/odoo/config/odoo.conf

13. 查看開放port sudo ufw status verbose  , 新增port:sudo ufw allow 22/tcp

14. jupyter 64位元出現sqlite3問題，https://www.sqlite.org/download.html ，下載Precompiled Binaries for Windows對應的位元數放入DLLs檔案即可。

15. 永續成本，公司編輯視圖 
  > <group string="Cost Accounting" groups="account.group_account_user"> 
     <field name="anglo_saxon_accounting"/> 
    </group>
