# Variables

Variables can be used in Discord Webhook messages and the view route to customize the message with dynamic content. Variables also allow you to use modifiers to format the content in a specific way.

**Format:** `{variableName.property::modifier::secondModifier}`

At the bottom of this guide there is information about testing variables.

## Available Variables

### User

| Variable | Type | Description |
|----------|------|-------------|
| `{user.id}` | string | The user's ID |
| `{user.createdAt}` | date | The user's creation date |
| `{user.updatedAt}` | date | The user's last update date |
| `{user.username}` | string | The user's username |
| `{user.role}` | string | The user's role: USER \| ADMIN \| SUPERADMIN |

### File

> **Info:** These variables are only available in the case of anything related to files.

| Variable | Type | Description |
|----------|------|-------------|
| `{file.id}` | string | The file's ID |
| `{file.createdAt}` | date | The file's creation date |
| `{file.updatedAt}` | date | The file's last update date |
| `{file.deletesAt}` | date | The file's expiration date (optional) |
| `{file.favorite}` | boolean | If the file is favorited |
| `{file.name}` | string | The file's name |
| `{file.originalName}` | string | The file's original name (optional) |
| `{file.size}` | number | The file's size in bytes |
| `{file.type}` | string | The file's type |
| `{file.views}` | number | The file's views |
| `{file.maxViews}` | number | The file's max views (optional) |
| `{file.folderId}` | string | The file's folder ID (optional) |

### URL

> **Info:** These variables are only available in the case of anything related to URLs.

| Variable | Type | Description |
|----------|------|-------------|
| `{url.id}` | string | The URL's ID |
| `{url.createdAt}` | date | The URL's creation date |
| `{url.updatedAt}` | date | The URL's last update date |
| `{url.code}` | string | The URL's code |
| `{url.vanity}` | string | The URL's vanity (optional) |
| `{url.destination}` | string | The URL's destination |
| `{url.views}` | number | The URL's views |
| `{url.maxViews}` | number | The URL's max views (optional) |

### Link

> **Info:** These variables are only available on the `onUpload` and `onShorten` events.

| Variable | Type | Description |
|----------|------|-------------|
| `{link.returned}` | string | The returned link when a file is uploaded or a URL is shortened (optional) |
| `{link.raw}` | string | Only available on the onUpload event, this will be the raw file link (optional) |

### User Metrics

These are variables to access user metrics.

| Variable | Type | Description |
|----------|------|-------------|
| `{metricsUser.files}` | number | The user's total files |
| `{metricsUser.urls}` | number | The user's total URLs |
| `{metricsUser.storage}` | number | The user's total storage in bytes |
| `{metricsUser.fileViews}` | number | The user's total file views |
| `{metricsUser.urlViews}` | number | The user's total URL views |

### ShareHost Metrics

These are variables for the current instance metrics (not limited to the user).

| Variable | Type | Description |
|----------|------|-------------|
| `{metricsZipline.files}` | number | The total files |
| `{metricsZipline.urls}` | number | The total URLs |
| `{metricsZipline.storage}` | number | The total storage in bytes |
| `{metricsZipline.fileViews}` | number | The total file views |
| `{metricsZipline.urlViews}` | number | The total URL views |

> **Note:** The variable names still use `metricsZipline` for backwards compatibility with the original codebase.

### Debug

If you are having issues with variables, you can use these debug variables to see the raw data in JSON format.

| Variable | Type | Description |
|----------|------|-------------|
| `{debug.json}` | string | The raw JSON data of the event unformatted (optional) |
| `{debug.jsonf}` | string | The raw JSON data of the event formatted with 2 space tabs (optional) |

## Modifiers

To use modifiers, you need to add them after the variable with a double colon `::`. For example, to format a date to UTC time you would use `{user.createdAt::utc}`.

### String Modifiers

| Modifier | Description | Example |
|----------|-------------|---------|
| `upper` | Uppercase the string | `aBcD` → `ABCD` |
| `lower` | Lowercase the string | `aBcD` → `abcd` |
| `title` | Title case the string | `aBcD` → `Abcd` |
| `length` | Get the string length | `aBcD` → `4` |
| `reverse` | Reverse the string | `aBcD` → `DcBa` |
| `base64` | Encode the string to base64 | `aBcD` → `YUJjRA==` |
| `hex` | Encode the string to hex | `aBcD` → `61426344` |
| `string` | Convert the value to string | `aBcD` → `aBcD` |

Unknown modifier returns: `{unknown_str_modifier({mod})}`

### Number Modifiers

| Modifier | Description | Example |
|----------|-------------|---------|
| `comma` | Add commas to the number | `1000` → `1,000` |
| `hex` | Encode the number to hex | `1000` → `3E8` |
| `octal` | Encode the number to octal | `1000` → `1750` |
| `binary` | Encode the number to binary | `1000` → `1111101000` |
| `bytes` | Convert the number to bytes | `1000` → `1 KB` |
| `string` | Convert the value to string | `1000` → `1000` |

Unknown modifier returns: `{unknown_int_modifier({mod})}`

### Date Modifiers

| Modifier | Description | Example | Requirements |
|----------|-------------|---------|--------------|
| `locale` | Format the date to the locale provided or system default | `9/22/2024` → `9/22/2024, 12:00:00 AM` | locale/timezone configuration |
| `time` | Format the date to the time provided | `9/22/2024` → `12:00:00 AM` | locale/timezone configuration |
| `date` | Format the date to the date provided | `9/22/2024` → `9/22/2024` | locale/timezone configuration |
| `unix` | Convert the date to a Unix timestamp | `9/22/2024` → `1692819200000` | |
| `iso` | Convert the date to an ISO string | `9/22/2024` → `2024-09-22T00:00:00.000Z` | |
| `utc` | Convert the date to UTC time | `9/22/2024` → `2024-09-22T00:00:00.000Z` | |
| `year` | Get the year from the date | `9/22/2024` → `2024` | |
| `month` | Get the month from the date | `9/22/2024` → `9` | |
| `day` | Get the day from the date | `9/22/2024` → `22` | |
| `hour` | Get the hour from the date | `9/22/2024` → `0` | |
| `minute` | Get the minute from the date | `9/22/2024` → `0` | |
| `second` | Get the second from the date | `9/22/2024` → `0` | |
| `string` | Convert the value to string | `9/22/2024` → `9/22/2024` | |
| `ampm` | Get the am/pm from the date | `9/22/2024 12:00:00 am` → `am` | |
| `AMPM` | Get the AM/PM from the date | `9/22/2024 12:00:00 am` → `AM` | |

## Locale/Timezone Modifiers

ShareHost lets you specify the locale and timezone for the `locale`, `time`, and `date` modifiers. To achieve this you need to specify the 2nd modifier: `{user.createdAt::locale::en-UK,Europe/London}`.

For example, using `{user.createdAt::locale::ja-JP,Asia/Tokyo}` will format the date to the Japanese locale and timezone and will yield a result of `2024/9/23 0:30:00` when the system time is `9/22/2024 11:30 AM` in the `America/Los_Angeles` timezone.

It is also possible to continue using the system locale, but specify a different timezone. To do this just specify the timezone: `{user.createdAt::locale::,Europe/London}`. Notice the comma is right after the double colons.

Some specific use cases for this may be if you want to use 24-hour time but continue using an American timezone, you can use `{user.createdAt::locale::en-UK,America/Los_Angeles}`. This will format the date and time to use 24-hour time and `dd/mm/yyyy` format instead of the default `mm/dd/yyyy` format used in the US.

### Useful Info

If you are looking for a list of possible locales, you can visit [Unicode CLDR Language Territory Information](https://www.unicode.org/cldr/charts/44/supplemental/language_territory_information.html). To use this table, take the language code ("Code" in the table) and the territory code ("Territory" in the table) and combine them with a hyphen. For example, the code for English in the United Kingdom is `en-UK`, and the code for Japanese in Japan is `ja-JP`.

A list of timezones can be found at [Wikipedia: List of tz database time zones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones). Use the value under the "TZ identifier" column.

> **Info:** All values are case insensitive, so `en-UK` is the same as `EN-uk` and `en-uk`. The same goes for timezones: `America/Los_Angeles` is the same as `america/los_angeles` and `AMERICA/LOS_ANGELES`.

## Conditional Modifiers

To use conditional modifiers, you need to add them after the variable with a double colon `::`, like normal modifiers but with a different format: `{variableName.property::conditionalModifier["trueString"||"falseString"]}`.

For example, to show the file's views if it has max views, you would use `{file.maxViews::>0["{file.views}/{file.maxViews}"||"No max views"]}`. This will show the views and max views if the max views are greater than 0, otherwise it will show "No max views".

### Available Conditional Modifiers

| Modifier | Description | Applicable Types | Requirements |
|----------|-------------|------------------|--------------|
| `istrue` | If the boolean is true | boolean | None |
| `exists` | Whether the element exists | string, date | None |
| `$X` | If the string starts with X | string | X = string |
| `^X` | If the string ends with X | string | X = string |
| `~X` | If the string includes X | string | X = string |
| `=X` | If the value equals to X | string, number | X = string or number |
| `>=X` | If the number is greater or equal to X | number | X = number |
| `>X` | If the number is greater than X | number | X = number |
| `<=X` | If the number is lesser or equal to X | number | X = number |
| `<X` | If the number is lesser than X | number | X = number |

## Examples

### Basic Usage

```
{user.username} uploaded {file.name}
```
Output: `john_doe uploaded screenshot.png`

### With Modifiers

```
{file.size::bytes} file uploaded by {user.username::upper}
```
Output: `2.5 MB file uploaded by JOHN_DOE`

### With Conditionals

```
{file.maxViews::>0["{file.views}/{file.maxViews} views"||"Unlimited views"]}
```
Output: `150/1000 views` (if maxViews > 0) or `Unlimited views` (if maxViews = 0)

### Date Formatting

```
Uploaded on {file.createdAt::date::en-US,America/New_York} at {file.createdAt::time::en-US,America/New_York}
```
Output: `Uploaded on 12/14/2025 at 3:30:15 PM`

### Complex Example

```
{user.username} ({file.id}) uploaded {file.name} ({file.size::bytes}) (original name: {file.originalName}) at {file.createdAt::hour}:{file.createdAt::minute} today
```
Output: `john_doe (cm1dvtfpy000008kv7f4dea03) uploaded 51QcNn.png (5 MB) (original name: screenshot.png) at 15:30 today`

## Testing Variables

To test variables in your ShareHost instance, you can use:

1. **Discord Webhooks** - Set up a test webhook and use variables in the message
2. **View Routes** - Configure view routes with variables and test by uploading files
3. **Debug Variables** - Use `{debug.jsonf}` to see all available data in formatted JSON

## Sample Data Structure

```json
{
  "file": {
    "createdAt": "2025-12-14T08:21:48.784Z",
    "updatedAt": "2025-12-14T08:21:48.784Z",
    "deletesAt": "2025-12-14T08:21:48.784Z",
    "favorite": true,
    "id": "cm1dvtfpy000008kv7f4dea03",
    "originalName": "fileOriginalName.png",
    "name": "51QcNn.png",
    "size": 5242880,
    "type": "image/png",
    "views": 12345,
    "maxViews": 1000000,
    "folderId": "cm1dvw7xo000208kv7bhiebxl"
  },
  "url": {
    "createdAt": "2025-12-14T08:21:48.784Z",
    "updatedAt": "2025-12-14T08:21:48.784Z",
    "id": "cm1dvwl5n000308kv49475k66",
    "code": "5XbW8b",
    "vanity": "google",
    "destination": "https://google.com",
    "views": 12345,
    "maxViews": 1000000
  },
  "user": {
    "id": "cm1dvxhfq000408kvf42r6dgb",
    "createdAt": "2025-12-14T08:21:48.784Z",
    "updatedAt": "2025-12-14T08:21:48.784Z",
    "role": "USER",
    "username": "john_doe"
  },
  "link": {
    "raw": "https://example.com/r/51QcNn.png",
    "returned": "https://example.com/u/51QcNn.png"
  },
  "metricsUser": {
    "files": 100,
    "urls": 23,
    "storage": 1073741824,
    "fileViews": 12345,
    "urlViews": 12345
  },
  "metricsZipline": {
    "files": 200,
    "urls": 30,
    "storage": 2147483648,
    "fileViews": 37035,
    "urlViews": 24690
  }
}
```

---

*Last updated: December 14, 2025*

*This documentation is part of the ShareHost project - a self-hosted file and URL sharing platform.*
