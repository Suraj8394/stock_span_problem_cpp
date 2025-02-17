📌 **Explanation: Stock Span Problem**

🔍 **Problem Understanding**  
We are given an array of stock prices for `n` days, and the task is to find the **span** of stock's price for each day. The span of a stock's price is defined as the maximum number of consecutive days (including the current day) the stock price has been less than or equal to the current day's price.

📌 **Example Walkthrough**  
Example 1:  
Input: `[100, 80, 60, 70, 60, 75, 85]`  
Output: `[1, 1, 1, 2, 1, 4, 6]`  
Explanation:  
- Day 1: Price is 100 → Span = 1  
- Day 2: Price is 80 → Span = 1  
- Day 3: Price is 60 → Span = 1  
- Day 4: Price is 70 → Span = 2 (70 > 60)  
- Day 5: Price is 60 → Span = 1  
- Day 6: Price is 75 → Span = 4 (75 > 60, 70, 80, 100)  
- Day 7: Price is 85 → Span = 6 (all prices are less than 85)

🚀 **Approach: Stack-based Approach**  
The most efficient solution is to use a **stack**. A stack allows us to keep track of the indices of elements in the array while maintaining the necessary comparisons in an efficient manner.  

🔢 **Step-by-Step Breakdown**  
🔹 **Step 1**: Initialize an empty stack.  
🔹 **Step 2**: For each stock price, compare it with the top of the stack.  
    - If the current price is greater than the price at the top of the stack, pop elements from the stack.  
🔹 **Step 3**: Calculate the span for the current day by checking the difference between the current index and the index from the stack’s top.  
🔹 **Step 4**: Push the current index to the stack.  

💻 **Code Implementation**  
```cpp
#include <iostream>
#include <stack>
#include <vector>
using namespace std;

vector<int> calculateSpan(const vector<int>& prices) {
    int n = prices.size();
    vector<int> span(n);
    stack<int> s;  // Stack to store indices

    for (int i = 0; i < n; ++i) {
        while (!s.empty() && prices[s.top()] <= prices[i]) {
            s.pop();
        }
        span[i] = (s.empty()) ? i + 1 : i - s.top();
        s.push(i);
    }

    return span;
}

int main() {
    vector<int> prices = {100, 80, 60, 70, 60, 75, 85};
    vector<int> result = calculateSpan(prices);

    for (int i : result) {
        cout << i << " ";
    }
    return 0;
}
```


1. **Initialization**:
   - `vector<int> span(n);`: A vector to store the span values for each price. Each element will store the span of the corresponding stock price.
   - `stack<int> s;`: A stack to store indices of the stock prices as we traverse the list.

2. **Main Loop (`for` loop)**:
   - We iterate through the prices one by one, with `i` representing the index of the current price.
   
3. **While Loop**:
   - Inside the `for` loop, there's a `while` loop that pops elements from the stack as long as the price at the top of the stack is less than or equal to the current price (`prices[s.top()] <= prices[i]`). This ensures that the stack holds only the indices of prices that are greater than the current price.
   
4. **Span Calculation**:
   - After popping smaller prices from the stack, if the stack is empty, it means no price is greater than the current price, so the span for that price is `i + 1` (the number of days from the start to the current day).
   - If the stack is not empty, the span is the difference between the current index `i` and the index at the top of the stack (`i - s.top()`). This gives the number of consecutive days with prices smaller than or equal to the current price.

5. **Pushing Current Index**:
   - After calculating the span for the current price, we push the index `i` onto the stack to keep track of it for the next comparisons.

6. **Final Output**:
   - After the loop finishes, the `span` vector will contain the span values for all the stock prices, which we print out in the `main` function.

### **Key Points**:
- **Stack Usage**: The stack ensures that we can efficiently keep track of the indices of the stock prices that are relevant for calculating the span. Each price is pushed and popped from the stack at most once, so the time complexity is linear, i.e., `O(N)`.
- **Span Calculation**: By maintaining the stack, we can calculate the span for each price in constant time after popping the smaller prices.

This method is highly efficient with a time complexity of **O(N)** and space complexity of **O(N)**, making it suitable for large inputs.

---

📌 **Dry Run of the Code**  
🔹 **Initial State**:  
List: `[100, 80, 60, 70, 60, 75, 85]`  
🔹 **Step 1**: Initialize an empty stack.  
🔹 **Step 2**: Traverse through the list:  
- For 100, no previous prices, so span is 1.  
- For 80, no prices greater, span is 1.  
- For 60, no prices greater, span is 1.  
- For 70, 60 is smaller, span is 2.  
- For 60, no prices greater, span is 1.  
- For 75, all previous prices are smaller, span is 4.  
- For 85, all previous prices are smaller, span is 6.  
🔹 **Step 3**: Final result: `[1, 1, 1, 2, 1, 4, 6]`

⏳ **Time & Space Complexity Analysis**  
Operation | Time Complexity | Explanation  
---|---|---  
Finding span | O(N) | Traverse the list once using the stack  
Overall Complexity | O(N) | Single pass solution  

✅ **Optimized Approach**: This solution runs in **O(N)** time and uses **O(N)** space for the stack.

🔥 **Key Takeaways**  
✔ Stack-based approach is efficient for maintaining previous prices.  
✔ Each price is processed once, ensuring an optimal solution.  
✔ The time complexity is linear, making this method highly efficient for large inputs.



