# OLA Java client

EXTRA_DIST = pom.xml \
             src/main/java/ola/OlaClient.java \
             src/main/java/ola/rpc/SimpleRpcController.java \
             src/main/java/ola/rpc/StreamRpcChannel.java \
             src/test/java/ola/OlaClientTest.java

src/main/java/ola/proto/Ola.java: ${top_srcdir}/common/protocol/Ola.proto
	$(PROTOC) --java_out=src/main/java --proto_path=${top_srcdir}/common/protocol ${top_srcdir}/common/protocol/Ola.proto

src/main/java/ola/rpc/Rpc.java: ${top_srcdir}/common/rpc/Rpc.proto
	$(PROTOC) --java_out=src/main/java --proto_path=${top_srcdir}/common/rpc ${top_srcdir}/common/rpc/Rpc.proto

ola.jar: generated-src/main/java/ola/proto/Ola.java generated-src/main/java/ola/rpc/Rpc.java
	cd ${top_builddir}/java && mvn --file ${top_srcdir}/java/pom.xml -DbuildDir=${abs_top_builddir}/java -DprotobufGeneratedSource=$(abs_top_builddir)/java/generated-src/main/java -DprotobufJavaVersion=$(PROTOBUF_VERSION) package

CLEANFILES = src/main/java/ola/proto/Ola.java \
             src/main/java/ola/rpc/Rpc.java

if BUILD_JAVA_LIBS
# .jars aren't really data, but it sure ain't a program.
noinst_DATA = ola.jar
endif
