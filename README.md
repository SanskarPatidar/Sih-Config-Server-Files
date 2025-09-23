## How It Works: Property Precedence
Spring Boot applies configuration in a specific order, creating layers of properties. When the same property is defined in multiple places, the one with the higher precedence (the one applied later) wins.

Here's the simplified order of precedence for your scenario, from highest to lowest:

Local Profile Properties (application-local.yml): These are the most specific and will override everything below them.

Local Application Properties (application.yml): The base local configuration.

Remote Properties from Config Server: These act as the default values for your application. They have the lowest priority and can be easily overridden locally.
