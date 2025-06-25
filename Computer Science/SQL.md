#data8 #cs161 

**Structured query language**, or SQL, is a language used to interact with [[databases]]. It is a *declarative* programming language, meaning that we use it to state the desired result, rather than the process of getting to the result.
### syntax

As the name suggests, SQL is a query-based language. This means that we create statements to tell the database server to tell it what data we're looking for. Queries are comprised of a few syntactic features:
- **Keywords** perform specific, pre-defined tasks. These are denoted by being all caps.
- **Identifiers** are named parts of the database schema, like tables, columns, and views
---
## sql injection

SQL injection is a malicious attack where attackers insert their own SQL into queries constructed by the server. 

For some background, when [[world wide web|websites]] have spaces which allow for user input or search, they often time use that user input as a field in a SQL query to return relevant data. This means that those queries contain blanks that are filled by whatever is sent from the client to the server. If the server's handling of that input is not secure, it can allow for attackers to cause malicious behavior.

##### example
Take the following example code which could exist in a web server for `www.vulnerable.com`:
```
username = r.URL.Query()["item"][0]

query := "SELECT name, age FROM users WHERE name= '%s'"
row, err := database.QueryRow(fmt.Sprintf(query, username))
```
Here, `username` is pulled from the request from the user, where the request looks something like this:
```
http://vulnerable.com/users?username=erin
```
This is the expected input, where `username` is a plaintext string. However, an attacker could set there username to something like this:
```
http://vulnerable.com/users?username='; DROP TABLE users --
```

