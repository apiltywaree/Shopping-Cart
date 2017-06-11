# Shopping-Cart
Shopping cart application using spring, hibernate, bootstrap, angular js

########use schema name if my sql used-> here emusicstore is the schema########
create table users(
      username varchar_ignorecase(50) not null primary key,
      password varchar_ignorecase(50) not null,
      enabled boolean not null);

  create table authorities (
      username varchar_ignorecase(50) not null,
      authority varchar_ignorecase(50) not null,
      constraint fk_authorities_users foreign key(username) references users(username));
      create unique index ix_auth_username on authorities (username,authority);
      
      <security:http auto-config="true">
		<security:intercept-url pattern="/admin/**"
			access="ROLE_USER" />
		<security:form-login login-page="/login"
			default-target-url="/admin/" authentication-failure-url="/login?error"
			username-parameter="username" password-parameter="password" />
		<security:logout logout-success-url="/login?logout" />
	</security:http>

	<security:authentication-manager>
		<security:authentication-provider>
			<security:jdbc-user-service
				data-source-ref="dataSource"
				authorities-by-username-query="SELECT username, authority From emusicstore.authorities WHERE username = ?"
				users-by-username-query="SELECT username, password, enabled FROM emusicstore.users WHERE username = ?" />
		</security:authentication-provider>
	</security:authentication-manager>
