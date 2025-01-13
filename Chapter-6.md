1. `MyBatis` is an open source Java persistence framework that abstracts JDBC boilerplate code and provides a simple and easy-to-use API to interact with database
2. It's a *SQL mapping farmework* - automates the process of populating the `SQL resultset` into java objects and it persists data into tables by extracting the data from the Java objects
3. `mybatis-spring-boot-starter` - dependency
4. Create a SQL mapper interface
5. XML based configuration - create mapper XML files for SQL statement query definitions and mapping of corresponding mapper interface methods
```java
package com.apress.demo.mappers;
public interface UserMapper
{
	void insertUser(User user);
	User findUserById(Integer id);
	List<User> findAllUsers();
}
```

```xml
<!DOCTYPE mapper
  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="com.apress.demo.mappers.UserMapper">

  <resultMap id="UserResultMap" type="User">
    <id column="id" property="id" />
    <result column="name" property="name" />
    <result column="email" property="email" />
  </resultMap>

  <select id="findAllUsers" resultMap="UserResultMap">
    select id, name, email from users
  </select>

  <select id="findUserById" resultMap="UserResultMap">
    select id, name, email from users WHERE id=#{id}
  </select>

  <insert id="insertUser" parameterType="User" 
	  useGeneratedKeys="true" keyProperty="id">
    insert into users(name, email) values(#{name}, #{email})
  </insert>

</mapper>
```
   
6. Observations-
	1.  The namespace in the mapper XML should be the same as the *Fully Qualified Name (FQN)* of the mapper interface.
	2. The statement id values should be the same as the mapper interface method names.
	3. If the query result column names are different from the bean property names, then the `<resultMap>` configuration can be used to provide mapping between column names and their corresponding bean property names.
7. MyBatis also provides annotation-based query configurations without needing mapper XMLs-
   ```java
	public interface UserMapper
	{
	    @Insert("insert into users(name,email) values(#{name},#{email})")
	    @SelectKey(statement="call identity()", keyProperty="id",
	                before=false, resultType=Integer.class)
	    void insertUser(User user);
	    @Select("select id, name, email from users WHERE id=#{id}")
	    User findUserById(Integer id);
	    @Select("select id, name, email from users")
	    List<User> findAllUsers();
	}
	```

8. Configure the starter configuration parameters inside the `application.properties`
9. `@MapperScan("path-to-the-mapper-interface")` - to annotate the bootstrapping class to specify where to look for the mapper interface. Instead of using `@MapperScan`, it is possible to annotate mapper interfaces with new `@Mapper` annotation 
10. [Spring Boot integration docs](https://mybatis.org/spring-boot-starter/mybatis-spring-boot-autoconfigure/)
