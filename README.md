# Currency-Converter-Program
For this program the task was to create a program for employees taking customer orders, which converted GBP into American Dollars, Euros, Brazilian Real, Japanese Yen and Turkish Lira. Also taking a commission fee depending on amount transferred as well as if the customer was an employee it would apply a 5% discount, finally printing it in an bill.


#Currencies
A_DOLLAR = 1.4
EURO = 1.14
B_REAL = 4.77
J_YEN = 151.05
T_LIRA = 5.68

#Commission fees
UNDER_300 = float(0.035) #3.5%
OVER_300 = float(0.03) # 3%
OVER_750 = float(0.025) # 2.5%
OVER_1000 = float(0.02) # 2%
OVER_2000 = float(0.015) # 1.5%

#Staff discount
STAFF_DISCOUNT = 0.05 # 5%

#Validates that the amount of pounds is within 1 - 2500 if it isnt than it asks the user to input another value
def validatePound(amountPound):
    while amountPound < 1 or amountPound > 2500:
        print("Invalid data.")
        print("------------------------------------------------------------------------------------------------------------------------------------------------------")
        amountPound = int(input("Enter the pounds being converted, (Maximum of 2500): "))
    return amountPound

#Validates that the chosen currency is one of the accepted currencies, otherwise it asks the user to input another value
def validateChosenCurrency(chosenCurrency):
    while chosenCurrency.lower() not in ("dollar", "euro", "real", "yen", "lira"):
        print("Invalid data.")
        print("------------------------------------------------------------------------------------------------------------------------------------------------------")
        chosenCurrency = str(input("Enter the currency the customer wishes to convert into, (Dollar, Euro, Real, Yen or Lira): "))
    return chosenCurrency

#Compares chosenCurrency to the available currencies, after it has compared it will calculate the converted value and get the currencies sign
def currencyFindAndCalc(chosenCurrency, amountPound):
    if chosenCurrency.lower() == "dollar":
        convertedValue = amountPound * A_DOLLAR
        currencySign = "$"
    elif chosenCurrency.lower() == "euro":
        convertedValue = amountPound * EURO
        currencySign = "€"
    elif chosenCurrency.lower() == "real":
        convertedValue = amountPound * B_REAL
        currencySign = "R$"
    elif chosenCurrency.lower() == "yen":
        convertedValue = amountPound * J_YEN
        currencySign = "¥"
    elif chosenCurrency.lower() == "lira":
        convertedValue = amountPound * T_LIRA
        currencySign = "₺"
    return convertedValue, currencySign

#Gets the commission based on the amount of pounds
def commissionFind(amountPound):
    if amountPound < 300:
        commission = UNDER_300
    elif amountPound < 750:
        commission = OVER_300
    elif amountPound < 1000:
        commission = OVER_750
    elif amountPound < 2000:
        commission = OVER_1000
    else:
        commission = OVER_2000
    return commission

#Prints the bill, as well as applying a discount if the customer is an employee
def bill(amountPound, commission, totalCost, currencySign, convertedValue, employeeYorN, baseAmount):
    print("------------------------------------Bill------------------------------------")
    print("Thank you for using our service,")
    print(f"You put in £{baseAmount:.2f}")
    print(f"Our commission fee for the amount is {commission*100}%")
    print(f"You converted £{amountPound:.2f} into {currencySign}{convertedValue:.2f}.")
    if employeeYorN.lower() == "yes":
        print(f"As an employee you are entitled to 5% discount,")
        discount = totalCost * STAFF_DISCOUNT
        finalCost = totalCost - discount
        print(f"Your final amount transfered £{finalCost:.2f}")
    else:
        print(f"The amount transfered is £{totalCost:.2f}")
    print("----------------------Thank you for using our service----------------------")


#Main programme
def main():
 #Asks the user for the number of pounds the passing it through the function, after its passes through it sets it as the base value
    amountPound = int(input("Enter the amount of pounds the customer wishes to convert (Maxiumum of £2500): "))
    amountPound = validatePound(amountPound)
    baseAmount = amountPound
    print("------------------------------------------------------------------------------------------------------------------------------------------------------")
    
 #Asks the user to choose a currency then passing it through the function to validate it
    chosenCurrency = str(input("Enter which currency the customer wishes to convert to, (Dollar, Euro, Real, Yen or Lira): "))
    chosenCurrency = validateChosenCurrency(chosenCurrency)
    
  #Gets the commission from the function, then calculating the transfered amount of money
    commission = commissionFind(amountPound)
    amountPound = amountPound-(amountPound*commission)
    
  #Gets the converetedValue and currencySign from the function
    convertedValue, currencySign = currencyFindAndCalc(chosenCurrency, amountPound)
    totalCost = amountPound
    print("------------------------------------------------------------------------------------------------------------------------------------------------------")

  #Asks if the customer is an employee, afterwards calling the bill function
    employeeYorN = str(input("Is the customer an employee: "))
    bill(amountPound, commission, totalCost, currencySign, convertedValue, employeeYorN, baseAmount)

#Initiates the program
main()
