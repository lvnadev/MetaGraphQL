This request queries the store page for a specific app using an app id.

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

| Key              | Type   | Description                                                                       |
|------------------|--------|-----------------------------------------------------------------------------------|
| `access_token`   | string | **Required.** Your personal Oculus Graph API token.                               |
| `variables`      | JSON   | JSON-encoded object with the `itemId` field set to the App ID you want to query.  |
| `doc_id`         | string | Always use `"8733883600046341"` for this query.                                   |
| `operation_name` | string | Always use `"StoreAppQuery"`.                                                     |

---

## Python Example

```python
import requests
import json

url = "https://graph.oculus.com/graphql"

appid = "6458628580871969" # desired app id, this is the app id for the Rift version of Gorilla Tag

headers = {
    "Content-Type": "application/x-www-form-urlencoded"
}

payload = {
    "access_token": "YOUR_ACCESS_TOKEN_HERE",
    "variables": json.dumps({
        "itemId":"3262063300561328","first":5,"last":None,"after":None,"before":None,"forward":True,"hmdType":"HOLLYWOOD"
    }),
    "doc_id": "8733883600046341",
    "operation_name": "StoreAppQuery"
}

response = requests.post(url, headers=headers, data=payload)

print("status", response.status_code)
print("response", response.json())
```

---

Sure! Here's your modified **example response** section, rewritten to reflect the **cleaned-up JSON** you provided earlier for *Gorilla Tag*:

---

## Example Response

Here’s a **sample response** for the app *Gorilla Tag* (trunicated) (`appid: 3262063300561328`):

```json
{
  "data": {
    "node": {
      "id": "3262063300561328",
      "display_name": "Gorilla Tag",
      "platform": "PC",
      "developer_name": "Another Axiom Inc",
      "publisher_name": "Another Axiom",
      "release_date": 1626368427,
      "website_url": "https://gorillatagvr.com/",
      "privacy_policy_url": "https://gorillatagvr.com/privacy-policy/",
      "terms_of_service_url": "https://gorillatagvr.com/tos/",
      "description": "Run, climb, and jump in VR using just your hands. Four game modes, six maps, crossplay, and mod support. Includes 5000 Shiny Rocks (in-app currency).",
      "age_rating": "Everyone",
      "content_descriptors": ["Mild Fantasy Violence"],
      "interactive_elements": ["Users Interact", "In-Game Purchases"],
      "supported_input_devices": [
        "Touch Controller (Rift)",
        "Touch Controller (Quest 2)",
        "Touch Controller (Quest Pro)"
      ],
      "supported_hmd_platforms": ["Quest", "Rift"],
      "current_version": {
        "version": "1.0.0",
        "release_notes": null
      },
      "supported_player_modes": [
        "Sitting",
        "Standing",
        "RoomScale"
      ],
      "app_icons": {
        "square": {
          "uri": "https://static.oculuscdn.com/image/upload/t_share_icon/...",
          "height": 360,
          "width": 360
        }
      },
      "category": {
        "category_type": "GAMES",
        "name": "Action"
      },
      "iap_details": {
        "supported": true
      },
      "supported_in_app_languages": [
        {
          "locale": "en_US",
          "name": "English (US)",
          "support_level": "FULL"
        }
      ],
      "system_requirements": {
        "recommended_cpu": "Intel i5-4590 / AMD Ryzen 5 1500X or greater",
        "recommended_gpu": "NVIDIA GTX 1060 / AMD RX 480 or greater",
        "recommended_memory_in_mb": 8192,
        "recommended_os_version": "Windows 10",
        "recommended_disk_space": "1 GB available space"
      },
      "url": "https://www.meta.com/experiences/3262063300561328/"
    }
  }
}
```

### Fields

* `display_name`: Name of the application
* `platform`: Device platform (e.g. `"PC"`)
* `developer_name`, `publisher_name`: Developer and publisher
* `release_date`: Epoch timestamp of the release
* `website_url`, `privacy_policy_url`, `terms_of_service_url`: External links
* `description`: Short summary of the game
* `age_rating`, `content_descriptors`, `interactive_elements`: ESRB and store metadata
* `supported_input_devices`, `supported_hmd_platforms`: Hardware compatibility
* `current_version.version`: Latest known version string
* `supported_player_modes`: VR play modes supported
* `app_icons.square.uri`: App icon URL (square format)
* `category.name`: App genre/category
* `iap_details.supported`: Whether in-app purchases are supported
* `supported_in_app_languages`: Language and support level info
* `system_requirements`: Recommended system specs
* `url`: Store page for the app


---

## Notes

- The `doc_id` and `operation_name` are **fixed** and must not be changed.
- Only the **`appid`** and **`access_token`** should be modified depending on your target.

---

## Use Cases

- Displaying update history for an app
- Monitoring version changes
- Fetching release notes for changelog bots or dashboards

