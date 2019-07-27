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

Varificar instalación
```
    http://localhost:8000/
```

Varificar servicios desde al api manager
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