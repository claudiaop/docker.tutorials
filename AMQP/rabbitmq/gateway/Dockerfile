FROM kaazing/development-enterprise-gateway:5.6.2-RC001

# Generate Keystore entry for kaazing.example.com
RUN keytool -genkeypair -keystore conf/keystore.db -storetype JCEKS -keypass ab987c -storepass ab987c -alias kaazing.example.com -keyalg RSA -dname "CN=kaazing.example.com, OU=Example, O=Example, L=Mountain View, ST=California, C=US"

# Add and Build Javascript Client tutorials to web directory so we can test it from a browser,
# TODO pull in built tutorials when they are released


ENV NODE_VERSION 0.10.45

RUN curl -LOk  https://github.com/kaazing/javascript.client.tutorials/files/324463/websocket-amqp-tutorial.zip \
    && unzip ./websocket-amqp-tutorial.zip \
    && mkdir -p ./web/javascript.client.tutorials/amqp \
    && cp -r ./websocket-amqp-tutorial/* ./web/javascript.client.tutorials/amqp/

# Add rabbitmq client libs
ADD https://github.com/rabbitmq/rabbitmq-server/releases/download/rabbitmq_v3_6_2/rabbitmq-java-client-bin-3.6.2.tar.gz lib/ext/

# Add gateway config
COPY amqp-rabbitmq-gateway-config.xml conf/gateway-config.xml
