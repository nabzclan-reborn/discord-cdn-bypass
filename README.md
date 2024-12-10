
# Discord CDN Bypass API

This API allows users to bypass Discord CDN URLs, download the file to the server, and return the file URL for access. Files are automatically deleted 5 minutes after being saved.


## ⚠️ Warning

We’ve moved this endpoint to a new subdomain. Please update your applications to use the current endpoint.

## 📝 Docs (NEW)

[https://public-apis.nabzclan.vip/hc/articles/1/2/3/discord-cdn-bypasser](https://public-apis.nabzclan.vip/hc/articles/1/2/3/discord-cdn-bypasser)

## 📖 API Status

[Visit Status Page](https://uptime.nabzclan.vip/status/public-apis)

![Status Badge](https://uptime.nabzclan.vip/api/badge/5/status?style=plastic)

## Endpoints

### Bypass Discord CDN URL
**Endpoint:**  
`https://public-api.nabzclan.vip/v1/discord-cdn-bypass/`

**Description:**  
This endpoint accepts a Discord CDN URL, downloads the file, saves it to the server, and returns a file URL. The file will be automatically deleted after 5 minutes.

**Request:**

```text
 https://public-api.nabzclan.vip/v1/discord-cdn-bypass/?apitoken=apitokenhere&url=<discord_cdn_url>
```

**Parameters:**

| Parameter | Type   | Description                                     |
|-----------|--------|-------------------------------------------------|
| `url`     | String | The full Discord CDN URL to bypass and download |

**Example Request:**

```text
  https://public-api.nabzclan.vip/v1/discord-cdn-bypass/?apitoken=apitokenhere&url=https://media.discordapp.net/attachments/1148078060407640084/1284251990146154542/IMG_0739.jpg
```

### Response:

**Successful Response:**

The API returns a JSON response with the `file_url` and expiration time.

```json
{
    "success": true,
    "message": "File successfully downloaded and saved.",
    "file_url": "https://public-api.nabzclan.vip/v1/discord-cdn-bypass/uploads/unique_folder/file.png",
    "expires_in": "5 minutes"
}
```

**Error Responses:**

If the provided URL is invalid or unsafe:

```json
{
    "success": false,
    "message": "Invalid or unsafe URL. Please provide a valid Discord CDN link."
}
```

If the `url` parameter is missing:

```json
{
    "success": false,
    "message": "No URL provided."
}
```

If too many requests are made in a short period (rate limiting):

```json
{
    "success": false,
    "message": "Too many requests. Please slow down."
}
```

### File Deletion:

The downloaded file will be automatically deleted from the server **5 minutes** after it is saved. The expiration time is provided in the API response under the `expires_in` field.

## Usage Notes

1. **Rate Limiting**: The API is rate-limited to prevent abuse. If you make too many requests in a short period, you'll receive a "Too many requests" response. Please wait for a moment before retrying.
2. **HTTPS Enforcement**: The API enforces HTTPS for all requests. If the request is made over HTTP, the API will automatically redirect to HTTPS.
3. **Auto-Deletion**: The downloaded file will be deleted from the server 5 minutes after it's saved. The API response provides the expiration time so users know how long they can access the file.

## Example Workflow

1. Send a GET request to the API with the Discord CDN URL.
2. Receive a response with the URL of the saved file and the expiration time.
3. Access the file within 5 minutes using the provided file URL.

**Example API Call:**

```bash
curl "https://public-api.nabzclan.vip/v1/discord-cdn-bypass/?apitoken=apitokenhere&url=https://media.discordapp.net/attachments/1148078060407640084/1284251990146154542/IMG_0739.jpg"
```

**Example JSON Response:**

```json
{
    "success": true,
    "message": "File successfully downloaded and saved.",
    "file_url": "https://public-api.nabzclan.vip/v1/discord-cdn-bypass/uploads/unique_folder/file.png",
    "expires_in": "5 minutes"
}
```

## FAQ

**Q: What happens after 5 minutes?**  
A: The file is automatically deleted from the server, and the link becomes inaccessible.

**Q: How can I test this API?**  
A: You can use tools like `curl`, Postman, or a browser to test the API by sending a GET request with the `url` parameter.

**Q: Is there any limit to the file size I can download?**  
A: This API is limited by your server configuration. Please ensure your server can handle the file sizes you plan to download.

---

## Contributing

If you find any bugs or issues, please feel free to open an issue or contribute to the project by submitting a pull request.

## License

This project is licensed under the MIT License.
