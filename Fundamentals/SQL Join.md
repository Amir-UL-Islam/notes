> Join Algorithms
- Nester Loop [With 2 For Loop]
- Marge Join [Sort's the Table Then 1 Loop]
m_users

| id  | name |
| --- | ---- |
| 1   | Amir |
| 2   | Rize |
pksf_referrals

| id  | refer_to | user_id |
| --- | -------- | ------- |
| 1   | xyz      | 1       |
| 2   | xyz      | 3       |
| 3   | abc      | 1       |
1st => Sort the Tables

| id  | name |
| --- | ---- |
| 1   | Amir |
| 2   | Rize |
pksf_referrals

| id  | refer_to | user_id |
| --- | -------- | ------- |
| 1   | xyz      | 1       |
| 3   | abc      | 1       |
| 2   | xyz      | 3       |
2nd => 1 loop and the condition will work fine. As the `user_id` from will be **grouped**

- Hash Join [Create Hash Table of Joining Attribute]