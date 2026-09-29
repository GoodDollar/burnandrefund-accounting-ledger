### How to read the accounting ledgers

There is one ledger for each chain. 
Each covers transactions involving selected G$ pools or trading contracts from **2 to 18 September 2026**.

The ledger labels recognizable trades as **buys** or **sales** and records the G$ amount, what was paid or received, and the calculated USD amount. 
A sale can appear even if that wallet has no earlier recorded buy. 
Recognized liquidity movements and G$ outflows that could not be explained as trades are listed separately; they are not counted as trade profit or loss but subsequently have been analyzed to determine their action and destinations (liquidity movements)

The reported P/L is **USD received from recorded sales minus USD spent on recorded buys**. 

### How to verify your address
The zip in this repository consists of 3 files, one ledger.json for each chain.

Open the file for the relevant chain. you can just CTRL + F for your address (**in lowercase!**). 
all hits are either buy/sale. the last hit for your address is the breakdown of the totals.
your address should match when its put as 'receiver' in 'totals' section.

That totals set shows:

| Field | Meaning |
|---|---|
| `buyCount`, `sellCount` | Number of recognized buys and sales counted for the address. |
| `gdBought`, `gdSold` | G$ bought and sold; both totals are shown as positive amounts. |
| `knownCostUsd` | USD value spent on recorded buys. |
| `knownEarningsUsd` | USD value received from recorded sales. |
| `knownProfitLossUsd` | Recorded earnings minus recorded costs. |
| `gdOutflowCandidateCount`, `gdOutflowCandidate` | G$ outflows that could not be classified as trades. These are **not losses** in the P/L figure. |
| `latestGdBalance` | Balance at the ledger’s saved cutoff block |

To check individual numbers per trade, look at the others hits for you addresses. 
Each buy or sale shows its transaction hash, date, G$ amount, other tokens paid or received, USD calculation, and the address credited with the trade. 
Match the transaction hash against its on-chain transaction. On **Celo**, use `accountingOwner` to see whose total receives a sale; on **Fuse and XDC**, use `receiver`.

Two details matter: 
tiny entries identified in `dustEvents` are visible in the JSON but excluded from totals, and an event without a complete price is not added to `knownProfitLossUsd`. 
Celo may also show `profitsAsRecipient`—proceeds received on someone else’s behalf—which is informational and is not added to that recipient’s trade P/L.

These figures describe **recorded trade spending and proceeds**, not the full value of G$ still held or an approved refund.



A simpler instruction is: **Search for your address near the end of the file and check that the match is in `"receiver": "your-address"` within `totals`.** If the last hit is instead in `recipientProfitCallers`, search backward for your `receiver` row.
