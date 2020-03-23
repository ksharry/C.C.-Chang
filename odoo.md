<table>
    <tr>
        <td>ubuntu啟動指令</td>
    </tr>
</table>

#### 紀錄 
1. docker背景啟動postgresql路徑：/home/dsc/work/docker_community_13
    > docker-compose up -d
    
    > docker ps 
    
2. 啟動odoo環境
    > source odoo13/bin/activate

3. 路徑 要有odoo-bin:/home/dsc/odoo
    > python3 odoo-bin -w odoo -r odoo -c /home/dsc/odoo/config/odoo.conf

4. 登入網址：
   > http://0.0.0.0:8069/
