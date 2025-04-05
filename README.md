Here's a Systematic Withdrawal Plan (SWP) calculator app using Python and Tkinter:

```python
import tkinter as tk
from tkinter import ttk
from math import pow

class SWPCalculator:
    def __init__(self, root):
        self.root = root
        self.root.title("SWP Calculator")
        self.root.geometry("400x350")
        
        # Variables
        self.principal = tk.DoubleVar()
        self.rate = tk.DoubleVar()
        self.frequency = tk.StringVar()
        self.years = tk.IntVar()
        self.result = tk.StringVar()
        
        self.create_widgets()
    
    def create_widgets(self):
        # Input Frame
        input_frame = ttk.Frame(self.root, padding=10)
        input_frame.pack(pady=10)
        
        # Principal Amount
        ttk.Label(input_frame, text="Initial Investment:").grid(row=0, column=0, sticky=tk.W)
        ttk.Entry(input_frame, textvariable=self.principal).grid(row=0, column=1)
        
        # Annual Interest Rate
        ttk.Label(input_frame, text="Annual Interest Rate (%):").grid(row=1, column=0, sticky=tk.W)
        ttk.Entry(input_frame, textvariable=self.rate).grid(row=1, column=1)
        
        # Withdrawal Frequency
        ttk.Label(input_frame, text="Withdrawal Frequency:").grid(row=2, column=0, sticky=tk.W)
        frequency_combo = ttk.Combobox(input_frame, textvariable=self.frequency, 
                                     values=["Monthly", "Quarterly", "Half-Yearly", "Yearly"])
        frequency_combo.grid(row=2, column=1)
        frequency_combo.current(0)
        
        # Withdrawal Period
        ttk.Label(input_frame, text="Withdrawal Period (years):").grid(row=3, column=0, sticky=tk.W)
        ttk.Entry(input_frame, textvariable=self.years).grid(row=3, column=1)
        
        # Calculate Button
        ttk.Button(self.root, text="Calculate SWP", command=self.calculate_swp).pack(pady=10)
        
        # Result Display
        result_frame = ttk.Frame(self.root, padding=10)
        result_frame.pack()
        ttk.Label(result_frame, text="Monthly Withdrawal Amount:").pack()
        ttk.Label(result_frame, textvariable=self.result, font=('Helvetica', 12, 'bold')).pack()
    
    def calculate_swp(self):
        try:
            P = self.principal.get()
            r = self.rate.get() / 100
            years = self.years.get()
            
            freq_map = {
                "Monthly": 12,
                "Quarterly": 4,
                "Half-Yearly": 2,
                "Yearly": 1
            }
            n = freq_map[self.frequency.get()]
            
            total_periods = n * years
            rate_per_period = r / n
            
            # SWP formula
            swp = (P * rate_per_period) / (1 - pow(1 + rate_per_period, -total_periods))
            
            self.result.set(f"₹{swp:,.2f}")
        except ValueError:
            self.result.set("Invalid input!")
        except ZeroDivisionError:
            self.result.set("Error in calculation")

if __name__ == "__main__":
    root = tk.Tk()
    app = SWPCalculator(root)
    root.mainloop()
```

This SWP calculator:

1. Takes inputs for:
   - Initial investment amount
   - Annual interest rate
   - Withdrawal frequency (Monthly/Quarterly/Half-Yearly/Yearly)
   - Withdrawal period in years

2. Calculates the fixed withdrawal amount using the formula:
   ```
   SWP = (P * r/n) / [1 - (1 + r/n)^(-n*t)]
   Where:
   P = Principal amount
   r = Annual interest rate
   n = Number of withdrawals per year
   t = Number of years
   ```

3. Features:
   - Dropdown menu for frequency selection
   - Error handling for invalid inputs
   - Formatted currency output
   - Simple and intuitive GUI

To use:
1. Enter your initial investment amount
2. Input the expected annual return rate
3. Select withdrawal frequency
4. Enter the number of years for withdrawals
5. Click "Calculate SWP" to see the periodic withdrawal amount

Example:
For ₹1,000,000 investment at 8% annual return with monthly withdrawals over 10 years:
SWP = ₹12,133.23 per month

Note: This assumes a constant rate of return and doesn't account for market fluctuations or taxes. Actual returns may vary.# Swp-calculator-app-
