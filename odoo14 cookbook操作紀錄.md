<table>
    <tr>
        <td>odoo14 cookbook</td>
    </tr>
</table>

## 大綱
#### 書中各章節有點重複或不清楚，紀錄自己修改的CODE進行紀錄，書本資料來源:https://alanhou.org/odoo-14-creating-odoo-add-on-modules/

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
  
    dropdb odoo-test2
    rm -rf ~/.local/share/Odoo/filestore/odoo-test2

  14. 建立備份
  
    pg_dump -Fc -fodoo-test.dump odoo-test
    tar cjf odoo-test.tgz odoo-test.dump ~/.local/share/Odoo/filestore/odoo-test
  
   15. 還原備份
  
    tar xf odoo-test.tgz
    pg_restore -C -d odoo-test odoo-test.dump
    
   16. 配置服務
  
    ./odoo-bin --save --config myodoo.cfg --stop-after-init
    ./odoo-bin --help | less    可查詢指令
    ./odoo-bin -c myodoo.cfg    開始指令
    
## 第二章 管理Odoo服務端實例
   1. 配置插件位置  addons_path=~/odoo-dev/odoo/addons,~/odoo-dev/local-addons
   2. save選項保存路徑到配置文件中
   
    mkdir -p ~/odoo-dev/local-addons/dummy
    touch ~/odoo-dev/local-addons/dummy/__init__.py
    echo '{"name": "dummy", "installable": False}' > ~/odoo-dev/local-addons/dummy/__manifest__.py
    odoo/odoo-bin -d mydatabase --addons-path="odoo/odoo/addons,odoo/addons,~/odoo-dev/local-addons" --save -c ~/odoo-dev/my-instance.cfg --stop-after-init

   3. 標準化目錄布局
   a. 每個環境創立一個目錄：
     
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

## 第三章 創建ODOO的addons
  1. 進入到工作目錄即你要操作並放置新建的自定義模塊的插件目錄中：

    cd ~/odoo-dev/local-addons
    mkdir local-addons/my_library
    touch local-addons/my_library/__init__.py
    
  2. touch local-addons/my_library/__manifest__.py
  
    {
        'name': "My library",
        'summary': "輕鬆管理圖書",
        'description': """
    Manage Library
    ==============
    Description related to library.
         """,
        'author': "Harry",
        'website': "",
        'category': 'Uncategorized',
        'version': '14.0.1',
        'depends': ['base'],
        'data': [],
        'demo': [],
    }
    
3. 為代碼文件創建目錄：
    
    cd local-addons/my_library
    mkdir models
    touch models/__init__.py
    mkdir controllers
    touch controllers/__init__.py
    mkdir views
    touch views/views.xml
    mkdir security
    mkdir wizard
    touch wizard/__init__.py
    mkdir report
    mkdir data
    mkdir demo
    mkdir i18n

  4. 編輯模塊的頂級 __init__.py文件，這樣子目錄中的代碼會被加載到：
    
    from . import models
    from . import controllers
    from . import wizard

  5. 這會給我們一個包含最常用入手目錄結構，類似下面這樣：

    my_library
    ├── __init__.py
    ├── __manifest__.py
    ├── controllers
    │   └── __init__.py
    ├── data
    ├── demo
    ├── i18n
    ├── models
    │   └── __init__.py
    ├── report
    ├── security
    ├── static
    │   └── description
    │       └── icon.png
    ├── views
    │   └── views.xml
    └── wizard
        └── __init__.py
        
  6. 为模块添加一个 Python 文件models/library_book.py，代码如下：

    from odoo import models, fields

    class LibraryBook(models.Model):
        _name = 'library.book'
        name = fields.Char('Title', required=True)
        date_release = fields.Date('Release Date')
        author_ids = fields.Many2many(
            'res.partner',
            string='Authors'
        )

  7 models/__init__.py
    
    from . import library_book
    
  8. 查看安裝後資料庫數據方式。

    psql odoo-test
    test-14.0# \d library_book;
    \q
    
  10. 使用superuser可以不用設置權限就可以使用模組。
  11. library_book.xml
  
    <?xml version="1.0" encoding="utf-8"?>
    <odoo>
      <record id='library_book_action' model='ir.actions.act_window'>
        <field name="name">Library Books</field>
        <field name="res_model">library.book</field>
        <field name="view_mode">tree,form</field>
      </record>
      <menuitem name="My Library" id="library_base_menu" />
      <menuitem name="Books" id="library_book_menu" parent="library_base_menu"     action="library_book_action"/>
      <record id="library_book_view_form" model="ir.ui.view">
        <field name="name">Library Book Form</field>
        <field name="model">library.book</field>
        <field name="arch" type="xml">
            <form>
                <group>
                    <group>
                       <field name="name"/>
                       <field name="author_ids" widget="many2many_tags"/>
                    </group>
                    <group>
                        <field name="date_release"/>
                    </group>
                </group>
            </form>
        </field>
      </record>
      <record id="library_book_view_tree" model="ir.ui.view">
        <field name="name">Library Book List</field>
        <field name="model">library.book</field>
        <field name="arch" type="xml">
            <tree>
                <field name="name"/>
                <field name="date_release"/>
            </tree>
        </field>
      </record>
      <record id="library_book_view_search" model="ir.ui.view">
        <field name="name">Library Book Search</field>
        <field name="model">library.book</field>
        <field name="arch" type="xml">
           <search>
                <field name="name"/>
                <field name="author_ids"/>
                <filter string="No Authors" name="without_author" domain="[('author_ids','=',False)]"/>
            </search>
        </field>
      </record>
    </odoo>

  12. __manifest__.py
  
    {
        'name': "My library",
        'summary': "輕鬆管理圖書",
        'description': """
    Manage Library
    ==============
    Description related to library.
         """,
        'author': "Harry",
        'website': "",
        'category': 'Uncategorized',
        'version': '14.0.1',
        'depends': ['base'],
        'data': [
                 'security/groups.xml',
                 'security/ir.model.access.csv',
                 'views/library_book.xml'
                ],
        'demo': [],
    }

  13. security/groups.xml

    <?xml version="1.0" encoding="utf-8" ?>
    <odoo>
        <record id="group_librarian" model="res.groups">
            <field name="name">Librarians</field>
            <field name="users" eval="[(4, ref('base.user_admin'))]" />
        </record>
    </odoo>
    
  14. security/ir.model.access.csv

    id,name,model_id:id,group_id:id,perm_read,perm_write,perm_create,perm_unlink
    acl_book,library.book_default,model_library_book,,1,0,0,0
    acl_book_librarian,library.book_librarian,model_library_book,group_librarian,1,1,1,1
    
  15. ~/odoo-dev/odoo/odoo-bin scaffold my_module2
  16. 内置的模板位于./odoo/cli/templates，可使用~/odoo-dev/odoo/odoo-bin scaffold -t "自定義路徑" my_module3，此處使用了default模板，但也可以為網站主題編寫的theme模板。
  
## 第四章 應用模型
  1. 
