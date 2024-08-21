spring:
  security:
    oauth2:
      client:
        provider:
          # OAuth2 provider configuration
          webclient:
            token-uri: https://api-ce.kroger.com/v1/connect/oauth2/token

        registration:
          # OAuth2 client registration details
          webclient:
            client-id: ${CORE_SERVICE_CLIENT_ID}
            client-secret: ${CORE_SERVICE_CLIENT_SECRET}
            authorization-grant-type: client_credentials
            scope:
              - urn:com:kroger:kr:sfp-domain:read
              - urn:com:kroger:kr:sfp-domain:write

      resourceserver:
        sfp:
          # Resource server and JWK configuration
          token-uri: https://api-ce.kroger.com/v1/connect/oauth2/token
          sfp-endpoint-uri: https://api-ce.kroger.com/v1/.well-known/jwks.json

application:
  # Application metadata
  name: SFP-Experience-service
  version: 1.0.e
  base_url: https://localhost:8080/

r2dbc:
  # R2DBC (Reactive Relational Database Connectivity) configuration
  url: ${SPRING_R2DBC_URL}
  username: ${SPRING_R2DBC_USERNAME}
  password: ${SPRING_R2DBC_PASSWORD}

  pool:
    # Connection pool settings
    enabled: true
    initial-size: 5
    max-size: 20
    max-create-connection-time: PT30S  # 30 seconds
    max-idle-time: PT15M  # 15 minutes

  # Validation query
  validation-query: SELECT 1
  mode: verify-full
  #root cert: path/to/server/certificate  # Optional root certificate configuration

kroger:
  echo:
    # Kroger Echo service routing and server URL
    routing-key: sfp-core-experience-platform-stage
    server-url: echocollector-stage.kroger.com

swagger:
  service:
    # Swagger service information
    title: SFP Core Experience 300
    description: Space and Floor service endpoints.
    devUrl: https://localhost:8080/
    stageUrl: https://localhost:8080/
    prodUrl: https://localhost:8080/

  contact:
    # Swagger contact information
    name: SFP Core Experience 300
    url: https://confluence.kroger.com/confluence/display/SPT/SFP+Core+Experience+300

domain-service:
  # Domain service scopes
  read: urn:com:kroger:kr:sfp-domain:read
  write: urn:com:kroger:kr:sfp-domain:write

timeout:
  # Timeout settings
  sfp-core-validation: 2000  # Timeout for core validation in milliseconds
  sfp-core-connect-validation: 2000  # Timeout for core connection validation in milliseconds

by:
  apis:
    baseUrl: https://n06@jdafs43.kroger.com:44350

    EkbPlanograms:
      # Planograms API endpoints
      hierarchyNodes: /ckb-planograms/v2/hierarchyNodes
      planograms: /ckb-planograms/v2/planograms
      projects: /ckb-planograms/v2/projects

    ckbFloorplans:
      # Floorplans API endpoints
      hierarchyNodes: /ckb-floorplans/v2/hierarchyNodes
      floorplans: /ckb-floorplans/v2/floorplans

# Token placeholder
token: ${TOKEN}
