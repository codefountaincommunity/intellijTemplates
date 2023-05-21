# IntellijTemplates
IntellijIdea provides two type of templates \
1)Live templates \
2)File and Code templates\
we can create our own templates


## CodeFountain Templates:
You can import LiveTemplates by File -> Manage IDE Settings -> Import Settings -> Select **codefountainintellijideatemplets.zip**
### Live Templates:
#### Java:
##### logger template:
Intellijidea goto settings -> Live Templates --> right hand side click **+** button select live template
abbravitation box write looger \
template text box past the below template \
click on editvariable expression field select **className()**
below template text select **define** expand java select **declaration** \

```private static final org.slf4j.Logger LOGGER = org.slf4j.LoggerFactory.getLogger($NAME$.class);
```
##### MySql:
Intellijidea goto settings -> Live Templates --> right hand side click **+** button select live template
abbravitation box write mysql \
template text box past the below template \
click on editvariable for NAME , USERNAME,PASSWORD expression field select **complete()** \
below template text select **define** select **properties file**


```
spring.datasource.url=jdbc:mysql://localhost:3306/$NAME$ \
spring.datasource.username=$USERNAME$ \
spring.datasource.password=$PASSWORD$ \
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver \
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQLDialect \
spring.jpa.hibernate.ddl-auto=update \ 

```

## File and code Template:

1)Entity template \
2)controller template \
3)serviceImpl template \
4)repository template \
5)package structure template \
6)curd operations template \