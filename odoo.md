<table>
    <tr>
        <td>ubuntu啟動指令</td>
    </tr>
</table>

#### 紀錄 
0. 工具安裝
    + sudo apt install vim


1. docker 安裝https://docs.docker.com/install/linux/docker-ce/ubuntu/

2. postgresql安裝  
    > docker run -d -e POSTGRES_USER=odoo -e POSTGRES_PASSWORD=odoo --name db postgres:12.1

2.wkhtmltopdf安裝
    > wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.xenial_amd64.deb
    
    > sudo apt --fix-broken install,sudo dpkg -i libpng12-0_1.2.54-1ubuntu1_amd64.deb
    
    > sudo dpkg -i dpkg -i wkhtmltox_0.12.5-1.xenial_amd64.deb
    
3. odoo安裝
    >git clone https://github.com/odoo/odoo.git
    
    >sudo apt-get install python3-venv ; python3 -m venv odoo13
    
    >source odoo13/bin/activate

   > pip3 install wheel
   
   > sudo apt-get install python3 python-dev python3-dev \
     build-essential libssl-dev libffi-dev \
     libxml2-dev libxslt1-dev zlib1g-dev \
     python-pip
     
   > sudo apt-get install libsasl2-dev python-dev libldap2-dev libssl-dev
   
   > pip3 install -r requirements.txt
   
 4.設定odoo環境
    + 

0. 確認docker是否啟動
    > sudo docker run hello-world
    
1. docker背景啟動postgresql路徑：/home/dsc/work/docker_community_13
    > docker-compose up -d
    
    > docker ps 
    
2. 啟動odoo環境
    > source odoo13/bin/activate

3. 路徑 要有odoo-bin:/home/dsc/odoo
    > python3 odoo-bin -w odoo -r odoo -c /home/dsc/odoo/config/odoo.conf

4. 登入網址：
   > http://0.0.0.0:8069/
   
5.database網址：
  >  http://0.0.0.0:8069/web/database/manager


http://paste.ubuntu.com/p/3SvZyGzwcH/
