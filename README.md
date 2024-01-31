# Code Smells
Examples of Code smells and Clean code

I am making a curated list of common code smells and their respective clean code in Swift and Kotlin programming languages.

Before jumping into the code smelss, here is an overview of common code smells:
- Duplicate Code
- Long Method
- Long Parameter List
- Uncommunicative Name
- Type Embedded in Name
- Magic Numbers
- Inconsistent Names
- Data Class

The types of code smells can vary, but they generally include characteristics in the source code that may indicate a deeper problem. Also an important thing to note here is that these code smells are not necessarily bugs, but they can indicate weaknesses in design, slow down development, or increase the risk of bugs or failures. Identifying and addressing code smells is an important aspect of maintaining code quality and preventing technical debt.

Here are the examples of smelly code and clean code:

## Swift

### Example of Duplicate Code
#### Smelly Code
```
class FruitModel {
    var fruits: [Fruit]
    var searchedText: String?
    
    init() {
        //initialize
    }
    
    func getFruit() -> Int {
        if let text = searchedText {
            if !text.isEmpty {
                let searchedFruits = fruits.filter { code }
                return searchedFruits.count
            }
        }
        return fruits.count
    }
    
    func getFruitByIndex(_ at: Int) -> Fruit {
        if let text = searchedText {
            if !text.isEmpty {
                let searchedFruits = fruits.filter { code }
                return searchedFruits[at]
            }
        }
        return fruits[at]
    }
}
```
#### Clean Code

```
class FruitModel {
    var fruits: [Fruit]
    var searchedText: String?
    
    init() {
        //initialize
    }
    
    func getFruit() -> Int {
        return getFruits().count
    }
    
    func getFruitByIndex(_ at: Int) -> Fruit {
        return getFruits()[at]
    }
    
    private func getFruits() -> [Fruit] {
        if let text = searchedText, !text.isEmpty {
            return fruits.filter { code }
        }
        return fruits
    }
}
```

In the above example, the "Smelly Code" section demonstrates duplicate code in the getFruit() and getFruitByIndex() methods. The "Clean Code" section shows the refactored version, which extracts the duplicate code into a private method getFruits(), making the code more readable and maintainable.

### Example of Long Method
#### Smelly Code
```
func calculateTotalPrice(quantity: Int, price: Double, tax: Double) -> Double {
    let subTotal = Double(quantity) * price
    let totalTax = subTotal * tax
    return subTotal + totalTax
}
```

#### Clean code
```
func calculateTotalPrice(quantity: Int, price: Double, tax: Double) -> Double {
    return calculateSubTotal(quantity: quantity, price: price) + calculateTotalTax(subTotal: subTotal, tax: tax)
}

func calculateSubTotal(quantity: Int, price: Double) -> Double {
    return Double(quantity) * price
}

func calculateTotalTax(subTotal: Double, tax: Double) -> Double {
    return subTotal * tax
}
```

In the above example, the smelly code contains a long method that calculates the total price of an item. The clean code, however, refactors the long method into shorter methods, making the code more readable and maintainable.

### Example of Long Parameter List
#### Smelly Code
```
func createNewUser(name: String, age: Int, address: String, email: String, phone: String, username: String, password: String) {
    // Method implementation
}
```

#### Clean code
```
struct User {
    var name: String
    var age: Int
    var address: String
    var email: String
    var phone: String
    var username: String
    var password: String
}

func createNewUser(user: User) {
    // Method implementation
}
```

In the above example, the smelly code contains a long parameter list in the createNewUser method. The clean code, however, refactors the long parameter list into a single parameter of type User, making the code more readable and maintainable.

### Example of Uncommunicative Name
#### Smelly Code
```
func calculate(a: Double, b: Double, c: Double, d: Double, e: Double) -> Double {
    // Method implementation
}
```

#### Clean Code
```
func calculateTotalPrice(basePrice: Double, tax: Double, discount: Double, shippingCost: Double, additionalFees: Double) -> Double {
    // Method implementation
}
```

### Example of Type Embedded in Name
#### Smelly Code
```
var userNameString: String
func calculateTotalPriceDouble(quantityInt: Int, priceDouble: Double)
```

#### Clean Code
```
var userName: String
func calculateTotalPrice(quantity: Int, price: Double)
```

In the smelly code, the type is embedded in the variable and function names, leading to redundant and less readable code. The clean code, however, uses clear and concise names without embedding the type, leading to more maintainable and readable code.

### Example of Magic Numbers
#### Smelly Code
```
func calculateArea(radius: Double) -> Double {
    return 3.14 * radius * radius
}
```

#### Clean Code
```
let pi = 3.14
func calculateArea(radius: Double) -> Double {
    return pi * radius * radius
}
```

In the smelly code, the value of π (pi) is hard-coded as 3.14, which is a magic number. In the clean code, the magic number is replaced with a named constant pi, making the code more readable and maintainable.

### Example of Inconsistent Names
#### Smelly Code
```
func calculateTotalPrice(quantity: Int, price: Double, tax: Double) -> Double {
    let subTotal = Double(quantity) * price
    let totalTax = subTotal * tax
    return subTotal + totalTax
}
```

### Clean Code
```
func calculateTotalPrice(itemQuantity: Int, itemPrice: Double, itemTax: Double) -> Double {
    let subTotal = Double(itemQuantity) * itemPrice
    let totalTax = subTotal * itemTax
    return subTotal + totalTax
}
```

In the smelly code, the parameter names are inconsistent and do not clearly convey their purpose, making the code harder to understand and maintain. In the clean code, the parameter names are more consistent and descriptive, making the code more readable and maintainable.

### Example of Inconsistent Names
#### Smelly Code
```
struct Product {
    var name: String
    var price: Double
    var category: String
    var inStock: Bool
}
```

#### Clean Code
```
struct Product {
    var name: String
    var price: Double
    var category: String
    
    func isAvailableInStock() -> Bool {
        // Method implementation
    }
}
```
In the smelly code, the Product struct only contains data and no behavior. In the clean code, the isAvailableInStock method is added to provide behavior to the Product struct, addressing the "Data Class" code smell.
