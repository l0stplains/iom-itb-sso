FROM quay.io/keycloak/keycloak:25.0

# Bundle realm import and custom theme into the image so deployment does not depend on host bind mounts.
COPY realm-export.json /opt/keycloak/data/import/realm-export.json
COPY themes/iom-itb /opt/keycloak/themes/iom-itb
