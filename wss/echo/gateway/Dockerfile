FROM kaazing/enterprise-gateway:latest

# Generate Keystore entry for kaazing.example.com
RUN keytool -genkeypair -keystore conf/keystore.db -storetype JCEKS -keypass ab987c -storepass ab987c -alias kaazing.example.com -keyalg RSA -dname "CN=kaazing.example.com, OU=Example, O=Example, L=Mountain View, ST=California, C=US"

# Add and Build Javascript Client tutorials to web directory so we can test it from a browser,
# TODO pull in built tutorials when they are released

ENV NODE_VERSION 0.10.45

RUN curl -LOk  https://github.com/kaazing/javascript.client.tutorials/files/324472/websocket-echo-tutorial.zip \
    && unzip ./websocket-echo-tutorial.zip \
    && mkdir -p ./web/javascript.client.tutorials/ws \
    && cp -r ./websocket-echo-tutorial/* ./web/javascript.client.tutorials/ws/

# Add gateway config
COPY echo-wss-gateway-config.xml conf/gateway-config.xml
