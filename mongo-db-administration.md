# MongoDB Database Commands

- **List databases:** `show dbs`
- **Switch/create db:** `use mydb`
- **Current db:** `db`
- **Drop db:** `db.dropDatabase()`


## User & Authentication Management

### Create Admin User

```javascript
use admin

db.createUser({
  user: "adminUser",
  pwd: "StrongPassword",
  roles: [ { role: "root", db: "admin" } ]
})
```

### Create Read/Write User for a DB

```javascript
use mydb

db.createUser({
  user: "appUser",
  pwd: "AppPassword",
  roles: [ { role: "readWrite", db: "mydb" } ]
})
```

### List Users

```javascript
use admin

db.getUsers()
```

### Update User Password

```javascript
db.updateUser("appUser", { pwd: "NewPassword" })
```

### Delete User

```javascript
db.dropUser("appUser")
```

## Role Management

### List Roles

```javascript
use admin

db.getRoles({ showBuiltinRoles: true })
```

### Grant Role to User

```javascript
db.grantRolesToUser("appUser", [{ role: "dbAdmin", db: "mydb" }])
```

### Revoke Role from User

```javascript
db.revokeRolesFromUser("appUser", [{ role: "dbAdmin", db: "mydb" }])
```






Practice

db.createUser({
  user: "prodAppUser",
  pwd: "----------------",
  roles: [ { role: "readWrite", db: "prod-stock-db" } ]
});

db.createUser({
  user: "devAppUser",
  pwd: "---------------",
  roles: [ { role: "readWrite", db: "dev-stock-db" } ]
});





db.updateUser("devAdminUser", { pwd: "LocalP$123" })

mongodb://devAdminUser:LocalP$123@3.108.2.222:27017/admin

db.dropUser("devAdminUser")

db.grantRolesToUser("appUser", [{ role: "dbAdmin", db: "mydb" }])


