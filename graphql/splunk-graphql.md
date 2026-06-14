# Splunk GraphQL Schema

Conceptual GraphQL schema for the Splunk platform, covering search, indexing, data inputs, access control, dashboards, saved searches, metrics, clustering, licensing, and diagnostics.

## Source APIs

- [Splunk Enterprise REST API](https://docs.splunk.com/Documentation/Splunk/latest/RESTREF/RESTprolog)
- [Splunk Developer Portal](https://dev.splunk.com/enterprise/docs/devtools/restapi/)
- [Splunk Cloud Platform REST API](https://help.splunk.com/en/splunk-cloud-platform/rest-api-reference)
- [Splunk Observability Cloud API](https://dev.splunk.com/observability/)
- [Splunk HTTP Event Collector (HEC) API](https://docs.splunk.com/Documentation/Splunk/latest/Data/UsetheHTTPEventCollector)
- [GitHub: splunk](https://github.com/splunk)

## Schema File

[splunk-schema.graphql](splunk-schema.graphql)

## Types

### Search

| Type | Description |
|---|---|
| `SearchJob` | A dispatched SPL search job with status, counts, and metadata |
| `SearchJobStatus` | Enum of job lifecycle states: QUEUED, PARSING, RUNNING, PAUSED, FINALIZING, FAILED, DONE |
| `SearchMessage` | Informational or error message returned alongside search results |
| `SearchResults` | Paginated result set with field definitions and row data |
| `SearchField` | Column descriptor returned within a result set |
| `SearchPreview` | Partial results available before a job completes |
| `SearchTimeline` | Bucket-based time distribution of events for a search job |
| `TimelineBucket` | A single time slice within a search timeline |

### Indexes and Metadata

| Type | Description |
|---|---|
| `Index` | A Splunk event or metric index with storage configuration and statistics |
| `IndexDatatype` | Enum: EVENT or METRIC |
| `IndexSummary` | Aggregated statistics for an index across hosts, sources, and sourcetypes |
| `HostSummary` | Event count and recency for a specific host field value |
| `SourcetypeSummary` | Event count and recency for a specific sourcetype |
| `SourceSummary` | Event count and recency for a specific source |
| `Sourcetype` | Source type definition controlling parsing and line breaking |
| `Source` | A data source observed in the index |
| `Host` | A host dimension observed in the index |

### Apps

| Type | Description |
|---|---|
| `App` | A Splunk application package with metadata and state |
| `AppConfig` | A key-value configuration entry scoped to an app |

### Users and Access Control

| Type | Description |
|---|---|
| `User` | A Splunk user account with roles and capabilities |
| `Role` | A named collection of capabilities and index access controls |
| `Permission` | Read/write access grant on a specific Splunk resource |
| `Capability` | An atomic permission token such as `search` or `admin_all_objects` |

### KV Store

| Type | Description |
|---|---|
| `KVStore` | A KV store collection definition with field schema |
| `KVStoreData` | A single document record within a KV store collection |

### Dashboards and Views

| Type | Description |
|---|---|
| `Dashboard` | A Splunk dashboard with panels and view state |
| `DashboardPanel` | An individual visualization panel within a dashboard |
| `ViewState` | Persisted UI state for a dashboard or view |

### Saved Searches and Alerts

| Type | Description |
|---|---|
| `SavedSearch` | A named, optionally scheduled SPL search |
| `Alert` | An alert triggered by a saved search threshold condition |
| `AlertSeverity` | Enum: INFO, WARNING, ERROR, CRITICAL |
| `AlertSuppression` | Rule to suppress repeated alert firings for a period |

### Data Models

| Type | Description |
|---|---|
| `Datamodel` | A structured data model built over indexed data |
| `DatamodelObject` | A node within a data model hierarchy |
| `DatamodelConstraint` | An SPL constraint scoped to a data model object |
| `DatamodelField` | A field definition within a data model object |
| `DatamodelAcceleration` | Acceleration configuration and status for a data model |

### Lookups and Transforms

| Type | Description |
|---|---|
| `Lookup` | A lookup table definition mapping input fields to output fields |
| `LookupTable` | The header and row data of a CSV or KV lookup table |
| `Transforms` | A transforms.conf stanza (lookup, extraction, alias, or metric schema) |
| `TransformType` | Enum: LOOKUP, EXTRACTION, ALIAS, METRIC_SCHEMA |
| `FieldExtraction` | A field extraction regex or delimited extraction definition |
| `FieldAlias` | A field alias mapping alternative field names |

### Macros and Event Types

| Type | Description |
|---|---|
| `MacroDefinition` | A reusable SPL search macro with optional arguments |
| `EventType` | A named search that categorizes events with tags |
| `Tag` | A metadata tag applied to field-value pairs |
| `TagObject` | A field-value pair that a tag applies to |

### Tokens

| Type | Description |
|---|---|
| `Token` | A Splunk authentication token with expiration and claims |

### Metrics

| Type | Description |
|---|---|
| `MetricIndex` | A metric-type index with dimension and metric name inventory |
| `MetricTimeseries` | A time series of metric measurements filtered by dimensions |
| `MetricPoint` | A single timestamp-value pair in a metric time series |

### Workflow Actions

| Type | Description |
|---|---|
| `WorkflowAction` | A context menu action triggered from event fields |
| `WorkflowActionType` | Enum: LINK or SEARCH |

### FTS Configuration

| Type | Description |
|---|---|
| `FTSConfig` | Full-text search configuration for an index |

### Clustering

| Type | Description |
|---|---|
| `ClusterConfig` | Index cluster configuration including replication and search factors |
| `ClusterMode` | Enum: MASTER, PEER, SEARCHHEAD, DISABLED |
| `ClusterNode` | An individual peer node in an index cluster |
| `ClusterNodeStatus` | Enum: UP, DOWN, DECOMMISSIONING |
| `ClusterBundle` | A configuration bundle distributed to cluster peers |
| `ClusterBucket` | A data bucket stored on a cluster peer |

### HEC

| Type | Description |
|---|---|
| `HECToken` | An HTTP Event Collector token with index routing and ACK settings |

### Forwarders and Inputs

| Type | Description |
|---|---|
| `Forwarder` | A Splunk Universal or Heavy Forwarder registered with the indexer |
| `Input` | A generic data input definition |
| `InputType` | Enum of input categories: MONITOR, TCP, UDP, SCRIPT, WINDOWS_EVENT_LOG, SYSLOG, MODULAR |
| `Monitor` | A file or directory monitor input |
| `WinEventLog` | A Windows Event Log input channel definition |
| `Script` | A scripted data input with execution interval |
| `TCP` | A raw or cooked TCP network input |
| `UDP` | A UDP network input |
| `Syslog` | A syslog-protocol input |
| `ModularInput` | A custom modular input with a declarative scheme |

### Deployment

| Type | Description |
|---|---|
| `DeploymentServer` | A Splunk Deployment Server managing client configurations |
| `DeploymentApp` | An app distributed via a Deployment Server |

### Licensing

| Type | Description |
|---|---|
| `LicensePool` | A license pool grouping slaves and tracking quota consumption |
| `LicenseSlave` | A Splunk instance consuming from a license pool |

### Health and Diagnostics

| Type | Description |
|---|---|
| `HealthReport` | System health summary across Splunk features |
| `HealthStatus` | Enum: GREEN, YELLOW, RED |
| `HealthReason` | An individual health indicator with description and settings |
| `DiagBundle` | A diagnostic data bundle for support or troubleshooting |

### Root Operations

| Type | Description |
|---|---|
| `Query` | Read operations for all Splunk resources |
| `Mutation` | Write operations: create/update/delete searches, indexes, users, inputs, and tokens |
| `Subscription` | Real-time notifications for search job status, alert firings, and health changes |

## Total Named Types

65 named types (object types, enums, and operation roots).
