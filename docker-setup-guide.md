
# 🏗️ Guía para la Base de Datos  

## 🌐 **Configuración de la red compartida (`nabi-network`)**  
Docker maneja la comunicación entre servicios mediante **redes internas**.  
- La red `nabi-network` permite que el backend, la base de datos y el frontend **se comuniquen entre sí por nombre de servicio** en lugar de IP o `localhost`.  
- Docker resolverá automáticamente el nombre del contenedor como `nabi_backend`, `nabi_mysql`, `nabi_frontend`, etc.  
- Si la red **no existe**, créala manualmente antes de levantar cualquier servicio:  

```bash
docker network create nabi-network
```

✅ Si la red ya existe → Docker simplemente la usará.  
✅ Si la red no existe → Docker la creará automáticamente.  

---


## **1️⃣ Detener y eliminar la base de datos**
Para detener solo la base de datos (sin afectar el backend o el frontend):

```bash
docker compose down
```

Si quieres eliminar también los volúmenes (esto eliminará los datos guardados):

```bash
docker compose down -v
```

---

## **2️⃣ Eliminar imagen de MySQL**
Si necesitas reconstruir la imagen de MySQL:

```bash
docker rmi mysql:8.0
```

---

## **3️⃣ Levantar la base de datos**
Para reconstruir y levantar MySQL y Adminer desde cero:

```bash
docker compose up --build
```

Para ejecutarlo en segundo plano:

```bash
docker compose up --build -d
```

---

## **4️⃣ Verificar que la base de datos está corriendo**
```bash
docker ps
```

✅ Si todo está bien, debería aparecer algo como esto:

```
CONTAINER ID   IMAGE         STATUS         PORTS                   NAMES
efgh5678       mysql:8.0     Up 10 seconds  0.0.0.0:3306->3306/tcp  nabi_mysql
ijkl9012       adminer       Up 10 seconds  0.0.0.0:8080->8080/tcp  mi-adminer
```

---

## **5️⃣ Acceder a Adminer**
Adminer estará disponible en:

```
http://localhost:8080
```

✅ Credenciales de acceso:
- **Sistema:** MySQL  
- **Servidor:** nabi_mysql  
- **Usuario:** root  
- **Contraseña:** root  

---

## **6️⃣ Conectarse manualmente a MySQL**
Si necesitas entrar directamente al contenedor:

```bash
docker exec -it nabi_mysql mysql -u root -p
```

