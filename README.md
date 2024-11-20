# BidSlammer API Documentation and Examples

Welcome to the BidSlammer API documentation! This API is designed for developers and computer-savvy customers to interact with BidSlammer's services programmatically. You can use it to create applications or automate tasks using your tools and utilities, such as AppleScript.

## Overview

- Access: The API requires an API key, which you can find under the Preferences tab after logging in.
- Requirements: A [Power Pack upgrade](https://bidslammer.com/pricing) is necessary to use the API.
- Call Format: The API uses HTTP GET for all calls, including update and delete operations.
- Important: Ensure you urlencode all values.

For high-volume usage or additional questions, please [contact us](https://bidslammer.com/support).

## Table of Contents

- [Overview](#overview)
- [API Endpoints](#api-endpoints)
  - [justTesting](#justtesting)
  - [addBid](#addbid)
  - [deleteBid](#deletebid)
  - [addSearch](#addsearch)
  - [fetchItem](#fetchitem)
  - [getSearchResults](#getsearchresults)
  - [getUserItems](#getuseritems)
  - [importWatchList](#importwatchlist)
  - [getBidHistoryDataset](#getbidhistorydataset)

## Overview

- **Access**: The API requires an API key, which you can find under the Preferences tab after logging in.
- **Requirements**: A [Power Pack upgrade](https://bidslammer.com/payment) is necessary to use the API.
- **Call Format**: The API uses HTTP GET for all calls, including update and delete operations.
- **Important**: Ensure you urlencode all values.

For high-volume usage or additional questions, please [contact us](https://bidslammer.com/support).

---

## API Endpoints

### justTesting

#### Description
`justTesting` is for testing the API functionality.

#### Parameters
| Parameter | Type   | Description                                          |
|-----------|--------|------------------------------------------------------|
| `key`     | string | (Required) Your API key.                             |
| `arg1`    | string | (Required) Any value to include in the return data.  |
| `arg2`    | string | (Optional) Another value to include in the return.   |
| `arg3`    | string | (Optional) Another value to include in the return.   |

#### Sample Call
`https://bidslammer.com/api/justTesting?key={API_KEY}&arg1=Hello%2C+World`

#### Sample Response
```json
{
    "status": "OK",
    "message": "Well, the API seems to be working.",
    "arg1": "Hello, World",
    "arg2": "",
    "arg3": "",
    "version": "1",
    "timestamp": "2020-03-01 21:41:53"
}
```

---

### addBid

#### Description
`addBid` adds a snipe bid.

#### Parameters
| Parameter   | Type      | Description                                      |
|-------------|-----------|--------------------------------------------------|
| `key`       | string    | (Required) Your API key.                         |
| `item_no`   | integer   | (Required) The eBay item number.                 |
| `bid`       | float     | (Optional) The bid amount (default is 0.00).     |
| `groupName` | string    | (Optional) Name of the Bid Group.                |
| `delay`     | integer   | (Optional) Lead time in seconds (1–15).          |
| `enabled`   | boolean   | (Optional) Enable/disable snipe (0 or 1).        |
| `force`     | boolean   | (Optional) Force bid even if it loses (0 or 1).  |

#### Sample Call
`https://bidslammer.com/api/addBid?key={API_KEY}&item_no=123456789012&bid=0.01&force=1`

#### Sample Response
```json
{
    "bid": "0.01",
    "status": "OK",
    "message": "You successfully added a snipe for 0.01 on eBay item #153847324676."
}
```

---

### deleteBid

#### Description
`deleteBid` removes a snipe bid.

#### Parameters
| Parameter | Type    | Description               |
|-----------|---------|---------------------------|
| `key`     | string  | (Required) Your API key.  |
| `item_no` | integer | (Required) The item number.|

#### Sample Call
`https://bidslammer.com/api/deleteBid?key={API_KEY}&item_no=123456789012`

---

### addSearch

#### Description
`addSearch` adds a query to your "Saved Searches."

#### Parameters
| Parameter | Type   | Description                               |
|-----------|--------|-------------------------------------------|
| `key`     | string | (Required) Your API key.                  |
| `query`   | string | (Required) Search query (max 255 chars).  |

#### Sample Call
`https://bidslammer.com/api/addSearch?key={API_KEY}&query=Beanie+Babies`

---

### deleteSearch

#### Description
`deleteSearch` deletes a search from your "Saved Searches" list.

#### Parameters
| Parameter | Type    | Description                                        |
|-----------|---------|----------------------------------------------------|
| `key`     | string  | (Required) Your API key.                           |
| `id`      | integer | (Required) The ID number of the query to be deleted.|

#### Sample Call
`https://bidslammer.com/api/deleteSearch?key={API_KEY}&id=123456`

#### Sample Response
```json
{
    "status": "OK",
    "message": "Search successfully deleted.",
    "id": 123456
}
```

---

### fetchItem

#### Description
`fetchItem` retrieves details about an item in your account.

#### Parameters
| Parameter | Type    | Description                |
|-----------|---------|----------------------------|
| `key`     | string  | (Required) Your API key.   |
| `item_no` | integer | (Required) The item number.|

#### Sample Call
`https://bidslammer.com/api/fetchItem?key={API_KEY}&item_no=123456789012`

#### Sample Response
```json
{
    "status": "OK",
    "currentPrice": 9.99,
    "title": "Coconut Lime Verbena Candle",
    "sellerUserId": "seller123",
    "endTime": "2023-12-31 23:59:59"
}
```

---

### checkSnipeStatus

#### Description
`checkSnipeStatus` provides the win/loss status of the snipe. If it is a loss, the reason is included. If the snipe has not executed, it will return a status of "Pending."

#### Parameters
| Parameter | Type    | Description               |
|-----------|---------|---------------------------|
| `key`     | string  | (Required) Your API key.  |
| `item_no` | integer | (Required) The item number.|

#### Sample Call
`https://bidslammer.com/api/checkSnipeStatus?key={API_KEY}&item_no=123456789012`

#### Sample Response
```json
{
    "status": "OK",
    "item_no": "123456789012",
    "snipe_status": "Pending",
    "message": "The snipe is scheduled to execute."
}
```

---

### getSearchResults

#### Description
`getSearchResults` retrieves search results (up to 100 items) from eBay based on a given query.

#### Parameters
| Parameter      | Type   | Description                                            |
|----------------|--------|--------------------------------------------------------|
| `key`          | string | (Required) Your API key.                               |
| `country_code` | string | (Optional) 2-letter country code (default: `US`).       |
| `query`        | string | (Required) The search query.                           |

#### Sample Call
`https://bidslammer.com/api/getSearchResults?key={API_KEY}&query=Beanie+Babies`

#### Sample Response
```json
{
    "status": "OK",
    "results": [
        {
            "item_no": "123456789012",
            "title": "Vintage Beanie Baby",
            "price": 25.99,
            "currency": "USD",
            "end_time": "2023-12-31 23:59:59",
            "seller": "example_seller"
        },
        {
            "item_no": "234567890123",
            "title": "Rare Beanie Baby Elephant",
            "price": 45.50,
            "currency": "USD",
            "end_time": "2024-01-01 12:00:00",
            "seller": "another_seller"
        }
    ]
}
```

---

### getUserItems

#### Description
`getUserItems` returns a list of user snipes with all parameters.

#### Parameters
| Parameter  | Type    | Description                                                                 |
|------------|---------|-----------------------------------------------------------------------------|
| `key`      | string  | (Required) Your API key.                                                    |
| `filter`   | string  | (Required) The list of items you want. Options: `watched`, `current`, `completed`, `archive`. |
| `orderby`  | string  | (Optional) Field to order by. Options: `ends` or `bids`.                    |
| `dir`      | string  | (Optional) Order direction. Options: `ASC` or `DESC`.                      |
| `offset`   | integer | (Optional) Number of records to skip.                                       |
| `limit`    | integer | (Optional) Maximum number of records to return (default is 20).             |
| `show_won` | boolean | (Optional) Include "won" items in the results. Options: `0` or `1`.         |

#### Sample Call
`https://bidslammer.com/api/getUserItems?key={API_KEY}&filter=current`

#### Sample Response
```json
{
    "status": "OK",
    "items": [
        {
            "item_no": "123456789012",
            "title": "Example Item Title",
            "current_price": 19.99,
            "end_time": "2023-12-31 23:59:59",
            "status": "won"
        },
        {
            "item_no": "234567890123",
            "title": "Another Example Item",
            "current_price": 15.00,
            "end_time": "2023-12-30 22:00:00",
            "status": "lost"
        }
    ]
}
```

---

### getUserSearches

#### Description
`getUserSearches` retrieves the list of "Saved Searches" for the user.

#### Parameters
| Parameter | Type   | Description               |
|-----------|--------|---------------------------|
| `key`     | string | (Required) Your API key.  |

#### Sample Call
`https://bidslammer.com/api/getUserSearches?key={API_KEY}`

#### Sample Response
```json
{
    "status": "OK",
    "searches": [
        {
            "id": 123456,
            "query": "Vintage Watches",
            "created_at": "2023-01-01 12:00:00"
        },
        {
            "id": 234567,
            "query": "Rare Coins",
            "created_at": "2023-01-05 15:30:00"
        }
    ]
}
```

---

### importWatchList

#### Description
`importWatchList` imports the user's Watch List from eBay. Note: This operation can take up to a minute or more.

#### Parameters
| Parameter | Type   | Description               |
|-----------|--------|---------------------------|
| `key`     | string | (Required) Your API key.  |

#### Sample Call
`https://bidslammer.com/api/importWatchList?key={API_KEY}`

#### Sample Response
```json
{
    "status": "OK",
    "message": "Watch List successfully imported.",
    "items_imported": 25
}
```

---

### getBidHistoryDataset

#### Description
`getBidHistoryDataset` provides bidding history data for an item in a format compatible with Chart.js or QuickChart.io.

#### Parameters
| Parameter | Type    | Description                |
|-----------|---------|----------------------------|
| `key`     | string  | (Required) Your API key.   |
| `item_no` | integer | (Required) The item number.|

#### Sample Call
`https://bidslammer.com/api/getBidHistoryDataset?key={API_KEY}&item_no=123456789012`

#### Sample Response
```json
{
    "status": "OK",
    "data": [
        {
            "x": 1714944227000,
            "y": 10.00
        },
        {
            "x": 1715048287000,
            "y": 12.00
        }
    ],
    "snipe_value": 15.00
}
```
