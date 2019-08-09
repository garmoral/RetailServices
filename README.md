# Proyecto Microservicios Retail Services

## Compilación

``` bash
    cd api-manager
    mvn clean package
    
    cd order-service
    mvn clean package
    
    cd product-service
    mvn clean package
        
    cd user-service
    mvn clean package
```

Levantar BD
Usuario: postgres  
```bash
    docker run --name postgresdb -p 5432:5432 -e POSTGRES_DB=unbound -e POSTGRES_PASSWORD=project123 -d postgres
```

Actualizar BD, esto toma el xml y lo convierte a sentencias sql para postgres   
```
    Checar liquibase.properties
    cd liquidbase/
    liquibase --changeLogFile="changesets/db.changelog-master.xml" update
```

Levantar Servicios   
```
    cd api-manager/
    java -jar target/*.jar
    
    cd order-service/
    java -jar order-web/target/order-web-1.0-SNAPSHOT.jar
    
    cd product-service/
    java -jar product-web/target/product-web-1.0-SNAPSHOT.jar
    
    cd user-service/
    java -jar user-web/target/user-web-1.0-SNAPSHOT.jar
```

Verificar instalación
```
    http://localhost:8000/
```

Verificar servicios desde al api manager
```
    http://localhost:8000/api/orders/order/test
    http://localhost:8000/api/products/product/test
    http://localhost:8000/api/users/user/test
```

Directo a los servicios
```
    http://localhost:8200/order/test
    http://localhost:8300/product/test
    http://localhost:8100/user/test
```


Dockerfile (api-manager)
```
    docker build -t api_manager -f Dockerfile-apimanager .
    docker run -d -p 8000:8000 api_manager
```

Dockerfile-order
```
    docker build -t api_order_service -f Dockerfile-order .
    docker run -d -p 8200:8200 api_order_service
```

Dockerfile-product
```
    docker build -t api_product_service -f Dockerfile-product .
    docker run -d -p 8300:8300 api_product_service
```

Dockerfile-user
```
    docker build -t api_user_service -f Dockerfile-user .
    docker run -d -p 8100:8100 api_user_service
```

Docker compose
```
    docker-compose up -d
    docker network connect reatilservices_default postgresdb
    docker network disconnect reatilservices_default postgresdb
    docker-compose down --rmi all
```