FROM kaazing/enterprise-gateway:latest

# Generate Keystore entry for kaazing.example.com
RUN keytool -genkeypair -keystore conf/keystore.db -storetype JCEKS -keypass ab987c -storepass ab987c -alias kaazing.example.com -keyalg RSA -dname "CN=kaazing.example.com, OU=Example, O=Example, L=Mountain View, ST=California, C=US"

# Add and Build Javascript Client tutorials to web directory so we can test it from a browser,
# TODO pull in built tutorials when they are released

ENV NODE_VERSION 0.10.45

RUN curl -LOk https://github.com/kaazing/javascript.client.tutorials/files/324464/websocket-jms-tutorial.zip \
    && unzip ./websocket-jms-tutorial.zip \
    && mkdir -p ./web/javascript.client.tutorials/jms \
    && cp -r ./websocket-jms-tutorial/* ./web/javascript.client.tutorials/jms/

# Add broker specific client libs
ADD http://central.maven.org/maven2/org/apache/activemq/activemq-client/5.14.1/activemq-client-5.14.1.jar lib/ext/

ADD http://central.maven.org/maven2/org/apache/geronimo/specs/geronimo-jms_1.1_spec/1.1/geronimo-jms_1.1_spec-1.1.jar lib/ext/
ADD http://central.maven.org/maven2/org/apache/geronimo/specs/geronimo-j2ee-management_1.1_spec/1.0.1/geronimo-j2ee-management_1.1_spec-1.0.1.jar lib/ext/

ADD http://central.maven.org/maven2/org/apache/geronimo/specs/geronimo-jta_1.1_spec/1.1/geronimo-jta_1.1_spec-1.1.jar lib/ext/
ADD http://central.maven.org/maven2/org/fusesource/hawtbuf/hawtbuf/1.10/hawtbuf-1.10.jar lib/ext/

# Add gateway config
COPY jms-activemq-gateway-config.xml conf/gateway-config.xml
