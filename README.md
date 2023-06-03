# IntellijTemplates
IntellijIdea provides two type of templates \
1)Live templates \
2)File and Code templates\
we can create our own templates
## CodeFountain Templates
You can import LiveTemplates by File -> Manage IDE Settings -> Import Settings -> Select **settings.zip**
### Live Templates
#### Java
##### logger template
Intellijidea goto settings -> Live Templates --> right hand side click **+** button select live template
abbravitation box write looger \
template text box past the below template \
click on editvariable expression field select **className()**
below template text select **define** expand java select **declaration** 

```java
private static final org.slf4j.Logger LOGGER = org.slf4j.LoggerFactory.getLogger($NAME$.class);

```
##### MySql
Intellijidea goto settings -> Live Templates --> right hand side click **+** button select live template
abbravitation box write mysql \
template text box past the below template \
click on editvariable for NAME , USERNAME,PASSWORD expression field select **complete()** \
below template text select **define** select **properties file**


```ruby
spring.datasource.url=jdbc:mysql://localhost:3306/$NAME$
spring.datasource.username=$USERNAME$
spring.datasource.password=$PASSWORD$
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQLDialect
spring.jpa.hibernate.ddl-auto=update 

```
##### togglz

```ruby
togglz.features.$FEATURE_NAME$.enabled=true
togglz.console.enabled=true
togglz.console.path=/togglz-console
togglz.console.secured=false
togglz.console.use-management-port=false

```

## File and code Template:
**note:**  ***this file templates designed based on springboot version 3.0 if you are using springboot version below 3.0 you need to change the import statments all jakarta packages to javax package***
Intellijidea goto settings -> File and Code Templates --> under files->click on + icon \
file name ***Entity*** extension java

#### Entity  
```java
#if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME};#end
import jakarta.persistence.Id;
import jakarta.persistence.Entity;
import jakarta.persistence.Table;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Column;
import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@NoArgsConstructor
@AllArgsConstructor
@Builder
@Entity
@Table(name = "${NAME.toLowerCase()}")
public class ${NAME} {
    @Id
    @Column(name = "id")
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
}

```

#### controller  
```java
#if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME};#end
#set ($index = $NAME.indexOf("Controller"))
#set ($API= $NAME.substring(0, $index))
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
@RestController
@RequestMapping("/${API}")
public class ${NAME} {
private static final Logger LOGGER = LoggerFactory.getLogger(${NAME}.class);

}
```

#### repository  
```java
#if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME};#end
#set ($index = $NAME.indexOf("Repository"))  #set ($index = $NAME.indexOf("Repo"))
#set ($ENTITY= $NAME.substring(0, $index))

import org.springframework.data.jpa.repository.JpaRepository;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public interface ${NAME} extends JpaRepository<$ENTITY, Long> {
private static final Logger LOGGER = LoggerFactory.getLogger(${NAME}.class);
}
```
#### ServiceImpl  
create serviceImpl templete frist we create base templete service class and then we create there implementation calss

##### Service
```java
#if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME};#end
public interface ${NAME}{
}
```
select this service templete and click on create child template
##### ServiceImpl 
```java
#if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME};#end
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Service;
import ${PACKAGE_NAME}.${NAME};
@Service
public class ${NAME}Impl implements ${NAME}{
private static final Logger LOGGER = LoggerFactory.getLogger(${NAME}Impl.class);


}
```

#### Package Structure Template 
create a base template as dummyclass 
```java
#if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME};#end
class Dummy${NAME}{
}
```
under this select child templete create below templetes

##### Dto 
filename: dto/${NAME}
```java
#if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME};#end
import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;
@Data
@NoArgsConstructor
@AllArgsConstructor
@Builder
public class ${NAME}DTO {
   
    private Long id;
    

    
}
```
##### Entity 
filename: entities/${NAME}
```java
#if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME};#end
import jakarta.persistence.Id;
import jakarta.persistence.Entity;
import jakarta.persistence.Table;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Column;
import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;
import ${PACKAGE_NAME}.dto.${NAME}DTO;
@Data
@NoArgsConstructor
@AllArgsConstructor
@Builder
@Entity
@Table(name = "${NAME.toLowerCase()}")
public class ${NAME} {
    @Id
    @Column(name = "id")
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;


    public ${NAME} dtoToEntity(${NAME}DTO ${NAME.toLowerCase()}Dto){
   
    ${NAME} ${NAME.toLowerCase()} = new ${NAME}();
       ${NAME.toLowerCase()}.setId(${NAME.toLowerCase()}Dto.getId());
        return ${NAME.toLowerCase()};
    }
    
    
    }
 
    
```
##### Service 
filename:services/${NAME}
```java
#if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME};#end
import ${PACKAGE_NAME}.entities.${NAME};
public interface ${NAME}Service{
}
```
##### ServiceImpl 
fielname:services/impl/${NAME}
```java
#if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME};#end
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Service;
import org.springframework.beans.factory.annotation.Autowired;
import ${PACKAGE_NAME}.services.${NAME}Service;
import ${PACKAGE_NAME}.repositories.${NAME}Repository;

@Service
public class ${NAME}ServiceImpl implements ${NAME}Service{
private static final Logger LOGGER = LoggerFactory.getLogger(${NAME}ServiceImpl.class);

    @Autowired
    private  ${NAME}Repository ${NAME.toLowerCase()}Repository;
    
}
```
##### Repository 
filename: repositories/${NAME}
```java
#if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME};#end
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.jpa.repository.JpaRepository;
import ${PACKAGE_NAME}.entities.${NAME};
public interface ${NAME}Repository extends JpaRepository<${NAME}, Long> {
}
```
##### Controller 
filename: controller/${NAME}
```java
#if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME};#end

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;

import ${PACKAGE_NAME}.services.${NAME}Service;
@RestController
@RequestMapping("/${NAME.toLowerCase()}")
public class ${NAME}Controller {
private static final Logger LOGGER = LoggerFactory.getLogger(${NAME}Controller.class);
    @Autowired
    private  ${NAME}Service ${NAME.toLowerCase()}Service;
}
```
#### Curd Operations Template
it is same as above **Package Structure templete** here we cover basic curd operations like \
--> create \
--> update \
--> getById \
--> getAll \
--> getAllPageable \
--> deleteById \
--> deleteAll

##### Dto
```java
#if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME};#end
import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;
@Data
@NoArgsConstructor
@AllArgsConstructor
@Builder
public class ${NAME}DTO {
   
    private Long id;
    
    
}
```
##### Entity
```java
#if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME};#end
import jakarta.persistence.Id;
import jakarta.persistence.Entity;
import jakarta.persistence.Table;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Column;
import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;
import ${PACKAGE_NAME}.dto.${NAME}DTO;

@Data
@NoArgsConstructor
@AllArgsConstructor
@Builder
@Entity
@Table(name = "${NAME.toLowerCase()}")
public class ${NAME} {
    @Id
    @Column(name = "id")
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    public ${NAME} dtoToEntity(${NAME}DTO ${NAME.toLowerCase()}Dto){
   
    ${NAME} ${NAME.toLowerCase()} = new ${NAME}();
       ${NAME.toLowerCase()}.setId(${NAME.toLowerCase()}Dto.getId());
        return ${NAME.toLowerCase()};
    }
    
    
}
```
##### Repository
```java
#if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME};#end
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.jpa.repository.JpaRepository;
import ${PACKAGE_NAME}.entities.${NAME};

public interface ${NAME}Repository extends JpaRepository<${NAME}, Long> {
}
```
##### Service
```java
#if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME};#end
import org.springframework.data.domain.Page;
import org.springframework.data.domain.Pageable;
import ${PACKAGE_NAME}.entities.${NAME};
import ${PACKAGE_NAME}.dto.${NAME}DTO;
import java.util.List;
public interface ${NAME}Service{
  public ${NAME} create${NAME}(${NAME}DTO ${NAME.toLowerCase()}DTO);
    public ${NAME} update${NAME}(Long id, ${NAME}DTO ${NAME.toLowerCase()}DTO);
    public ${NAME} get${NAME}ById(Long id);  
    public List<${NAME}> getAll${NAME}s();
    public Page<${NAME}> getAll${NAME}s(Pageable pageable);
    public void delete${NAME}(Long id);
    public void deleteAll${NAME}s(); 

}
```
##### ServiceImpl
```java
#if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME};#end
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.data.domain.Page;
import org.springframework.data.domain.Pageable;
import org.springframework.stereotype.Service;
import org.springframework.beans.factory.annotation.Autowired;
import java.util.List;
import java.util.Optional;
import ${PACKAGE_NAME}.entities.${NAME};
import ${PACKAGE_NAME}.dto.${NAME}DTO;
import ${PACKAGE_NAME}.services.${NAME}Service;
import ${PACKAGE_NAME}.repositories.${NAME}Repository;

@Service
public class ${NAME}ServiceImpl implements ${NAME}Service{
private static final Logger LOGGER = LoggerFactory.getLogger(${NAME}ServiceImpl.class);

    @Autowired
    private  ${NAME}Repository ${NAME.toLowerCase()}Repository;
     @Override
     public ${NAME} create${NAME}(${NAME}DTO ${NAME.toLowerCase()}DTO) {
        ${NAME} ${NAME.toLowerCase()}= new ${NAME}();
       ${NAME} new${NAME}= ${NAME.toLowerCase()}.dtoToEntity(${NAME.toLowerCase()}DTO);
        LOGGER.info("${NAME} created");
        return ${NAME.toLowerCase()}Repository.save(new${NAME});
    }
    
    @Override
    public ${NAME} update${NAME}(Long id, ${NAME}DTO ${NAME.toLowerCase()}DTO) {
        ${NAME}  existing${NAME}  = get${NAME}ById(id);
              ${NAME} updated${NAME}=existing${NAME}.dtoToEntity(${NAME.toLowerCase()}DTO);
         LOGGER.info("${NAME} updated");
        return ${NAME.toLowerCase()}Repository.save(updated${NAME});
    }
    
     @Override
    public ${NAME} get${NAME}ById(Long id) {
        LOGGER.info("getEmployeeId:" + id);
        Optional<${NAME}> ${NAME.toLowerCase()}= ${NAME.toLowerCase()}Repository.findById(id);
        if(${NAME.toLowerCase()}.isPresent()){
            return ${NAME.toLowerCase()}.get();

        }
            else{
             LOGGER.info("${NAME} doesn't exist");
            return null;
        }
    }
     @Override
    public List<${NAME}> getAll${NAME}s() {
    LOGGER.info("getAll ${NAME}s");
        return ${NAME.toLowerCase()}Repository.findAll();
    }
    
     @Override
    public Page<${NAME}> getAll${NAME}s(Pageable pageable) {
    LOGGER.info("getAll Pageable ${NAME}s");
        return ${NAME.toLowerCase()}Repository.findAll(pageable);
    }
     @Override
    public void delete${NAME}(Long id) {
    ${NAME} ${NAME.toLowerCase()} = get${NAME}ById(id);
    LOGGER.info("delete ${NAME} Id"+id);
    ${NAME.toLowerCase()}Repository.delete(${NAME.toLowerCase()});
    }
    
      @Override
    public void deleteAll${NAME}s() {
    LOGGER.info("delete ${NAME}s");
        ${NAME.toLowerCase()}Repository.deleteAll();
    }
}

```
##### Controller
```java
#if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME};#endimport org.springframework.data.domain.Page;
import org.springframework.data.domain.PageRequest;
import org.springframework.data.domain.Pageable;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestParam;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import java.util.List;
import ${PACKAGE_NAME}.services.${NAME}Service;
import ${PACKAGE_NAME}.dto.${NAME}DTO;
import ${PACKAGE_NAME}.entities.${NAME};
@RestController
@RequestMapping("/${NAME.toLowerCase()}")
public class ${NAME}Controller {
private static final Logger LOGGER = LoggerFactory.getLogger(${NAME}Controller.class);
    @Autowired
    private  ${NAME}Service ${NAME.toLowerCase()}Service;
    
     @PostMapping("/create")
    public ResponseEntity<${NAME}> create${NAME}(@RequestBody ${NAME}DTO ${NAME.toLowerCase()}DTO) {
        ${NAME} created${NAME} = ${NAME.toLowerCase()}Service.create${NAME}(${NAME.toLowerCase()}DTO);
      LOGGER.info("${NAME} created");
        return ResponseEntity.status(HttpStatus.CREATED).body(created${NAME});
    }
    @PutMapping("/update/{id}")
    public ResponseEntity<${NAME}> update${NAME}(@PathVariable Long id, @RequestBody ${NAME}DTO ${NAME.toLowerCase()}DTO) {
        ${NAME} updated${NAME} = ${NAME.toLowerCase()}Service.update${NAME}(id, ${NAME.toLowerCase()}DTO);
      LOGGER.info("${NAME} updated");
        return ResponseEntity.ok(updated${NAME});
    }
    @GetMapping("/getAll${NAME}s")
    public ResponseEntity<List<${NAME}>> getAll${NAME}s() {
        List<${NAME}> ${NAME.toLowerCase()}s = ${NAME.toLowerCase()}Service.getAll${NAME}s();
       LOGGER.info("getAll ${NAME}s");
        return ResponseEntity.ok(${NAME.toLowerCase()}s);
    }
    @GetMapping("/get${NAME}/{id}")
    public ResponseEntity<${NAME}> get${NAME}ById(@PathVariable Long id) {
        ${NAME} ${NAME.toLowerCase()} = ${NAME.toLowerCase()}Service.get${NAME}ById(id);
        if(${NAME.toLowerCase()}!=null) {
            LOGGER.info("get${NAME}Id:" + id);
            return ResponseEntity.ok(${NAME.toLowerCase()});
        }
        else{
            return ResponseEntity.notFound().build();

        }
    }
  
     @GetMapping("/getAll${NAME}s/pageable")
    public ResponseEntity<Page<${NAME}>> getAll${NAME}s(
            @RequestParam(defaultValue = "0") int page,
            @RequestParam(defaultValue = "10") int size
    ) {
        Pageable pageable = PageRequest.of(page, size);
        Page<${NAME}> ${NAME.toLowerCase()}s = ${NAME.toLowerCase()}Service.getAll${NAME}s(pageable);
       LOGGER.info("getAll Pageable ${NAME}s");
        return ResponseEntity.ok(${NAME.toLowerCase()}s);
    }
    @DeleteMapping("/delete${NAME}/{id}")
    public ResponseEntity<Void> delete${NAME}(@PathVariable Long id) {
        ${NAME.toLowerCase()}Service.delete${NAME}(id);
        LOGGER.info("delete ${NAME} Id"+id);
        return ResponseEntity.noContent().build();
    }

    @DeleteMapping("/deleteAll${NAME}s")
    public ResponseEntity<Void> deleteAll${NAME}s() {
       ${NAME.toLowerCase()}Service.deleteAll${NAME}s();
        LOGGER.info("delete ${NAME}s");
        return ResponseEntity.noContent().build();
    }
}

```
