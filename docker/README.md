# Dockerised - openapi-json-response-validator

Expose the `openapi-json-response-validator` in Docker.

See below for an example of how to expose the validator in docker

```yaml
version: '3'

services:

  validation-status:
    container_name: validation-status
    image: croweman/openapi-json-response-validator:0.0.8
    command: sh -c "sh wait-for-it.sh http://app:3010/readiness && echo 'We can now validate!'"
    volumes:
      - ./wait-for-it.sh:/app/wait-for-it.sh
  
  app:
    container_name: openapi-json-response-validator
    image: croweman/openapi-json-response-validator:0.0.8
    restart: "on-failure:10"
    volumes:
      - ./api.yaml:/app/api.yaml
    ports:
      - "3010:3010"
    environment:
      OPENAPI_JSON_RESPONSE_VALIDATOR_PORT: 3010
```

