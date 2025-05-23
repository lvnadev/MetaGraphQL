This request gets an apps version history and version details based on its specific App ID.

---

## Endpoint

```
POST https://graph.oculus.com/graphql
```

---

## Authentication

You must include a **valid access token** associated with your Meta developer account. The access token must have permission to query the app metadata.

- **Replace** the example `access_token` with your own.
- **Do not share** your token publicly.

---

## Request Details

### Headers

```http
Content-Type: application/x-www-form-urlencoded
```

### Payload Parameters

| Key              | Type   | Description                                                                 |
|------------------|--------|-----------------------------------------------------------------------------|
| `access_token`   | string | **Required.** Your personal Oculus Graph API token.                         |
| `variables`      | JSON   | JSON-encoded object with the `id` field set to the App ID you want to query.|
| `doc_id`         | string | Always use `"7752503738170734"` for this query.                            |
| `operation_name` | string | Always use `"AppReleaseNotesQuery"`.                                       |

---

## Python Example

```python
import requests
import json

url = "https://graph.oculus.com/graphql"
appid = "3262063300561328"  # Replace with the desired App ID

headers = {
    "Content-Type": "application/x-www-form-urlencoded"
}

payload = {
    "access_token": "YOUR_ACCESS_TOKEN_HERE",  # Replace with your own token
    "variables": json.dumps({
        "id": appid
    }),
    "doc_id": "7752503738170734",  # Must not be changed
    "operation_name": "AppReleaseNotesQuery"  # Must not be changed
}

response = requests.post(url, headers=headers, data=payload)

print("status", response.status_code)
print("response", response.json())
```

---

## Example Response

Here’s a **sample response** for the app Gorilla Tag (`appid: 3262063300561328`):

```json
{
  "data": {
    "node": {
      "__typename": "Application",
      "displayName": "Gorilla Tag",
      "supportedBinaries": {
        "edges": [
          {
            "node": {
              "__typename": "PCBinary",
              "version": "1.1.110",
              "versionCode": 356,
              "changeLog": null,
              "richChangeLog": "",
              "id": "9277642152336716"
            }
          }
          // ... More versions
        ]
      },
      "id": "3262063300561328"
    }
  }
}
```

### Fields

- `displayName`: Name of the application
- `supportedBinaries.edges`: List of released versions
  - `version`: Version string (e.g. `"1.1.110"`)
  - `versionCode`: Internal version code
  - `changeLog` / `richChangeLog`: Text content of the release notes (can be `null` or empty)
  - `id`: Unique ID for the binary release

---

## Notes

- The `doc_id` and `operation_name` are **fixed** and must not be changed.
- Only the **`appid`** and **`access_token`** should be modified depending on your target.
- The `richChangeLog` may often be empty or `null` depending on how the developer filled the metadata.

---

## Use Cases

- Displaying update history for an app
- Monitoring version changes
- Fetching release notes for changelog bots or dashboards
