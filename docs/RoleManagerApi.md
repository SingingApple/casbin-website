---
id: rolemanager-api
title: RoleManager API
---

## RoleManager

RoleManager provides interface to define the operations for managing roles.
Adding matching function to rolemanager allows using wildcards in role name and domain.

### `AddNamedMatchingFunc()`

AddNamedMatchingFunc add MatchingFunc by ptype RoleManager.
MatchingFunc will work when operating role matching.

```go
    e.AddNamedMatchingFunc("g", "", util.KeyMatch)
	_, _ = e.AddGroupingPolicies([][]string{{"*", "admin", "domain1"}})
	_, _ = e.GetRoleManager().HasLink("bob", "admin", "domain1") // -> true, nil
```

For example:

<!--DOCUSAURUS_CODE_TABS-->

<!--Go-->
```go
    e, _ := casbin.NewEnforcer("path/to/model", "path/to/policy")
    e.AddNamedMatchingFunc("g", "", util.MatchKey)
```

<!--END_DOCUSAURUS_CODE_TABS-->

### `AddNamedDomainMatchingFunc()`

AddNamedDomainMatchingFunc add MatchingFunc by ptype to RoleManager.
`DomainMatchingFunc` is similar to `MatchingFunc` listed above.

For example:

<!--DOCUSAURUS_CODE_TABS-->

<!--Go-->
```go
    e, _ := casbin.NewEnforcer("path/to/model", "path/to/policy")
    e.AddNamedDomainMatchingFunc("g", "", util.MatchKey)
```

<!--END_DOCUSAURUS_CODE_TABS-->

### `GetRoleManager()`

GetRoleManager gets the current role manager for `g`.

For example:

<!--DOCUSAURUS_CODE_TABS-->

<!--Go-->
```go
    rm := e.GetRoleManager()
```

<!--END_DOCUSAURUS_CODE_TABS-->

### `Clear()`

Clear clears all stored data and resets the role manager to the initial state.


For example:

<!--DOCUSAURUS_CODE_TABS-->

<!--Go-->
```go
    rm.Clear()
```

<!--END_DOCUSAURUS_CODE_TABS-->

### `AddLink()`

AddLink adds the inheritance link between two roles. role: name1 and role: name2.
Domain is a prefix to the roles (can be used for other purposes).

For example:

<!--DOCUSAURUS_CODE_TABS-->

<!--Go-->
```go
    rm.AddLink("u1", "g1", "domain1")
```

<!--END_DOCUSAURUS_CODE_TABS-->
### `DeleteLink()`

DeleteLink deletes the inheritance link between two roles. role: name1 and role: name2.
Domain is a prefix to the roles (can be used for other purposes).

For example:

<!--DOCUSAURUS_CODE_TABS-->

<!--Go-->
```go
    rm := DeleteLink("u1", "g1", "domain1")
```

<!--END_DOCUSAURUS_CODE_TABS-->

###	`HasLink()`

HasLink determines whether a link exists between two roles. role: name1 inherits role: name2.
Domain is a prefix to the roles (can be used for other purposes).

For example:

<!--DOCUSAURUS_CODE_TABS-->

<!--Go-->
```go
    rm.HasLink("u1", "g1", "domain1")
```

<!--END_DOCUSAURUS_CODE_TABS-->

### `GetRoles()`

GetRoles gets the roles that a user inherits.
Domain is a prefix to the roles (can be used for other purposes).

For example:

<!--DOCUSAURUS_CODE_TABS-->

<!--Go-->
```go
    rm.GetRoles("u1", "domain1")
```

<!--END_DOCUSAURUS_CODE_TABS-->

### `GetUsers()`

GetUsers gets the users that inherits a role.
Domain is a prefix to the users (can be used for other purposes).

For example:

<!--DOCUSAURUS_CODE_TABS-->

<!--Go-->
```go
    rm.GetUsers("g1")
```

<!--END_DOCUSAURUS_CODE_TABS-->

### `PrintRoles()`

PrintRoles prints all the roles to log.

For example:

<!--DOCUSAURUS_CODE_TABS-->

<!--Go-->
```go
    rm.PrintRoles()
```

<!--END_DOCUSAURUS_CODE_TABS-->

### `SetLogger()`

SetLogger sets role manager's logger.

For example:

<!--DOCUSAURUS_CODE_TABS-->

<!--Go-->
```go
	logger := log.DefaultLogger{}
	logger.EnableLog(true)
	rm.SetLogger(&logger)
	_ = rm.PrintRoles()
```

<!--END_DOCUSAURUS_CODE_TABS-->