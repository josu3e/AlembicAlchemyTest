# Alembic - SqlAlchemy
#### Versionando Base de Datos
En este repositorio pretendo hacer un ejemplo basico de como versionar los cambios en nuestra BD usando Alembic, SqlAchemy y como motor de BD Mysql.
#### Clonar el repositorio
```
git clone https://github.com/josu3e/alchemyTest.git
cd alchemyTest/
```
#### Entorno virtual
Para ello ejecutamos los siguientes comandos, y obtenemos un contenedor para nuestras dependencias agregadas en el archivo `requirements.txt`:
```
virtualenv env
source env/bin/activate
pip install -r requirements.txt
```
#### Inicializamos alembic
```
alembic init migrations
```
Esta es la estructura de carpetas y archivos que crea de forma automatica el comando anterior:
```
migrations/
	env.py
    README
    script.py.mako
	versions/
alembic.ini
```
#### Configuramos alembic
Es necesario modificar en el archivo `alembic.ini`. (Linea 38)
```
# sqlalchemy.url = driver://user:pass@localhost/dbname
sqlalchemy.url = mysql+mysqldb://root:passwd@localhost:3307/testdb?charset=utf8
```
#### Creamos la primera prueba
```
alembic revision -m "create user table"
```
Como resultado nos crea el siguiente archivo `a5d1c08ce3f2_create_user_table.py` en  la carpeta *"versions"*
```
migrations/
	...
	versions/
		a5d1c08ce3f2_create_user_table.py
```
En este archivo generado por la funcion anterior podemos revisar secciones importantes como *"revision"* la cual es similar a la parte inicial del nombre de archivo  (***a5d1c08ce3f2**_create_user_table.py*). En este caso el valor para *"down_revision"* va ser *"None"* por tratarse de nuestra primera iteración con alembic.
```
# revision identifiers, used by Alembic.
revision =  'a5d1c08ce3f2'
down_revision =  None
branch_labels =  None
depends_on =  None
```
Editamos las funciones **upgrade()** y **downgrade()**
```
def upgrade():
    op.create_table(
        'user',
        sa.Column('id', sa.Integer, primary_key=True),
        sa.Column('name', sa.String(50), nullable=False),
        sa.Column('lastname', sa.Unicode(200)),
    )

def downgrade():
    op.drop_table('user')
```
#### Ejecutamos nuestro codigo
Para ello es necesario escribir en la consola de nuestro ambiente virtual lo siguiente:
```
alembic upgrade head
```
#### Creamos una segunda prueba
```
alembic revision -m "user add a column"
```
```
migrations/
	...
	versions/
		a5d1c08ce3f2_create_user_table.py
		2c30b3d52da6_user_add_a_column.py
```
```  
def  upgrade():
	op.add_column('user', sa.Column('last_update_date', sa.DateTime))

def  downgrade():
	op.drop_column('user', 'last_transaction_date')
```
```
alembic upgrade head
```
#### Comandos adicionales
Para verificar la ultima revision aplicada:
```
alembic current
```
Para aplicar cambios o quitarlos a partir de la revision actual (current):
```
alembic upgrade +1
alembic upgrade a5d1+2
alembic downgrade -2
```

#### Referencias
[http://alembic.zzzcomputing.com/en/latest/tutorial.html](http://alembic.zzzcomputing.com/en/latest/tutorial.html)