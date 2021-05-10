# NISROOM API for Lambda

## Overview

### NISLAB Room Monitor API for AWS Lambda

Frontend is [here](https://github.com/Kenny-NISLab/nisroom)

## Architecture

![nisroom-architecture](https://user-images.githubusercontent.com/49851726/116494988-07617b80-a8dd-11eb-9c49-bb7cda1e2eb3.png)

## How To Use Repository

1. Fork and Clone
2. `git remote add upstream https://github.com/Kenny-NISLab/nisroom-api.git`
3. `git pull upstream develop`

## Setup

1. `npm install`

## Format before Commit

1. `npm run format`

## API Documentation

### API List

| No. | API Function No. | Type | API Name        | Overview               |
| --- | ---------------- | ---- | --------------- | ---------------------- |
| 0   | NISROOM-000      | API  | nisroom-api     | Production Environment |
| 1   | NISROOM-001      | API  | nisroom-api-dev | Test Environment       |

### Resource Types

#### students

| HTTP Method | Access URI   | Objective                         |
| ----------- | ------------ | --------------------------------- |
| GET         | /v1/students | Get all information about members |

- GET Data (JSON)

| Category | JSON Key | Type | Description |
| -------- | -------- | ---- | ----------- |
| None     |          |      |             |

- Response Data (JSON)

| Category                | JSON Key     | Type    | Description                             |
| ----------------------- | ------------ | ------- | --------------------------------------- |
| ID                      | id           | Value   | ID                                      |
| Image                   | avatar       | URL     | Image of Slack                          |
| First Name (En)         | e_first_name | String  | First Name in English                   |
| Last Name (En)          | e_last_name  | String  | Last Name in English                    |
| Grade                   | grade        | String  | Grade of member                         |
| Status of stay          | is_stay      | Boolean | Whether the member is in the Lab or not |
| First Name (Ja)         | j_first_name | String  | First Name in Japanese                  |
| Last Name (Ja)          | j_last_name  | String  | Last Name in Japanese                   |
| Student ID              | student_id   | Value   | Student ID                              |
| Scheduled date of visit | schedule     | Array   | Scheduled date of visit                 |

#### id

| HTTP Method | Access URI        | Objective                           |
| ----------- | ----------------- | ----------------------------------- |
| PATCH       | /v1/students/{id} | Update information about the member |

- PATCH Data (JSON)

| Category               | JSON Key | Type    | Description                                                                                                   |
| ---------------------- | -------- | ------- | ------------------------------------------------------------------------------------------------------------- |
| Status of stay         | is_stay  | Boolean | Whether the member is in the Lab or not (true or false)                                                       |
| Schedule date of visit | schedule | Array   | Scheduled date of visit ({YYYY-MM-DD, YYYY-MM-D'D', ...})<br>If the value is an empty array, it will be null. |

- Response Data (JSON)

| Category                | JSON Key | Type    | Description                                                       |
| ----------------------- | -------- | ------- | ----------------------------------------------------------------- |
| Status of stay          | is_stay  | Boolean | Whether the member is in the Lab or not (Same data as PATCH Data) |
| Scheduled date of visit | schedule | Array   | Scheduled date of visit (["YYYY-MM-DD", "YYYY-MM-D'D', ...])      |

## Database design and structure

<table>
<thead>
<tr>
<th scope="col">Primary Key</th>
<th align="center" scope="col" rowspan="2" colspan="9">Attributes</th>
</tr>
<tr>
<th scope="col">Partition Key</th>
</tr>
<tr>
<th align="center" scope="col">id</th>
<th align="center" scope="col">avater</th>
<th align="center" scope="col">e_first_name</th>
<th align="center" scope="col">e_last_name</th>
<th align="center" scope="col">grade</th>
</tr>
</thead>
<tbody>
<tr>
<td align="center">{Integer}</td>
<td align="center">{String}</td>
<td align="center">{String}</td>
<td align="center">{String}</td>
<td align="center">{Integer}</td>
</tr>
</tbody>
</table>

<table>
<thead>
<tr>
<th scope="col">Primary Key</th>
<th align="center" scope="col" rowspan="2" colspan="9">Attributes</th>
</tr>
<tr>
<th scope="col">Partition Key</th>
</tr>
<tr>
<th align="center" scope="col">is_stay</th>
<th align="center" scope="col">j_first_name</th>
<th align="center" scope="col">j_last_name</th>
<th align="center" scope="col">student_id</th>
<th align="center" scope="col">schedule</th>
</tr>
</thead>
<tbody>
<tr>
<td align="center">{Boolean}</td>
<td align="center">{String}</td>
<td align="center">{String}</td>
<td align="center">{Integer}</td>
<td align="center">{StringSet}</td>
</tr>
</tbody>
</table>
