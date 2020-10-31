# quarkus-enable-native-reflection
how to configure third party jar classes to be marked as register for reflection

to enable third party jar classes you have to configure native build at application.properties (@see applicat)
```
#######################
#Builder
#######################
quarkus.native.additional-build-args =-H:ReflectionConfigurationFiles=reflection-config.json,\
-H:ResourceConfigurationFiles=resources-config.json,\
-H:+TraceClassInitialization, -H:+AllowIncompleteClasspath
#, --report-unsupported-elements-at-runtime
```
And now configure what classes will be marked , specified on reflection-config.json
```
[
  {
    "name" : "org.hibernate.reactive.persister.collection.impl.ReactiveOneToManyPersister",
    "allDeclaredConstructors" : true,
    "allPublicConstructors" : true,
    "allDeclaredMethods" : true,
    "allPublicMethods" : true,
    "allDeclaredFields" : true,
    "allPublicFields" : true
  },
  {
    "name" : "org.hibernate.reactive.persister.collection.impl.ReactiveManyToOnePersister",
    "allDeclaredConstructors" : true,
    "allPublicConstructors" : true,
    "allDeclaredMethods" : true,
    "allPublicMethods" : true,
    "allDeclaredFields" : true,
    "allPublicFields" : true
  },
  ...
  ```

  The resources-config.json file specified what static content will be added to native image too.