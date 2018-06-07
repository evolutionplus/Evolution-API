# Evolution+ API documentation

* [Initialization](#initialization)
* [Actions](#actions)
* [Add action](#add-action)
* [Cancel action](#cancel-action)
* [User](#user)
* [Add User](#user-adding)
* [User Update](#user-editing)
* [Payment Transaction](#payment-transaction)
* [User Achievement](#user-achievement)

## Initialization
To work with the API, initialization is required using the private key and account ID. This information can be obtained from the control panel.

### Method

POST `evolution.plus/api/access_token`

### Initialization Params

| Field         | Type    | Description               |
| ------------- | ------- | ------------------------- |
| account_id    | Number  | Evolution+ account ID |
| secret_code   | String  | Evolution+ secret code     |

### Result

Returns an array with an authorization token and token lifetime (60 minutes).  The authorization token should be specified in all subsequent methods. 

| Field         | Type    | Description               |
| ------------- | ------- | ------------------------- |
| access_token  | String  | Authorization token       |
| timelife      | Number  | Token lifetime, seconds   |



***


## Actions
Getting a list of user actions according to the specified parameters.

### Method

POST `evolution.plus/api/method/action.get`

### Actions Params

| Field       | Type    | Description               |
| ------------- | ------- | ------------------------- |
| date1    | UNIXTIME  | Start date |
| date2   | UNIXTIME  | End date     |
| id    | Number  | Action ID |
| event_code   | String  | Action type code     |
| ext_id    | String  | External code of the action |
| user_id   | Number  | User ID     |

### Actions Result

Returns an array of actions according to the specified data selection parameters.  

| Field       | Type    | Description               |
| ------------- | ------- | ------------------------- |
| id  | Number  | Action ID       |
| ext_id      | String  | External code of the action   |
| code  | String  | Action type code       |
| name      | String  | Action name  |
| date  | Date/Time  | Action date and time       |
| user_id      | Number  | User ID   |

***

## Add Action
User action registering in accordance with the list of action types specified in the platform settings. You must specify the user ID or his hash code, as well as the action type code.

### Method

POST `evolution.plus/api/method/action.add`

### Params

| Field       | Type    | Description               |
| ------------- | ------- | ------------------------- |
| user_code    | Number | User external code |
| action_code   | String | Action type code     |
| time    | UNIXTIME | Action date and time |
| value   | Number | Quantity value      |
| ext_id    | String | External code of the action |
| hash   | String | User hash code     |

### Result

If the action is successfully added, its ID to be returned.

| Parameter       | Type    | Description               |
| ------------- | ------- | ------------------------- |
| action_id  | Number | Action ID       |

***

## Cancel action
User actions deletion is executed by external code ext_id. All awards associated with the actions are also to be deleted.

### Method

POST `evolution.plus/api/method/action.undo`

### Params

| Field        | Type    | Description               |
| ------------- | ------- | ------------------------- |
| ext_id    | String | External action code |


### Result

Returns the number of found actions with the code ext_id.

| Field       | Type    | Description               |
| ------------- | ------- | ------------------------- |
| actions  | Number | Number of actions to be deleted |


***

## USER
Receiving the user's personal data according to specified parameters. One of the parameters should be specified.

### Method

POST `evolution.plus/api/method/user.get`

### User Params

| Field       | Type    | Description               |
| ------------- | ------- | ------------------------- |
| ext_id    | String | User external code |
| id    | Number | User ID |
| hash    | String | User hash code |
| phone    | String | User phone (in any format) |


### Result

Returns an array with the user's personal data.

| Field         | Type    | Description               |
| ------------- | ------- | ------------------------- |
| id  | Number | User ID |
| hash  | String | User hash code |
| phone | Number | User phone |
| email | String | User email |
| name | String | Name |
| last_name | String | last_name |
| gender | String | User gender |
| ext_id | String | User external code |
| level_id | Number | User level ID |
| referrer_user_id  | Number | Referrer |
| admin_description | Text | Administrator’s notes |

***

## Add User
A new user adding in the platform. A username is required.

### Method

POST `evolution.plus/api/method/user.add`

### User Params

| Field         | Type    | Description               |
| ------------- | ------- | ------------------------- |
| ext_id    | Number | User external code |
| name    | String | Name |
| last_name    | String | Last name |
| photo    | String | User photo URL |
| email    | String | User email |
| phone    | String | User phone (in any format) |
| gender    | String | User gender (M or F) |


### Result

If the user is successfully added, his ID to be returned.

| Field         | Type    | Description               |
| ------------- | ------- | ------------------------- |
| ID    | Number | User ID |

***

## User Update
Updating user data. User external code or user ID must be specified.

### Method

POST `evolution.plus/api/method/user.update`

### User Params

| Field       | Type    | Description               |
| ------------- | ------- | ------------------------- |
| ext_id    | String | User external code |
| id    | Number | User ID |
| name    | String | Name |
| last_name | String | Last name |
| photo | String | User photo URL |
| email | String | User email |
| phone | String | User phone (in any format) |
| gender    | String | User gender (M or F) |
| admin_description | Text | Administrator’s notes |
| rating | String | Publish user rating (Y or N) |


### Result

If the user is successfully edited, his ID to be returned.

| Field       | Type    | Description               |
| ------------- | ------- | ------------------------- |
| ID    | Number | User ID |


***

## Payment Transaction
Adding a new user payment transaction.

### Method

POST `evolution.plus/api/method/money.add`

### Transaction Params

| Field       | Type    | Description               |
| ------------- | ------- | ------------------------- |
| money    | Number | Transaction amount |
| user_id    | Number | User ID |
| description    | String | Transaction description |


### Result

If the transaction is successfully added, "OK" to be returned.

***

## User Achievement
Achievement parameters and user current progress of achievement.

### Method

POST `evolution.plus/api/method/achievement.get`

### Achievement Params

| Field       | Type    | Description               |
| ------------- | ------- | ------------------------- |
| user_id    | Number | User ID |
| id    | Number | Achievement ID |


### Result

Returns an array with the achievement parameters and the current progress.

| Field       | Type    | Description               |
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
