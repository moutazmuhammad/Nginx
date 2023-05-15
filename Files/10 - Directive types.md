# [Directive types](../Code/07%2BInheritince%2B%26%2BDirective%2BTypes.conf)

- Three main directive types is the `standard directive`, the `array directive` and the `action directive`.


## (1) Array Directive
- Can be specified multiple times without overriding a previous setting
- Gets inherited by all child contexts
- Child context can override inheritance by re-declaring directive
- Example:
```
access_log /var/log/nginx/access.log;
```

## (2) Standard Directive
- Can only be declared once. A second declaration overrides the first
- Gets inherited by all child contexts
- Child context can override inheritance by re-declaring directive
- Example:
```
root /sites/site2;
```

## (3) Action Directive
- Invokes an action such as a rewrite or redirect
- Inheritance does not apply as the request is either stopped (redirect/response) or re-evaluated (rewrite)
```
return 403 "You do not have permission to view this.";
```