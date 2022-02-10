App 1 (Dapr StateStore)
```
dapr run --app-id DaprCounter dotnet run
```

NOTE
Default component configuration files arestored in the 
```$HOME/.dapr/components folder on Linux/macOS```
and in the
```%USERPROFILE%\.dapr\components folder on Windows```

To limit the namespaces between applications set it in the configuration, to limit the apps that can talk to the store you set the application names in the scope.

```
apiVersion: dapr.io/v1alpha1
kind: Component
metadata:
name: statestore
namespace: production <-- K8 namespaces
spec:
type: state.redis
version: v1
metadata:
- name: redisHost
value: localhost:6379
- name: redisPassword
value: ""
- name: actorStateStore
value: "true"
scopes:
- DaprCounter <-- App Name 
```