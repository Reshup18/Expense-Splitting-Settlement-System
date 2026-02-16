# Expense Splitting & Settlement System

## Overview

This project implements a Group Expense Splitting and Debt Settlement System.

When multiple people share expenses (such as trips, shared housing, or events), tracking who owes whom becomes complicated. While calculating individual balances is straightforward, minimizing the number of settlement transactions requires logical optimization.

This system allows users to:
- Add shared expenses
- Track individual balances
- Generate a settlement plan
- View expense history

---

## Features

### 1. Add Shared Expense
User inputs:
- Person who paid
- Total amount
- Participants involved (comma separated)
- Description

The system splits the amount equally among participants.

---

### 2. View All Expenses
Displays:
- Payer
- Amount
- Participants
- Description

---

### 3. View Balances
Shows net balance of each person:

- Positive balance → Person should receive money
- Negative balance → Person owes money

---

### 4. Generate Settlement Plan
Core functionality of the system.

The system:
- Separates creditors (positive balance)
- Separates debtors (negative balance)
- Matches them using a greedy algorithm
- Minimizes number of transactions
- Clears all balances

Output format:
Person A pays Person B ₹X

---

## Approach

### Step 1: Balance Calculation

We maintain a dictionary:

balances = { person_name : net_balance }

When an expense is added:
- The payer's balance increases by the full amount.
- Each participant's balance decreases by their share.

This ensures:
Sum of all balances = 0

---

### Step 2: Settlement Algorithm (Greedy Approach)

1. Create two lists:
   - Creditors (balance > 0)
   - Debtors (balance < 0)

2. Match the first debtor with the first creditor.

3. Transfer the minimum of:
   - Amount debtor owes
   - Amount creditor should receive

4. Update balances.

5. Move to next person when balance becomes zero.

Continue until all balances are cleared.

---

## Data Structures Used

1. Dictionary
   - Stores balances
   - O(1) lookup and update
   - Efficient for tracking individuals

2. List
   - Stores expense history
   - Stores creditors and debtors
   - Simple and efficient for iteration

---

## How to Run

1. Open terminal.
2. Navigate to project folder.
3. Run:

python filename.py

4. Use menu options to:
   - Add expenses
   - View balances
   - Generate settlement plan

---

## Assumptions

- Expenses are split equally among participants.
- Names uniquely identify individuals.
- Money is handled using float (rounded to 2 decimal places).
- Basic input validation assumed.

---

## Edge Cases Handled

- Circular debts (balances automatically become zero)
- Person not involved in all expenses
- No expenses case
- Already settled case
- Large groups (tested with 10+ members)

---

## Complexity Analysis

Adding Expense:
Time Complexity: O(n)
Where n = number of participants in the expense.

Viewing Balances:
Time Complexity: O(n)

Settlement Generation:
Time Complexity: O(n²) in worst case
Because debtors and creditors are matched iteratively.

Space Complexity:
O(n + m)
Where:
n = number of people
m = number of expenses stored

---

## Limitations

- Floating point precision may cause minor rounding differences.
- Greedy settlement is efficient but not mathematically guaranteed minimal in all theoretical cases.
- No persistent storage (data resets after program ends).
- No concurrency handling.

---

## Possible Improvements

- Custom percentage split
- Use Decimal for better currency precision
- Persistent storage using file or database
- Multi-currency support
- UI or web interface
- More advanced optimal settlement algorithm

---

## Conclusion

This project demonstrates:
- Strong understanding of data structures
- Logical problem solving
- Algorithmic thinking
- Debt settlement optimization using greedy strategy

Suitable for placement-level discussion and interview evaluation.
