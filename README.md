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

```
migrations/
        env.py
        README
        script.py.mako
        versions/
            3512b954651e\_add\_account.py
            2b1ae634e5cd\_add\_order_id.py
            3adcc9a56557\_rename\_username_field.py
alembic.ini
```

#### Referencias
[http://alembic.zzzcomputing.com/en/latest/tutorial.html](http://alembic.zzzcomputing.com/en/latest/tutorial.html)