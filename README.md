This is mongodb with docker-compose

@creat action role root:
use admin
db.createRole(
  {
    role: "root",
    privileges: [
      { resource: { anyResource: true }, actions: [ "anyAction" ] }
    ],
    roles: []
  }
)

@creat action role non-root:
use otherdb
db.createRole(
   {
     role: "dbOwner",
     privileges: [
       { resource: { db: "otherdb", collection: "" }, actions: [ "find", "insert", "update", "remove" ] },
     ],
     roles: []
   }
)

@creat new user and add role:
db.createUser(
  {
    user: "otheruser",
    pwd: "otherpass",
    roles: [ { role: "root", db: "admin" } ]
  }
)