Deploying this app on Openshift

```
oc new-build https://github.com/bbalakriz/hazelcast-embedded-sb.git --dockerfile='FROM maven:3.6.3-openjdk-11 as builder\nWORKDIR /project\nCOPY . /project/\nRUN mvn package -DskipTests -B\n\nFROM adoptopenjdk:11-jre-hotspot\nCOPY --from=builder /project/target/*.jar app.jar\nENTRYPOINT ["java","-jar","app.jar"]'

oc start-build hazelcast-embedded-sb --follow

oc apply -f https://raw.githubusercontent.com/bbalakriz/hazelcast-embedded-sb/master/deploy/deployment.yaml
```
