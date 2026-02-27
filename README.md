# data-lakehouse-pipeline

## Dremio + Nessie + MinIO Configuration

To successfully connect Dremio to MinIO using Nessie as a catalog, use the following configuration when adding a new "Nessie" source in Dremio:

### General
*   **Nessie endpoint:** `http://nessie:19120/api/v1`
*   **Auth:** `None`

### Storage
*   **Root path:** `s3://warehouse/iceberg`
*   **Access key:** `admin`
*   **Secret key:** `password`

### Advanced Options / Connection Properties
Add the following properties (ensure no `http://` prefix for the endpoint):

| Property Name | Value |
| :--- | :--- |
| `fs.s3a.endpoint` | `minio:9000` |
| `fs.s3a.path.style.access` | `true` |
| `fs.s3a.connection.ssl.enabled` | `false` |
| `dremio.s3.compat` | `true` |

> **Note:** The `fs.s3a.endpoint` must **not** contain `http://` or `https://`. Including the protocol will cause connection failures (e.g., `Failed to write manifest list file`).