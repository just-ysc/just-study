# Precautions for use `antMatchers`

## Blacklisting

- 기본적으로 모든 endpoint를 허용하고, 특정한 endpoint만 접근을 금지하거나, 인증을 요구하는 방식
```java
@EnableWebSecurity
public class SecurityConfiguration extends WebSecurityConfigurerAdapter {
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.httpBasic().disable()
            .csrf().disable()
            .authorizeRequests()
            .antMatchers(GET, "/v1/api/members").authenticated()
            .anyRequest().permitAll();
    }
}
```
- 그러나 위와 같은 설정에서 `/v1/api/members/`로 끝에 슬래시가 붙은 상태에서 요청하면 200 응답을 받게 된다.
  - 보안상의 취약점이 된다([CVE-2016-5007](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-5007)).

## Whitelisting

- 위와 같은 상황을 방지하기 위해, Spring Security는 Whitelisting을 권장한다.
- Whitelisting은 기본적으로 모든 endpoint에 대해 접근을 금지하거나 인증을 요구하고, 특정 endpoint에 대해서만 허용하는 방식이다.
```java
@EnableWebSecurity
public class SecurityConfiguration extends WebSecurityConfigurerAdapter {
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.httpBasic().disable()
            .csrf().disable()
            .authorizeRequests()
            .antMatchers(POST, "/v1/api/members").permitAll()
            .anyRequest().authenticated();
    }
}
```

## Using wildcard

- 또 다른 방법으로는 wildcard를 사용하는 것이다.
```java
@EnableWebSecurity
public class SecurityConfiguration extends WebSecurityConfigurerAdapter {
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.httpBasic().disable()
            .csrf().disable()
            .authorizeRequests()
            .antMatchers(GET, "/v1/api/members/**").authenticated()
            .anyRequest().permitAll();
    }
}
```
- 이렇게 하면 슬래시를 포함한 모든 하위 endpoint에 대해서 인증을 요구하게 된다.

## `mvcMatchers`

- 아니면 `antMatchers` 대신 `mvcMatchers`를 사용하는 방법이 있다.
```java
@EnableWebSecurity
public class SecurityConfiguration extends WebSecurityConfigurerAdapter {
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.httpBasic().disable()
            .csrf().disable()
            .authorizeRequests()
            .mvcMatchers(GET, "/v1/api/members").authenticated()
            .anyRequest().permitAll();
    }
}
```

### Difference between `antMatchers` and `mvcMatchers`
TBU

## Reference

- https://shirohoo.github.io/spring/spring-security/2022-03-31-mvcMatchers/