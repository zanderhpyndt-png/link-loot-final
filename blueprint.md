
{
  "entities": {
    "LootRecord": {
      "title": "LootRecord",
      "description": "A record of a product search and its found alternatives.",
      "type": "object",
      "properties": {
        "originalUrl": { "type": "string", "format": "uri" },
        "productName": { "type": "string" },
        "productImage": { "type": "string", "format": "uri" },
        "category": { "type": "string" },
        "originalPrice": { "type": "number" },
        "timestamp": { "type": "string", "format": "date-time" },
        "matches": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "storeName": { "type": "string" },
              "price": { "type": "number" },
              "productUrl": { "type": "string", "format": "uri" }
            }
          }
        }
      },
      "required": ["originalUrl", "productName", "timestamp"]
    },
    "UserProfile": {
      "title": "UserProfile",
      "description": "User account information.",
      "type": "object",
      "properties": {
        "displayName": { "type": "string" },
        "email": { "type": "string", "format": "email" },
        "photoURL": { "type": "string", "format": "uri" },
        "createdAt": { "type": "string", "format": "date-time" }
      }
    }
  },
  "auth": {
    "providers": ["google.com"]
  },
  "firestore": {
    "/users/{userId}": {
      "schema": { "$ref": "#/entities/UserProfile" },
      "description": "User profile data."
    },
    "/users/{userId}/history/{lootId}": {
      "schema": { "$ref": "#/entities/LootRecord" },
      "description": "A history of loots found by the user."
    }
  }
}
