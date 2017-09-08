# Evolution+ API documentation

* [Initialization](#initialization)
* [Actions](#actions)
* [Add action](#add-action)
* [Cancel action](#cancel-action)
* [User](#user)
* [User adding](#user-adding)
* [User editing](#user-editing)
* [Payment transaction](#payment-transaction)
* [User achievement](#user-achievement)

## Initialization
To work with the API, initialization is required using the private key and account ID.

### Method

POST `evolution.plus/api/access_token`

### Parameters

| Parameter       | Type    | Description               |
| ------------- | ------- | ------------------------- |
| account_id    | Number  | Evolution+ account ID |
| secret_code   | String  | Evolution+ secret code     |

### Result

Returns an array with an authorization token and token lifetime (60 minutes). The authorization token should be specified in all subsequent methods. 

| Parameter       | Type    | Description               |
| ------------- | ------- | ------------------------- |
| access_token  | String  | Authorization token       |
| timelife      | Number  | Token lifetime, seconds   |



***


## Actions
Getting a list of user actions according to the specified parameters.

### Method

POST `evolution.plus/api/method/action.get`

### Parameters

| Parameter       | Type    | Description               |
| ------------- | ------- | ------------------------- |
| date1    | UNIXTIME  | Data selection start date |
| date2   | UNIXTIME  | Data selection end date     |
| id    | Number  | Action ID |
| event_code   | String  | Action type code     |
| ext_id    | String  | Action external code |
| user_id   | Number  | User ID     |

### Result

Returns an array of actions according to the specified data selection parameters.  

| Parameter       | Type    | Description               |
| ------------- | ------- | ------------------------- |
| id  | Number  | Action ID       |
| ext_id      | String  | Action external code   |
| code  | String  | Action type code       |
| name      | String  | Action name  |
| date  | Date/Time  | Action date and time       |
| user_id      | Number  | User ID   |

***

## Add action
User action registering in accordance with the list of action types specified in the platform settings. You must specify the user ID or his hash code, as well as the action type code.

### Method

POST `evolution.plus/api/method/action.add`

### Parameters

| Parameter       | Type    | Description               |
| ------------- | ------- | ------------------------- |
| user_code    | Number | Evolution+ user ID |
| action_code   | String | Action type code     |
| time    | UNIXTIME | Action date and time |
| value   | Number | Quantity value      |
| ext_id    | String | Action external code |
| hash   | String | User hash code     |

### Result

If the action is successfully added, its ID to be returned. 

| Parameter       | Type    | Description               |
| ------------- | ------- | ------------------------- |
| action_id  | Number | Action ID       |

***

## Cancel action
User actions deletion is executed by external code EXT_ID. All awards associated with actions are also to be deleted.

### Method

POST `evolution.plus/api/method/action.undo`

### Parameters

| Parameter       | Type    | Description               |
| ------------- | ------- | ------------------------- |
| ext_id    | String | Action external code |


### Result

Returns the number of found actions with the code ext_id.

| Parameter       | Type    | Description               |
| ------------- | ------- | ------------------------- |
| actions  | Number | Number of actions to be deleted |


***

## USER
Receiving the user's personal data according to specified parameters. One of the parameters should be specified.

### Method

POST `evolution.plus/api/method/user.get`

### Parameters

| Parameter       | Type    | Description               |
| ------------- | ------- | ------------------------- |
| ext_id    | String | User external code |
| id    | Number | User ID |
| hash    | String | User hash code |
| phone    | String | User phone (in any format) |


### Result

Returns an array with the user's personal data.

| Parameter       | Type    | Description               |
| ------------- | ------- | ------------------------- |
| id  | Number | User ID |
| hash  | String | User hash code |
| phone | Number | User phone |
| email | String | User email |
| name | String | Name |
| last_name | String | last_name |
| referrer_user_id  | Number | Referrer |
| admin_description | Text | Administrator’s notes |

***

## User adding
A new user creation in the platform. A username must be specified.

### Method

POST `evolution.plus/api/method/user.add`

### Parameters

| Parameter       | Type    | Description               |
| ------------- | ------- | ------------------------- |
| ext_id    | Number | User external code |
| name    | String | Name |
| last_name    | String | Last name |
| photo_url    | String | User photo URL |
| email    | String | User email |
| phone    | String | User phone (in any format) |


### Result

If the user is successfully added, his ID to be returned.

***

## User editing
Editing user data. User external code or user ID must be specified.

### Method

POST `evolution.plus/api/method/user.update`

### Parameters

| Parameter       | Type    | Description               |
| ------------- | ------- | ------------------------- |
| ext_id    | String | User external code |
| id    | Number | User ID |
| name    | String | Name |
| last_name | String | Last name |
| photo_url | String | User photo URL |
| email | String | User email |
| phone | String | User phone (in any format) |
| admin_description | Text | Administrator’s notes |


### Result

If the user is successfully edited, his ID to be returned.

***

## Payment transaction
Adding a new user payment transaction. While debiting, a negative transaction amount is indicated.

### Method

POST `evolution.plus/api/method/money.add`

### Parameters

| Parameter       | Type    | Description               |
| ------------- | ------- | ------------------------- |
| money    | Number | Transaction amount |
| user_id    | Number | User ID |
| description    | String | Transaction description |


### Result

If the transaction is successfully added, "OK" to be returned.

***

## User achievement
Progress parameters and user current progress of achievement.

### Method

POST `evolution.plus/api/method/ achievement.get`

### Parameters

| Parameter       | Type    | Description               |
| ------------- | ------- | ------------------------- |
| user_id    | Number | User ID |
| id    | Number | Achievement ID |


### Result

Returns an array with the achievement parameters and the current progress.

| Parameter       | Type    | Description               |
| ------------- | ------- | ------------------------- |
| id  | Number | Achievement ID |
| name | String | Achievement title |
| level | Array | Array with steps of each level of achievement |
| money | Array | Array with reward amount for each level |
| level_count | Number | Number of levels of achievement |
| progress_value | Number | Current progress of achievement |
| level_now  | Number | Current level of achievement |
| date_unlock | Date/time | Date of achievement unlocking |
| progress_percent | Number | Current progress of achievement, percent |
