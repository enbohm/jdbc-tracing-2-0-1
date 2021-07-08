# jdbc-tracing-2-0-1

Using Quarkus 2.0.1.Final with OpenTracing-JDBC fails with the following stacktrace. Downgrading to 2.0.0.Final everything works.

1) Start the Oracle DB container
```
   docker run -d -p 49161:1521 oracleinanutshell/oracle-xe-11g
```
   
2) Start the application
```shell script
./mvnw compile quarkus:dev
```
3) Open http://127.0.0.1:8080/q/health

The resulting stacktrace

```
SRHCK01000: Error processing Health Checks: java.lang.NoClassDefFoundError: Could not initialize class oracle.net.nt.Clock
at oracle.net.nt.NetStatImpl.incrementBytesSent(NetStatImpl.java:80)
at oracle.net.nt.TimeoutSocketChannel.write(TimeoutSocketChannel.java:468)
at oracle.net.ns.NIOPacket.writeToSocketChannel(NIOPacket.java:361)
at oracle.net.ns.NIOConnectPacket.writeToSocketChannel(NIOConnectPacket.java:255)
at oracle.net.ns.NSProtocolNIO.negotiateConnection(NSProtocolNIO.java:157)
at oracle.net.ns.NSProtocol.connect(NSProtocol.java:350)
at oracle.jdbc.driver.T4CConnection.connect(T4CConnection.java:1967)
at oracle.jdbc.driver.T4CConnection.logon(T4CConnection.java:640)
at oracle.jdbc.driver.PhysicalConnection.connect(PhysicalConnection.java:1032)
at oracle.jdbc.driver.T4CDriverExtension.getConnection(T4CDriverExtension.java:90)
at oracle.jdbc.driver.OracleDriver.connect(OracleDriver.java:681)
at oracle.jdbc.driver.OracleDriver.connect(OracleDriver.java:602)
at io.agroal.pool.ConnectionFactory.createConnection(ConnectionFactory.java:204)
at io.agroal.pool.ConnectionPool$CreateConnectionTask.call(ConnectionPool.java:490)
at io.agroal.pool.ConnectionPool$CreateConnectionTask.call(ConnectionPool.java:472)
at java.base/java.util.concurrent.FutureTask.run(FutureTask.java:264)
at io.agroal.pool.util.PriorityScheduledExecutor.beforeExecute(PriorityScheduledExecutor.java:68)
at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1126)
at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
at java.base/java.lang.Thread.run(Thread.java:834)
```


 
 
