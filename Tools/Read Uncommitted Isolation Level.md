How much of one transaction is visible to other.
- t1 Transaction:
	- `SELECT * FROM TableA;`
- t2 Transaction:
	- `UPDATE TableA SET username = 'Adib001' WHERE id = 1`;

What will be visible if t1 is running while t2 is running.

In case of 
- Uncommitted Read -> t1 may ready uncommitted updates from t2.
	- Dirty Read ->  Read Uncommitted
	-  Phantom Read -> Number of count might be different
	- No-Repeatable -> Result might NOT Be Same again