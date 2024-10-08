# URL Shortener 

This URL Shortener provides functionality to shorten URLs, track analytics, and implement rate limiting. It also integrates Redis caching for frequent access and Bull for background job processing.

## Features
- **Shorten URLs**: Generate unique shortened URLs.
- **Custom Short Code**: Optionally provide a custom short code.
- **Expiry Date**: Set an expiry date for URLs.
- **Analytics**: Track visits with user agent, device type, and more.
- **Rate Limiting**: Limit requests to prevent abuse.
- **Caching**: Redis caching for quicker access to frequently accessed URLs.
- **Background Jobs**: Using Bull to handle visit analytics in the background.

## Setup

### Prerequisites

- Node.js
- MongoDB
- Redis
- Postman (optional)

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/url-shortener.git

2. Set up environment variables in a .env file:
    dbURI=mongodb://localhost:27017/urlShortener
    REDIS_HOST=localhost
    REDIS_PORT=6379

3. Start the server:
    npm start

## API Endpoints

## POST /api/shorten
Shorten a URL or create a custom short code.

### Request
{
  "originalUrl": "http://example.com",
  "customShortCode": "example123", // optional
  "expiryDate": "2024-09-07" // optional
}
### Response
{
  "originalUrl": "http://example.com",
  "shortUrl": "http://localhost:4000/example123",
  "message": "This URL has already been shortened" // if already in database
}

## GET /:shortCode
Redirect to the original URL based on the short code.

### Response
Redirects with status 302 if found.
Returns 404 if the short code is not found.

## GET /api/analytics/:shortCode
Fetch analytics data for a specific short code.

### Response
{
  "originalUrl": "http://example.com",
  "totalVisits": 15,
  "deviceBreakdown": {
    "mobile": 10,
    "desktop": 5
  }
}

## Security Measures
Rate Limiting: Prevent abuse by limiting requests to /shorten.
Input Validation: Ensure valid URLs are being shortened.
Redis Caching: Store frequently accessed URLs in Redis for fast lookup.
Background Processing: Use Bull queue to handle analytics without slowing down the API.


## Advanced Features
Expiry Dates: Automatically handle URL expiration.
Custom Short Codes: Users can provide their own custom short codes if not already in use.
Device Breakdown Analytics: Track mobile vs. desktop visits.
Redis: Caching system to speed up URL redirects.