---
title: JAVA-JPA-Setting
date: 2020-02-26 01:39:58
---

## JPA (Java Persistence API)

* Java 持久化 API
* 是 Java 對 **ORM(Object-Relation Mapping)** 做出的規範，一個`介面(Interface)`
* 讓 `Model class`跟 `DB Table` 做映射,取代直接跟 DB要資料
* 以 **hibernate**實作 JPA
* 設定 `persistence.xml`
    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <persistence version="1.0" 
    xmlns="http://java.sun.com/xml/ns/persistence" 
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
    xsi:schemaLocation="http://java.sun.com/xml/ns/persistence http://java.sun.com/xml/ns/persistence/persistence_1_0.xsd">
    <persistence-unit name="ContactPU" transaction-type="RESOURCE_LOCAL">
        <provider>org.hibernate.ejb.HibernatePersistence</provider>
        <class>Contact.Contact</class>
        <properties>
        <property name="hibernate.cache.provider_class" value="org.hibernate.cache.NoCacheProvider"/>
        <property name="hibernate.connection.driver_class" value="com.mysql.jdbc.Driver"/>
        <property name="hibernate.connection.url" value="jdbc:mysql://資料庫-IP:資料庫服務-TCP-埠號/資料庫名稱"/>
        <property name="hibernate.connection.username" value="資料庫帳號"/>
        <property name="hibernate.connection.password" value="資料庫密碼"/>
        </properties>
    </persistence-unit>
    </persistence>
    ```
* 建立 Table 對 物件的映射
    ```java
    @Entity
    public class Customer {
        @Id
        @GeneratedValue(strategy = GenerationType.IDENTITY)
        private Long id;
        private String name;
        private String email;
        private String address;
        
        protected Customer() {
            
        }
        
        protected Customer(String name,String email,String address) {
            this.name = name;
            this.address = address;
            this.email = email;		
        }
        
        public Long getId() {
            return this.id;
        }

        public String getName() {
            return this.name;
        }
        public void setName(String name) {
            this.name=name;
        }
        
        public String getEmail() {
            return this.email;
        }
        public void setEmail(String email) {
            this.email=email;
        }
        
        public String getAddress() {
            return this.address;
        }
        public void setAddress(String address) {
            this.address=address;
        }

    }
    ```
* 建立 `CrudRepository`
    ```java
    public interface CustomerRepository extends CrudRepository<Customer, Long>{

        //要做複雜的 Query
        @Query(value = 
                "SELECT c "
                + "FROM Customer c "
                + "WHERE c.name LIKE '%' || :keyword || '%'"
                + " OR c.email LIKE '%' || :keyword || '%'"
                + " OR c.address LIKE '%' || :keyword || '%'")
        public List<Customer> search(@Param("keyword") String keyword);
    }
    ```
* 建立 `Service`

    ```java

    @Service
    @Transactional
    public class CustomerService {
        @Autowired CustomerRepository repo;
        
        public void save(Customer customer) {
            repo.save(customer);		
        }
        
        public List<Customer> listAll() {
            return (List<Customer>)repo.findAll();		
        }
        
        public Customer get(Long Id) {
            return repo.findById(Id).get();
        }
        
        public void delete(Long Id) {
            repo.deleteById(Id);
        }
        
        public List<Customer> search(String keyword) {
            return repo.search(keyword);
        }
    }
    ```

 