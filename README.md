## Property Precedence
Spring Boot applies configuration in a specific order, creating layers of properties. When the same property is defined in multiple places, the one with the higher precedence (the one applied later) wins.

Here's the simplified order of precedence for your scenario, from highest to lowest:

1. Local Profile Properties (application-local.yml): These are the most specific and will override everything below them.

2. Local Application Properties (application.yml): The base local configuration.

3. Remote Properties from Config Server: These act as the default values for your application. They have the lowest priority and can be easily overridden locally.


### 🔹 How values are merged

* Config files are **merged at the property level**, not file level.
* That means if both `application.yaml` and `ApiGateway.yaml` define a property, the one in `ApiGateway.yaml` **overrides** the one in `application.yaml`.
* Properties not overridden remain in effect (they "cascade down").

So effectively, **all relevant files are applied**, but **per-property priority** decides the final value.

---

### 🔹 Example

**application.yaml** (shared defaults on GitHub):

```yaml
server:
  port: 8080
management:
  endpoints:
    web:
      exposure:
        include: "*"
```

**ApiGateway.yaml** (specific for API Gateway):

```yaml
server:
  port: 9090
```

Final `ApiGateway` config after merging:

```yaml
server:
  port: 9090        # from ApiGateway.yaml (overrides)
management:
  endpoints:
    web:
      exposure:
        include: "*" # from application.yaml (inherited)
```


