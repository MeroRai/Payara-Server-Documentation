# HealthCheck Service Asadmin Command Reference

The following is a detailed list of the administration commands that can be used to correctly configure the HealthCheck Service.

## `set-healthcheck-configuration` <a id="set-healthcheck-configuration"></a>

```text
set-healthcheck-configuration
 --enabled=true|false
 --dynamic=true|false
 --historic-trace-enabled=true|false
 --historic-trace-store-size=20
 --historic-trace-store-timeout=<integer.value>s|m|h|d
```

**Aim**

Enables and disables the HealthCheck service. This includes configuration for tracing historic health check events for later inspection.

### Command Options <a id="command-options-8"></a>

| Option | Type | Description | Default | Mandatory |
| :--- | :--- | :--- | :--- | :--- |
| `--target` | String | The instance or cluster that will enable or disable its service | server | no |
| `--dynamic` | Boolean | Whether to apply the changes directly to the server without a restart | false | no |
| `--enabled` | Boolean | Whether to enable or disable the service | N/A | yes |
| `--historic-trace-enabled` | Boolean | Enables historic checks if present | false | no |
| `--historic-trace-store-size` | Integer | Sets the maximum number of health checks to store | 20 | no |
| `--historic-trace-store-timeout` | String | Sets the time period after which a historic health check event entry is removed from visable history. The time expression should consist of a number followed by a time unit; `s` for seconds, `m` for minutes, `h` for hours or `d` for days. If no time unit is given the number specifies seconds. If the parameter is zero or unspecified there is no timeout for entries. | - | no |

|  | Enabling or disabling the health check service implicitly also enables or disables the log notifier which is the default notifier. This behaviour is similar to the replaced [`healthcheck-configure`](./) command. |
| :--- | :--- |


### Example <a id="example-8"></a>

The following example will enable the Healthcheck service such that it will only activate from the next time the server is restarted. It enables the log notifier and sets the historical trace store to retain 20 health checks.

```text
asadmin> set-healthcheck-configuration
    --enabled=true
    --dynamic=false
    --historic-trace-enabled=true
    --historic-trace-store-size=20
```

## `healthcheck-configure` <a id="healthcheck-configure"></a>

**Usage**

`asadmin> healthcheck-configure --enabled=true|false --dynamic=true|false --historicaltraceenabled --historicaltracestoresize=20`**Aim**

Enables and disables the HealthCheck service. Also allows configuration of the store of historical health checks.

### Command Options <a id="command-options"></a>

| Option | Type | Description | Default | Mandatory |
| :--- | :--- | :--- | :--- | :--- |
| `--target` | String | The instance or cluster that will enable or disable its service | server | no |
| `--dynamic` | Boolean | Whether to apply the changes directly to the server without a restart | false | no |
| `--enabled` | Boolean | Whether to enable or disable the service | N/A | yes |
| `--notifierenabled` | Boolean | Whether or not to enable the default notifier | false | no |
| `--historicaltraceenabled` | Boolean | Enables historic checks if present | false | no |
| `--historicaltracestoresize` | Integer | Sets the maximum number of health checks to store | 20 | no |

|  | Starting from release _4.1.1.171_, the `--notifierenabled` argument is used to enable or disable the **Log Notifier**, which is considered the _default_ notifier. Use the [`healthcheck-[NOTIFIER_NAME]-configure`](./) command to enable or disable other available notifiers. |
| :--- | :--- |


### Example <a id="example"></a>

The following example will enable the Healthcheck service such that it will only activate from the next time the server is restarted. It enables the log notifier and sets the historical trace store to retain 20 health checks.

```text
asadmin > healthcheck-configure
    --enabled=true
    --dynamic=false
    --notifierenabled=true
    --historicaltraceenabled=true
    --historicaltracestoresize=20
```

## `list-healthcheck-services` <a id="list-healthcheck-services"></a>

**Usage**

`asadmin> list-healthcheck-services`**Aim**

Lists the names of all available metric checker services.

### Command Options <a id="command-options-9"></a>

There are no options available.

### Example <a id="example-9"></a>

Running the command will show output similar to the example below:

```text
Available Health Check Services:
        healthcheck-cpool
        healthcheck-cpu
        healthcheck-gc
        healthcheck-heap
        healthcheck-threads
        healthcheck-machinemem

Command healthcheck-list-services executed successfully.
```

## `healthcheck-list-services` <a id="healthcheck-list-services"></a>

**Usage**

`asadmin> healthcheck-list-services`**Aim**

Lists the names of all available metric checker services.

### Command Options <a id="command-options-1"></a>

There are no options available.

### Example <a id="example-1"></a>

Running the command will show output similar to the example below:

```text
Available Health Check Services:
        healthcheck-cpool
        healthcheck-cpu
        healthcheck-gc
        healthcheck-heap
        healthcheck-threads
        healthcheck-machinemem

Command healthcheck-list-services executed successfully.
```

## `set-healthcheck-service-configuration` <a id="set-healthcheck-service-configuration"></a>

```text
set-healthcheck-service-configuration
 --service=<service.name>
 --enabled=true|false
 --dynamic=true|false
 --time=<integer.value>
 --time-unit=DAYS|HOURS|MINUTES|SECONDS|MILLISECONDS
 --threshold-critical=80
 --threshold-warning=50
 --threshold-good=0
 --hogging-threads-threshold=<integer.value>
 --hogging-threads-retry-count=<integer.value>
 --stuck-threads-threshold=<integer.value>
 --stuck-threads-threshold-unit=DAYS|HOURS|MINUTES|SECONDS|MILLISECONDS
```

**Aim**

Enables or disables the monitoring of an specific metric. The command also configures the frequency of monitoring for that metric. Furthermore it configures metric specific properties.

### Command Options <a id="command-options-10"></a>

| Option | Type | Description | Default | Mandatory |
| :--- | :--- | :--- | :--- | :--- |


| `--target` | String | The instance or cluster that will enable or disable its metric configuration | server | no |
| :--- | :--- | :--- | :--- | :--- |


| `--dynamic` | Boolean | Whether to apply the changes directly to the server/instance without a restart | false | no |
| :--- | :--- | :--- | :--- | :--- |


| `--enabled` | Boolean | Whether to enable or disable the metric monitoring | N/A | yes |
| :--- | :--- | :--- | :--- | :--- |


<table>
  <thead>
    <tr>
      <th style="text-align:left"><code>--service</code>
      </th>
      <th style="text-align:left">String</th>
      <th style="text-align:left">
        <p>The service metric name. One of:</p>
        <ul>
          <li><code>connection-pool</code> or <code>cp</code>
          </li>
          <li><code>cpu-usage</code> or <code>cu</code>
          </li>
          <li><code>garbage-collector</code> or <code>gc</code>
          </li>
          <li><code>heap-memory-usage</code> or <code>hmu</code>
          </li>
          <li><code>hogging-threads</code> or <code>ht</code>
          </li>
          <li><code>machine-memory-usage</code> or <code>mmu</code>
          </li>
          <li><code>stuck-thread</code> or <code>st</code>
          </li>
          <li><code>mp-health</code> or <code>mh</code>
          </li>
        </ul>
      </th>
      <th style="text-align:left">-</th>
      <th style="text-align:left">yes</th>
    </tr>
  </thead>
  <tbody></tbody>
</table>| `--time` | Integer | The amount of time units that the service will use to periodically monitor the metric | 5 | no |
| :--- | :--- | :--- | :--- | :--- |


| `--time-unit` | TimeUnit | The time unit to set the frequency of the metric monitoring. Must correspond to a valid [`java.util.concurrent.TimeUnit`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/TimeUnit.html) value | `MINUTES` | no |
| :--- | :--- | :--- | :--- | :--- |


| `--threshold-critical` | Integer | The threshold value that this metric must surpass to generate a **`CRITICAL`** event. A value between _WARNING VALUE_ and _100_ must be used. Available for services `cp`, `cu`, `gc`, `hmu` and `mmu`. | 90 | no |
| :--- | :--- | :--- | :--- | :--- |


| `--threshold-warning` | Integer | The threshold value that this metric must surpass to generate a **`WARNING`** event. A value between _GOOD VALUE_ and _CRITICAL VALUE_ must be used. Available for services `cp`, `cu`, `gc`, `hmu` and `mmu`. | 50 | no |
| :--- | :--- | :--- | :--- | :--- |


| `--threshold-good` | Integer | The threshold value that this metric must surpass to generate a **`GOOD`** event. A value between _0_ and _WARNING VALUE_ must be used. Available for services `cp`, `cu`, `gc`, `hmu` and `mmu`. | 0 | no |
| :--- | :--- | :--- | :--- | :--- |


| `--hogging-threads-threshold` | Integer | The threshold value that this metric will be compared to mark threads as hogging the CPU. Only available for `ht` service. | 95 | no |
| :--- | :--- | :--- | :--- | :--- |


| `--hogging-threads-retry-count` | Integer | The number of retries that the checker service will execute in order to identify a hogging thread. Only available for `ht` service. | 3 | no |
| :--- | :--- | :--- | :--- | :--- |


| `--stuck-threads-threshold` | Integer | The threshold above which a thread is considered stuck. Must be 1 or greater. Only available for `st` service. | - | no |
| :--- | :--- | :--- | :--- | :--- |


| `--stuck-threads-threshold-unit` | [`TimeUnit`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/TimeUnit.html) | The unit for the threshold for when a thread should be considered stuck. Only available for `st` service. | - | no |
| :--- | :--- | :--- | :--- | :--- |


### Examples <a id="example-10"></a>

A very basic example command to simply enable the GC checker and activate it without needing a restart would be as follows:

```text
asadmin> set-healthcheck-service-configuration
 --enabled=true
 --service=gc
 --dynamic=true
```

Monitoring the health of JDBC connection pools is a common need. In that scenario, it is very unlikely that on-the-fly configuration changes would be made, so a very high `CRITICAL` threshold can be set. Likewise, a nonzero `GOOD` threshold is needed because an empty or unused connection pool may not be healthy either.

The following command would apply these settings to the connection pool checker:

```text
asadmin> set-healthcheck-service-configuration
 --service=cp
 --dynamic=true
 --threshold-critical=95
 --threshold-warning=70
 --threshold-good=30
```

Monitoring which threads hog the CPU is extremely important since this can lead to performance degradation, deadlocks and extreme bottlenecks issues that web applications can incur. In some cases the defaults are all that is needed, but imagine that in a critical system you want to set the threshold percentage to **90%**, and you want to make sure that the health check service guarantees the state of such threads with a retry count of **5**. Additionally, you want to set the frequency of this check for every _20 seconds_.

The following command would apply these settings to the connection pool checker:

```text
asadmin> set-healthcheck-service-configuration
 --service=cp
 --dynamic=true
 --hogging-threads-threshold=90
 --hogging-threads-retry-count=5
 --time=20
 --time-unit=SECONDS
```

The following example configures the stuck threads checker to check every 30 seconds for any threads which have been stuck for more than 5 minutes and applies the configuration change without needing a restart:

```text
asadmin> set-healthcheck-service-configuration
 --service=stuck-thread
 --enabled=true
 --dynamic=true
 --time=30
 --time-unit=SECONDS
 --stuck-threads-threshold=5
 --stuck-threads-threshold-unit=MINUTES
```

## `healthcheck-configure-service` <a id="healthcheck-configure-service"></a>

**Usage**

`asadmin> healthcheck-configure-service --serviceName=<service.name> --checkerName=<name> --enabled=true|false --dynamic=true|false --time=<integer.value> --unit=MICROSECONDS|MILLISECONDS|SECONDS|MINUTES|HOURS|DAYS`**Aim**

Enables or disables the monitoring of an specific checker. The command also configures the frequency of monitoring for that metric.

### Command Options <a id="command-options-2"></a>

| Option | Type | Description | Default | Mandatory |
| :--- | :--- | :--- | :--- | :--- |


| `--target` | String | The instance or cluster that will enable or disable its metric configuration | server | no |
| :--- | :--- | :--- | :--- | :--- |


| `--dynamic` | Boolean | Whether to apply the changes directly to the server/instance without a restart | false | no |
| :--- | :--- | :--- | :--- | :--- |


| `--enabled` | Boolean | Whether to enable or disable the metric monitoring | N/A | yes |
| :--- | :--- | :--- | :--- | :--- |


| `--serviceName` | String | The metric service name. Must correspond to one of the values listed before | - | yes |
| :--- | :--- | :--- | :--- | :--- |


<table>
  <thead>
    <tr>
      <th style="text-align:left"><code>--checkerName</code>
      </th>
      <th style="text-align:left">String</th>
      <th style="text-align:left">A user determined name for easy identification of the checker. This should
        be unique among the services you have configured, to avoid confusion on
        the notification messages.</th>
      <th style="text-align:left">
        <p>Depends on the service checker. One of:</p>
        <ul>
          <li><code>CONP</code>
          </li>
          <li><code>CPUC</code>
          </li>
          <li><code>GBGC</code>
          </li>
          <li><code>HEAP</code>
          </li>
          <li><code>HOGT</code>
          </li>
          <li><code>MEMM</code>
          </li>
        </ul>
      </th>
      <th style="text-align:left">no</th>
    </tr>
  </thead>
  <tbody></tbody>
</table>| `--time` | Integer | The amount of time units that the service will use to periodically monitor the metric | 5 | no |
| :--- | :--- | :--- | :--- | :--- |


| `--unit` | TimeUnit | The time unit to set the frequency of the metric monitoring. Must correspond to a valid [`java.util.concurrent.TimeUnit`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/TimeUnit.html) value | `MINUTES` | no |
| :--- | :--- | :--- | :--- | :--- |


### Example <a id="example-2"></a>

A very basic example command to simply enable the GC checker and activate it without needing a restart would be as follows:

```text
asadmin> healthcheck-configure-service --enabled=true
      --serviceName=healthcheck-gc
      --name=MYAPP-GC
      --dynamic=true
```

## `healthcheck-configure-service-threshold` <a id="healthcheck-configure-service-threshold"></a>

**Usage**

`asadmin> healthcheck-configure-service-threshold --serviceName=<service.name> --dynamic=true|false --thresholdCritical=90 --thresholdWarning=50 --thresholdGood=0`**Aim**

Configures `CRITICAL`, `WARNING` and `GOOD` threshold range values for a service checker. The `dynamic` attribute should be set to `true` in order to apply the changes directly.

This command only configures thresholds for the following checkers:

* CPU Usage
* Connection Pool
* Heap Memory Usage
* Machine Memory Usage

### Command Options <a id="command-options-3"></a>

| Option | Type | Description | Default | Mandatory |
| :--- | :--- | :--- | :--- | :--- |
| `--target` | String | The instance or cluster that will be configured | server | no |
| `--dynamic` | Boolean | Whether to apply the changes directly to the server/instance without a restart | false | no |
| `--serviceName` | String | The metric service name. Must correspond to one of the values listed before | - | yes |
| `--thresholdCritical` | Integer | The threshold value that this metric must surpass to generate a **`CRITICAL`** event. A value between _WARNING VALUE_ and _100_ must be used | 90 | no |
| `--thresholdWarning` | Integer | The threshold value that this metric must surpass to generate a **`WARNING`** event. A value between _GOOD VALUE_ and _CRITICAL VALUE_ must be used | 50 | no |
| `--thresholdGood` | Integer | The threshold value that this metric must surpass to generate a **`GOOD`** event. A value between _0_ and _WARNING VALUE_ must be used | 0 | no |

|  | In order to execute this command for an specific metric, the `healthcheck-configure-service` command needs to be executed first. |
| :--- | :--- |


### Example <a id="example-3"></a>

Monitoring the health of JDBC connection pools is a common need. In that scenario, it is very unlikely that on-the-fly configuration changes would be made, so a very high `CRITICAL` threshold can be set. Likewise, a nonzero `GOOD` threshold is needed because an empty or unused connection pool may not be healthy either.

The following command would apply these settings to the connection pool checker:

```text
asadmin> healthcheck-configure-service-threshold
 --serviceName=healthcheck-cpool
 --dynamic=true
 --thresholdCritical=95
 --thresholdWarning=70
 --thresholdGood=30
```

## `healthcheck-hoggingthreads-configure` <a id="healthcheck-hoggingthreads-configure"></a>

**Usage**

`asadmin> healthcheck-hoggingthreads-configure --dynamic=true|false --threshold-percentage=50 --retry-count=3`**Aim**

Configures the **Hogging Threads** checker service settings. The checker will determine which running threads are hogging the CPU by calculating a percentage of usage with the ratio of elapsed time to the checker service execution interval and verifying if this percentage exceeds the `threshold-percentage`.

You can also use this command to enable the checker and configure the monitoring frequency as you would do with the `healthcheck-configure-service` command.

### Command Options <a id="command-options-4"></a>

| Option | Type | Description | Default | Mandatory |
| :--- | :--- | :--- | :--- | :--- |
| `--target` | String | The instance or cluster that will be configured | server | no |
| `--enabled` | Boolean | Whether to enable or disable the checker | true | no |
| `--dynamic` | Boolean | Whether to apply the changes directly to the server/instance without a restart | false | no |
| `--threshold-percentage` | Integer | The threshold value that this metric will be compared to mark threads as hogging the CPU | 95 | no |
| `--retry-count` | Integer | The number of retries that the checker service will execute in order to identify a hogging thread | 3 | no |
| `--time` | Integer | The periodic amount of time units the checker service will use to monitor hogging threads | 1 | no |
| `--unit` | TimeUnit | The time unit to set the frequency of the metric monitoring. Must correspond to a valid [`java.util.concurrent.TimeUnit`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/TimeUnit.html) value | `SECONDS` | no |

### Example <a id="example-4"></a>

Monitoring which threads hog the CPU is extremely important since this can lead to performance degradation, deadlocks and extreme bottlenecks issues that web applications can incur. In some cases the defaults are all that is needed, but imagine that in a critical system you want to set the threshold percentage to **90%**, and you want to make sure that the health check service guarantees the state of such threads with a retry count of **5**. Additionally, you want to set the frequency of this check for every _20 seconds_.

The following command would apply these settings to the connection pool checker:

```text
asadmin> healthcheck-hoggingthreads-configure
 --dynamic=true
 --threshold-percentage=90
 --retry-count=5
 --time=20
 --unit=SECONDS
```

## `healthcheck-stuckthreads-configure` <a id="healthcheck-stuckthreads-configure"></a>

**Usage**

`asadmin> healthcheck-stuckthreads-configure --enabled true|false --dynamic true|false --time=<integer.value> --unit=MICROSECONDS|MILLISECONDS|SECONDS|MINUTES|HOURS|DAYS --threshold=<integer.value> --thresholdUnit=MICROSECONDS|MILLISECONDS|SECONDS|MINUTES|HOURS|DAYS`**Aim**

Configures the Stuck Thread checker. The Stuck Threads checker is comparable to the request tracing service, in that it is triggered by exceeding a configured threshold. but in this case it reports on all threads that, when the healthcheck runs, have taken longer than the threshold time.

### Command Options <a id="command-options-5"></a>

| Option | Type | Description | Default | Mandatory |
| :--- | :--- | :--- | :--- | :--- |
| `--enabled` | Boolean | Enables or disables the checker | - | yes |
| `--dynamic` | Boolean | Whether or not to apply the changes dynamically \(without a restart\) | false | no |
| `--time` | Integer | The time between checks, must be 1 or greater | - | no |
| `--unit` | [`TimeUnit`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/TimeUnit.html) | The unit for the time between healthchecks | - | no |
| `--threshold` | Integer | The threshold above which a thread is considered stuck. Must be 1 or greater. | - | no |
| `--thresholdUnit` | [`TimeUnit`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/TimeUnit.html) | The unit for the threshold for when a thread should be considered stuck | - | no |
| `--target` | String | The target to enable the checker on | `server` \(the DAS\) | no |

### Example <a id="example-5"></a>

The following example configures the stuckthreads checker to check every 30 seconds for any threads which have been stuck for more than 5 minutes and applies the configuration change without needing a restart:

```text
asadmin> healthcheck-stuckthreads-configure
    --enabled=true
    --dynamic=true
    --time=30
    --unit=SECONDS
    --threshold=5
    --thresholdUnit=MINUTES
```

## `set-healthcheck-service-notifier-configuration` <a id="set-healthcheck-service-notifier-configuration"></a>

```text
asadmin> set-healthcheck-service-notifier-configuration
 --notifier=<string.value>
 --enabled=true|false
 --dynamic=true|false
 --noisy=true|false
```

**Aim**

This command can be used to enable or disable a specific notifier or to change its noisy setting.

### Command Options <a id="command-options-14"></a>

| Option | Type | Description | Default | Mandatory |
| :--- | :--- | :--- | :--- | :--- |


<table>
  <thead>
    <tr>
      <th style="text-align:left"><code>--notifier</code>
      </th>
      <th style="text-align:left">String</th>
      <th style="text-align:left">
        <p>The notifier to configure. One of (case insensitive):</p>
        <ul>
          <li><code>LOG</code>
          </li>
          <li><code>HIPCHAT</code>
          </li>
          <li><code>SLACK</code>
          </li>
          <li><code>JMS</code>
          </li>
          <li><code>EMAIL</code>
          </li>
          <li><code>XMPP</code>
          </li>
          <li><code>SNMP</code>
          </li>
          <li><code>EVENTBUS</code>
          </li>
          <li><code>NEWRELIC</code>
          </li>
          <li><code>DATADOG</code>
          </li>
          <li><code>CDIEVENTBUS</code>
          </li>
        </ul>
      </th>
      <th style="text-align:left">-</th>
      <th style="text-align:left">yes</th>
    </tr>
  </thead>
  <tbody></tbody>
</table>| `--enable` | Boolean | Enables or disables the notifier | false | Yes |
| :--- | :--- | :--- | :--- | :--- |


| `--noisy` | Boolean | Sets the notifier to noisy \(a.k.a verbose\) or not noisy. A noisy notifier includes more detailed logging information in the notifiers output. | - | No |
| :--- | :--- | :--- | :--- | :--- |


| `--dynamic` | Boolean | Whether to apply the changes directly to the server/instance without a restart | false | No |
| :--- | :--- | :--- | :--- | :--- |


| `--target` | String | The instance or cluster that will be configured | server | no |
| :--- | :--- | :--- | :--- | :--- |


To enable the log notifier for the HealthCheck Service without having to restart the server, use the following command:

```text
asadmin> set-healthcheck-service-notifier-configuration
 --notifier=log
 --enabled=true
 --dynamic=true
```

## `healthcheck-[NOTIFIER_NAME]-notifier-configure` <a id="healthcheck-notifier-configure"></a>

**Usage**

`asadmin> healthcheck-[NOTIFIER_NAME]-notifier-configure --enabled=true --dynamic=true`**Aim**

This command can be used to enable or disable the notifier represented by the _\[NOTIFIER\_NAME\]_ placeholder.

### Command Options <a id="command-options-6"></a>

| Option | Type | Description | Default | Mandatory |
| :--- | :--- | :--- | :--- | :--- |
| `--enable` | Boolean | Enables or disables the notifier | false | Yes |
| `--dynamic` | Boolean | Whether to apply the changes directly to the server/instance without a restart | false | No |

### Examples <a id="example-6"></a>

1. To enable the log notifier for the HealthCheck Service without having to restart the server, use the following command:

   ```text
   asadmin> healthcheck-log-notifier-configure
       --enabled=true
       --dynamic=true
   ```

2. To disable the [Hipchat notifier](https://github.com/MeroRai/Payara-Server-Documentation/tree/fbbb48a6e9e16131de3abd180b96158a6cf7a2ad/documentation/payara-server/notification-service/notifiers/hipchat-notifier.adoc) without having to restart the server, use the following command:

   ```text
   asadmin> healthcheck-hipchat-notifier-configure
       --enabled=false
       --dynamic=true
   ```

## `get-healthcheck-configuration` <a id="get-healthcheck-configuration"></a>

**Usage**

`asadmin> get-healthcheck-configuration`**Aim**

Lists the current configuration for the health check service, configured checkers and enabled notifiers.

### Command Options <a id="command-options-7"></a>

There are no options available.

### Example <a id="example-7"></a>

A sample output is as follows:

```text
Health Check Service Configuration is enabled?: true
Historical Tracing Enabled?: false
Name      Notifier Enabled
XMPP      false
DATADOG   true
EMAIL     false
SLACK     true
EVENTBUS  false
HIPCHAT   false
NEWRELIC  true
SNMP      false
LOG       true
JMS       false

Below are the list of configuration details of each checker listed by its name.

Name  Enabled  Time  Unit
GBGC  true     2     MINUTES

Name  Enabled  Time  Unit     Threshold Percentage  Retry Count
HOGT  true     5     MINUTES  78                    5

Name  Enabled  Time  Unit     Critical Threshold  Warning Threshold  Good Threshold
CPUC  true     30    SECONDS  80                  50                 0
HEAP  true     1     MINUTES  80                  50                 0

Command get-healthcheck-configuration executed successfully.
```

