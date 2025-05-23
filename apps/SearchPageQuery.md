This endpoint queries the search page to search for a specific app.

---

## Request Setup

**Endpoint:**  
```
https://graph.oculus.com/graphql
```

**Method:**  
`POST`

**Content-Type:**  
`application/x-www-form-urlencoded`

---

## Python Request Example

```python
import requests
import json

url = "https://graph.oculus.com/graphql"

query = "Orion Drift" # change to whatever app you want to query for (eg. Orion Drift, which is used in this case)

headers = {
    "Content-Type": "application/x-www-form-urlencoded"
}

payload = {
    "access_token": "YOUR_ACCESS_TOKEN_HERE",
    "variables": json.dumps({
        "query": f"{query}",
        "hmdType": "HOLLYWOOD",
        "sort": ["RELEVANCE"]
    }),
    "doc_id": "5228336560551371",
    "operation_name": "SearchPageQuery"
}

response = requests.post(url, headers=headers, data=payload)

print("Status Code:", response.status_code)
print("Response JSON:", response.json())
```

---

## Notes

- Replace the `access_token` value with a valid user access token.
- You can modify the `query` to search for other titles.
- `doc_id` and `operation_name` must **not be changed**.

---

## Sample Response (Truncated)

```json
{
  "data": {
    "application_search": {
      "results": {
        "search_request_id": "Aa4--kr6x8GdtvIGbaR_3nR",
        "edges": [
          {
            "node": {
              "canonical_name": "another-axiom-a2-android6d0f-tpbzjz",
              "display_name": "Orion Drift",
              "comfort_rating": "COMFORTABLE_FOR_SOME",
              "cover_landscape_image": {
                "uri": "https://...oriondrift_image.png"
              },
              "current_offer": {
                "price": {
                  "formatted": "$0.00"
                }
              },
              "quality_rating_aggregate": 4.17,
              "release_date": 1728324240,
              "supported_input_devices_list": [
                { "tag": "OCULUS_TOUCH" }
              ],
              "user_interaction_modes": ["MULTI_USER"]
            }
          },
          {
            "node": {
              "canonical_name": "commuter-games-v-speedway-alpha-android6d0f",
              "display_name": "V-Speedway",
              "genres": ["RACING", "SPORTS", "SIMULATION"],
              "comfort_rating": "COMFORTABLE_FOR_SOME",
              "cover_landscape_image": {
                "uri": "https://...vspeedway_image.png"
              },
              "current_offer": {
                "price": {
                  "formatted": "$0.00"
                }
              },
              "quality_rating_aggregate": 4.09,
              "release_date": 1615398633,
              "supported_input_devices_list": [
                { "tag": "OCULUS_TOUCH" }
              ],
              "user_interaction_modes": ["SINGLE_USER"]
            }
          }
        ]
      }
    }
  }
}
```

---

## Fields of Interest

- `display_name`: Name of the app
- `cover_landscape_image.uri`: App thumbnail
- `current_offer.price.formatted`: Price
- `genres`: App genres
- `quality_rating_aggregate`: Average rating
- `release_date`: Unix timestamp
- `user_interaction_modes`: Supported player modes (e.g., SINGLE_USER, MULTI_USER)

---

## Use Cases

This query is ideal for building:
- Search functions in Meta Quest data tools
- Browsers for VR game marketplaces
- Bots that provide app suggestions

---


