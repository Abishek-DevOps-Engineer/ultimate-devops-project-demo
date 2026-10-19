#base image with jdk
FROM eclipse-temurin:21-jdk AS builder

WORKDIR /usr/src/app

COPY gradlew* settings.gradle build.gradle .

COPY ./gradle ./gradle

RUN chmod +x gradlew

COPY . .

COPY ./pb ./proto

RUN ./gradlew installDist -PprotoSourceDir=./proto

#####################################################
#image only has jre
FROM eclipse-temurin:21-jre

WORKDIR /usr/src/app

COPY --from=builder /usr/src/app/ .

ENV AD_PORT=9090

ENTRYPOINT ["./build/install/opentelemetry-demo-ad/bin/Ad"]
